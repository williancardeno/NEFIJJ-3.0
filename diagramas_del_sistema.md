# Diagramas del sistema — NEFIJJ 3.0

Los siguientes diagramas se rediseñaron tomando como referencia visual los ejemplos suministrados: arquitectura cliente-servidor, flujo de autorización y modelo relacional. El contenido se contrastó con el código actual. No se agregan entidades ni funciones que el proyecto no tenga; en particular, protocolos de emergencia y alertas no forman parte del modelo actual.

## 1. Arquitectura local

[Abrir imagen PNG de arquitectura](diagramas_png/01_arquitectura.png)

![Arquitectura local de NEFIJJ](diagramas_png/01_arquitectura.png)

El navegador representa el sitio de administración Django que existe en `/admin/`. La interfaz principal para los roles de la institución es la aplicación móvil. El backend usa Django ORM para persistir en MySQL/MariaDB local. Las evidencias se guardan como archivos y se consultan por la API autenticada.

```mermaid
flowchart LR
    subgraph C[Clientes]
        M[App móvil<br/>React Native + Expo]
        W[Navegador web<br/>Django Admin]
    end
    subgraph DEV[Computador de desarrollo / red local]
        API[API REST<br/>Django REST Framework<br/>JWT y permisos por tenant]
        ADM[Django Admin]
        ORM[Django ORM]
        DB[(MySQL / MariaDB local<br/>nefijj_db · puerto 3308)]
        FS[(Archivos locales<br/>evidencias)]
        API --> ORM
        ADM --> ORM
        ORM --> DB
        API --> FS
    end
    M -->|JSON / HTTP local<br/>Bearer JWT| API
    W -->|HTTP local<br/>sesión administrativa| ADM
```

## 2. Validación de acceso y flujo por rol

[Abrir imagen PNG del flujo de autorización](diagramas_png/02_flujo_roles.png)

![Flujo de acceso, organización activa y permisos por rol](diagramas_png/02_flujo_roles.png)

La autorización se aplica en cada operación del servidor. Un estudiante con cuenta existente y sin membresía puede iniciar sesión y aceptar una invitación válida; una cuenta de soporte no se vincula mediante ese flujo. Para administradores se valida la organización; para técnicos y usuarios también se comprueba la sede y membresía activa correspondiente. El superadministrador puede administrar organizaciones y consultar incidencias globales, pero no efectuar cambios operativos sobre incidencias.

```mermaid
flowchart TD
    A[Inicio de sesión: API emite JWT] --> B{¿Superadministrador?}
    B -->|Sí| S[Gestiona organizaciones<br/>Consulta incidencias globales]
    S --> S2[Incidencias en solo lectura]
    B -->|No| C{¿Organización y ámbito solicitado activos?}
    C -->|No| X[Acceso denegado]
    C -->|Sí| D{¿Membresía activa?}
    D -->|No, cuenta user existente| E[Acepta invitación vigente<br/>con sesión iniciada]
    E --> D
    D -->|Sí| F[API valida rol y alcance en cada petición]
    F --> G[organization_admin<br/>Gestiona su organización,<br/>sedes, personal, categorías,<br/>rutas, invitaciones e incidencias]
    F --> H[technician<br/>Consulta su sede;<br/>actualiza solo asignadas:<br/>pendiente → en_proceso → resuelto]
    F --> I[user<br/>Crea incidencias y consulta<br/>solo sus propios reportes]
```

## 3. Modelo relacional actual

[Abrir imagen PNG del modelo relacional](diagramas_png/03_modelo_datos.png)

![Modelo relacional vigente de NEFIJJ](diagramas_png/03_modelo_datos.png)

El diagrama resume las entidades existentes en los modelos Django: organizaciones, sedes, usuarios, membresías, invitaciones, categorías, rutas de técnico, incidencias e historial de eventos. `PK` es clave primaria, `FK` clave foránea y `UK` campo o combinación única. Los campos agrupados son una síntesis visual, no el esquema SQL completo.

```mermaid
erDiagram
    ORGANIZATION ||--o{ LOCATION : contains
    ORGANIZATION ||--o{ ORGANIZATION_MEMBERSHIP : grants
    ORGANIZATION ||--o{ CATEGORY : defines
    ORGANIZATION ||--o{ ORGANIZATION_INVITATION : issues
    ORGANIZATION ||--o{ INCIDENT : scopes
    USER ||--o{ ORGANIZATION_MEMBERSHIP : member
    LOCATION o|--o{ ORGANIZATION_MEMBERSHIP : assigned_location
    LOCATION ||--o{ ORGANIZATION_INVITATION : invitation_site
    USER ||--o{ ORGANIZATION_INVITATION : creates_or_accepts
    CATEGORY ||--o{ CATEGORY_TECHNICIAN : route
    LOCATION ||--o{ CATEGORY_TECHNICIAN : route_site
    USER ||--o{ CATEGORY_TECHNICIAN : technician
    CATEGORY ||--o{ INCIDENT : classifies
    LOCATION ||--o{ INCIDENT : locates
    USER ||--o{ INCIDENT : reports
    USER o|--o{ INCIDENT : assigned_technician
    INCIDENT ||--o{ INCIDENT_EVENT : history
    USER ||--o{ INCIDENT_EVENT : actor

    ORGANIZATION {
      int id PK
      string name
      string slug UK
      string status
    }
    LOCATION {
      int id PK
      int organization_id FK
      string name
      string code UK
      boolean is_active
    }
    USER {
      int id PK
      string username UK
      string email UK
      string role
      int location_id FK
      boolean is_active
    }
    ORGANIZATION_MEMBERSHIP {
      int id PK
      int organization_id FK
      int user_id FK
      int location_id FK
      string role
      boolean is_active
    }
    ORGANIZATION_INVITATION {
      int id PK
      int organization_id FK
      int location_id FK
      int created_by_id FK
      int used_by_id FK
      string token_hash UK
      datetime expires_at
      datetime revoked_at
      datetime used_at
    }
    CATEGORY {
      int id PK
      int organization_id FK
      string name
      boolean is_active
    }
    CATEGORY_TECHNICIAN {
      int id PK
      int category_id FK
      int location_id FK
      int technician_id FK
      string category_location UK
    }
    INCIDENT {
      int id PK
      int organization_id FK
      int location_id FK
      int reported_by_id FK
      int category_id FK
      int assigned_to_id FK
      string title
      string priority
      string status
      string evidence_image
    }
    INCIDENT_EVENT {
      int id PK
      int incident_id FK
      int actor_id FK
      string event_type
      json old_value
      json new_value
      datetime created_at
    }
```

### Nota sobre las migraciones

Las entidades de invitación y enrutamiento están definidas en el código, pero sus migraciones siguen pendientes de revisión antes de aplicarse a la base MySQL local con esquema legado. El diagrama representa el modelo Django, no confirma que todas las tablas existan actualmente en esa base.
