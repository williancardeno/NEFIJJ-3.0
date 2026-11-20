# NEFIJJ 3.0

NEFIJJ es una aplicación móvil y una API para reportar, asignar y dar seguimiento a incidencias de infraestructura y operación en instituciones con varias organizaciones y sedes.

## Estado del proyecto

El repositorio contiene una app React Native/Expo y una API Django REST Framework. El código incluye autenticación, gestión de organizaciones, sedes, personal, categorías, invitaciones QR, reportes con evidencia y cambios de estado con permisos por rol. Esto describe funciones presentes en el código; no equivale a una certificación de funcionamiento en producción. La validación física con Expo Go y la operación sobre la base MySQL existente están pendientes.

**No ejecutes `manage.py migrate` en `nefijj_db` ni uses un script SQL de reconstrucción sin revisar antes el esquema y aprobar un plan.** La base local se describe como legado y las migraciones de invitaciones y enrutamiento aún no se han aplicado allí. El SQL destructivo que antes estaba incluido en este README se retiró para evitar que se confunda con instrucciones de instalación.

## Documentación

- [Problemática y solución](problematica_y_solucion.md): necesidad atendida, usuarios y alcance.
- [PRD y propuesta](prd_y_propuesta_del_proyecto.md): requisitos y objetivos del producto.
- [Arquitectura y diagramas](diagramas_del_sistema.md): componentes, entidades y flujos.
- [Arquitectura del sistema](arquitectura_del_sistema.md): decisiones de despliegue, datos, roles y API.
- [Manual de usuario](manual_usuario.md): instrucciones de uso por rol.
- [Libreto de presentación](libreto_presentacion.md): guion para exponer y defender el proyecto.
- [Diagnóstico y brechas](diagnostico_y_brechas.md): estado documental y funcional conocido, límites y pendientes.
- [Plan de pruebas y validación](Plan%20de%20Pruebas%20y%20Validaci%C3%B3n.md): casos de aceptación definidos; CP08 físico pendiente.
- [Tareas del proyecto](TASKS.md): fases registradas y trabajo pendiente.
- [Decisiones técnicas](DECISIONS.md): decisiones vigentes del proyecto.
- [Guía de desarrollo backend](Gu%C3%ADa%20de%20Desarrollo%20Backend.md) y [guía móvil](Gu%C3%ADa%20de%20Desarrollo%20Mobile.md): configuración local y ejecución.

## Componentes

- `backend/`: API Django REST Framework, autenticación JWT y persistencia MySQL.
- `mobile/`: cliente React Native con Expo, interfaz en `App.js` y servicios HTTP bajo `src/services/`.
- Los archivos `.env` y `.env.local` deben ser locales, no compartirse ni contener credenciales comprometidas.

## Inicio local

Consulta las guías de desarrollo antes de iniciar los servicios. En resumen, se requiere Python y dependencias del backend, Node.js/npm y dependencias móviles, MySQL/MariaDB local compatible y una IP LAN alcanzable desde el teléfono. Configura `backend/.env` y `mobile/.env.local` a partir de los ejemplos disponibles (si existen), establece la URL LAN de la API y arranca el servidor Django en `0.0.0.0:8000`; luego inicia Expo usando el script `start:lan` de `mobile/package.json`.

No se incluyen credenciales predeterminadas. Se necesita una cuenta previamente provisionada. La recuperación de contraseña no está implementada. Para hacer funcionar en MySQL las funciones que dependen de las nuevas tablas se debe revisar y aprobar primero la compatibilidad de migraciones con la base concreta.

## Alcance

NEFIJJ es una solución de gestión y trazabilidad de incidencias. No es un sistema de emergencias ni garantiza atención en tiempo real. Protocolos operativos y alertas automáticas están pendientes según el estado documentado.
