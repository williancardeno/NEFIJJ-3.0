# Manual de usuario — NEFIJJ

## 1. Antes de empezar

NEFIJJ necesita una cuenta provisionada por la institución. No tiene registro público ni recuperación de contraseña. En una prueba local, el backend debe estar activo, el móvil debe tener `EXPO_PUBLIC_API_URL` con la dirección LAN correcta y el teléfono debe alcanzar la computadora por la misma red Wi-Fi. Sigue las guías de desarrollo para iniciar los servicios.

La pantalla de acceso no sustituye la creación de una cuenta. Si no tienes usuario o no puedes acceder, contacta al administrador institucional.

## 2. Iniciar y cerrar sesión

1. Abre NEFIJJ desde Expo Go o desde la instalación que te haya entregado la institución.
2. Ingresa el nombre de usuario y contraseña asignados y pulsa **Iniciar sesión**.
3. Si tu cuenta aún no está vinculada a una sede, la app te llevará a **Vincular organización**.
4. Para salir, usa **Salir** en la barra superior.

La app guarda la sesión en el almacenamiento seguro del dispositivo para intentar restaurarla al abrir de nuevo la aplicación. Cierra la sesión si compartes el teléfono.

## 3. Estudiante o usuario: vincular cuenta y reportar

### Vincularse con QR

1. Solicita una invitación vigente al administrador de tu organización.
2. Inicia sesión con tu cuenta existente.
3. En **Vincular organización**, escanea el QR de invitación o escribe el código legible.
4. Confirma la vinculación cuando la app muestre el resultado.

El código es de un solo uso y expira. Si fue usado, revocado o venció, pide otra invitación. Si el escáner no está disponible o la cámara no tiene permiso, usa el campo para escribir el código.

### Crear un reporte

1. En **Incidencias**, pulsa **Nuevo reporte**.
2. Escribe título y descripción.
3. Selecciona una categoría activa y una prioridad: baja, media, alta o crítica.
4. Opcionalmente adjunta una imagen desde **Elegir de galería** o **Tomar foto**. Concede el permiso solicitado por el teléfono.
5. Pulsa **Enviar reporte** y espera la confirmación.

La incidencia aparecerá en tu lista. Si no hay categorías disponibles, informa al administrador. La aplicación no muestra una promesa de tiempo de respuesta.

## 4. Técnico: consultar y actualizar

1. Inicia sesión con tu cuenta técnica.
2. Revisa **Incidencias**; la API limita la lista a tu sede.
3. Abre/consulta la tarjeta del reporte y la evidencia disponible.
4. En los casos asignados a tu cuenta, usa la acción de cambio de estado que presenta la tarjeta.
5. Avanza de **Pendiente** a **En proceso** y luego a **Resuelto**.

Un técnico no puede actualizar reportes asignados a otra persona, saltar estados ni operar incidencias de otra sede. Si el botón no aparece, valida la asignación con el administrador.

## 5. Administrador de organización

Los controles de administración aparecen en la barra superior según el rol.

### Sedes

En **Sedes**, selecciona la organización, crea una sede con nombre y código, y usa la acción de estado para activar o desactivar una sede. Una sede inactiva deja de habilitar el acceso operativo correspondiente.

### Técnicos

En **Técnicos**, selecciona la sede, completa los datos de la cuenta y la contraseña inicial y crea el técnico. La lista permite activar o desactivar su acceso. Entrega las credenciales iniciales de forma privada y recomienda cambiarlas; no las envíes en un QR.

### Categorías y enrutamiento

En **Categorías**, selecciona la organización, crea o edita categorías y cambia su estado. Para asignar incidencias automáticamente, elige categoría, sede y técnico y guarda la ruta. Una categoría sin ruta puede producir casos sin asignación automática. Las categorías se desactivan; no se eliminan desde la API.

### Accesos QR

En **Accesos QR**, elige una sede activa y genera una invitación. Comparte el código/QR mostrado de forma segura; el secreto se presenta al crear la invitación y no se vuelve a recuperar desde la lista. Puedes revocar invitaciones que no se hayan utilizado. La persona invitada necesita una cuenta existente.

## 6. Superadministrador

En **Organizaciones**, crea una organización y activa o suspende su estado. Desde esa administración también puedes crear administradores de organización, activar/desactivar su membresía, restablecer su contraseña o eliminar su cuenta según las opciones disponibles.

La lista de incidencias del superadministrador es global y de consulta. No puede crear incidencias ni cambiar su estado desde la app.

## 7. Perfil y contraseña

En **Perfil** puedes consultar la cuenta y cambiar tu contraseña proporcionando la contraseña actual y confirmando la nueva. La recuperación de una contraseña olvidada desde el acceso no está implementada; solicita ayuda al administrador institucional.

## 8. Problemas frecuentes

| Síntoma | Qué revisar |
|---|---|
| La app indica que configures la conexión | Verifica `EXPO_PUBLIC_API_URL`; no uses `localhost` en un teléfono físico |
| No inicia sesión o no carga datos | Confirma que el backend esté levantado y accesible por la IP LAN, y que la cuenta esté activa |
| No permite vincular el QR | Confirma que la sesión sea de una cuenta de estudiante existente y que el código no haya vencido, sido revocado o usado |
| No puedes adjuntar una foto | Concede permiso de cámara/galería en los ajustes del teléfono |
| No aparecen categorías | Pide al administrador que active o cree categorías para la organización |
| El técnico no puede cambiar un estado | Confirma que el caso esté asignado a ese técnico y que siga el orden de estados permitido |
| La invitación o el enrutamiento falla contra MySQL | Las migraciones requeridas pueden no estar aplicadas; solicita revisión técnica antes de alterar la base |

## 9. Uso responsable

Adjunta solo imágenes relacionadas con la incidencia. Evita incluir rostros, documentos u otros datos personales si no son necesarios. La app no es un canal de emergencia; usa los canales oficiales de la institución para situaciones urgentes.
