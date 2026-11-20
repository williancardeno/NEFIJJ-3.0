# Diagnóstico y brechas — NEFIJJ 3.0

## Criterio de lectura

Este diagnóstico se elaboró leyendo la documentación y contrastándola con los archivos fuente presentes en el repositorio. No se ejecutó el sistema ni se corrieron pruebas durante esta revisión. Por eso distingue entre **presente en el código**, **registrado como probado por la documentación** y **validación pendiente**.

## Solicitud académica y respuesta documental

| Requisito | Estado | Evidencia / acción documental |
|---|---|---|
| Identificar una problemática | Documentado | [Problemática y solución](problematica_y_solucion.md) formula el problema y aclara que no hay estudio de campo documentado |
| Presentar solución funcional | Parcial | Hay código para los flujos principales, pero operación MySQL y validación física aún no se certifican; ver brechas abajo |
| Incluir diagramas | Cubierto | [Diagramas del sistema](diagramas_del_sistema.md) incluye arquitectura, entidades y flujos de reporte e invitación |
| Mantener archivos `.md` coherentes | Mejorado | README renovado, nuevos documentos y enlaces al PRD, arquitectura, decisiones y tareas existentes |
| Incluir libreto | Cubierto | [Libreto de presentación](libreto_presentacion.md), con guion, demo y preguntas previsibles |
| Explicar qué soluciona | Cubierto | [Problemática y solución](problematica_y_solucion.md) |
| Manual de usuario | Cubierto | [Manual de usuario](manual_usuario.md), por rol y con solución de problemas comunes |

## Funciones observadas en el código

- Autenticación JWT, perfil y cambio de contraseña autenticado.
- Roles efectivos y reglas de membresía para estudiantes, técnicos, administradores y superadministrador.
- Gestión de organizaciones, sedes, administradores y técnicos.
- Gestión de categorías y rutas de técnico por sede.
- Creación y consulta de incidencias; evidencia opcional y endpoint autenticado.
- Cambio de estado por técnico asignado y registro de eventos de incidencia.
- Creación, listado, revocación y aceptación de invitaciones QR.
- Cliente móvil Expo con pantallas para los flujos principales identificados.

La presencia de código no demuestra por sí sola que todos estos flujos funcionen en la configuración local o en producción.

## Brechas funcionales y operativas

1. **Migraciones MySQL pendientes.** Las migraciones `accounts.0002_organization_invitation` e `incidents.0002_categorytechnician_and_more` agregan estructuras que usan los flujos de invitaciones y enrutamiento. La documentación advierte que aún no se aplican a `nefijj_db` por ser un esquema legado. Se requiere inventariar y respaldar la base, comparar esquema y migraciones, preparar plan de reversión y validar en una copia antes de solicitar aprobación para producción/local compartida.
2. **Prueba física end-to-end pendiente.** CP08 está marcado pendiente: instalación/Expo Go, cámara, QR, red LAN, subida y consulta de evidencia y permisos de rol deben verificarse en un dispositivo real.
3. **Protocolos operativos no implementados.** Se mencionan en el PRD, pero no se hallaron modelos, endpoints o pantallas dedicados.
4. **Alertas/notificaciones no implementadas.** No se encontró módulo de notificaciones o entrega de alertas. La app requiere actualización/consulta manual para ver cambios.
5. **Recuperación de contraseña no definida ni implementada.** El cambio de contraseña con sesión sí aparece en cliente/API; el restablecimiento de administradores por superadministrador no equivale a recuperación de autoservicio.
6. **Despliegue productivo no documentado ni evidenciado.** La documentación describe entorno local con XAMPP y Expo Go. Antes de producción se necesita definir hosting, HTTPS, secretos, CORS/hosts, copias de seguridad, monitoreo, política de datos e imágenes, y operación/soporte.
7. **Validación real del impacto no disponible.** No hay métricas de línea base, entrevistas, piloto ni resultados cuantitativos documentados. La problemática actual es una hipótesis de producto, no un estudio de campo.

## Inconsistencias documentales corregidas o por vigilar

- El README anterior incluía SQL con `DROP TABLE`; se sustituyó por una guía segura e índice documental. No ejecutar reconstrucciones destructivas sobre una base con datos.
- El README anterior mezclaba roles de esquema legado (`admin`, `student`) con nombres del diseño actual (`organization_admin`, `user`). Las entidades y permisos deben seguir las definiciones actuales de modelos y API.
- El modelo declara `cerrado`, pero el flujo de interfaz/API documentado se detiene en `resuelto`; no se debe prometer cierre operativo.
- El PRD indica que el QR expira en siete días hábiles de Bogotá, excluyendo fines de semana pero no festivos. No se ha documentado un calendario institucional de festivos.
- Existe registro de `IncidentEvent` en el código; el antiguo SQL del README no representaba todas las tablas/modelos actuales.
- Varios Markdown existentes muestran texto con codificación dañada. Conviene guardarlos como UTF-8 y revisar tildes en una pasada editorial posterior.

## Plan recomendado para cerrar brechas

1. Respaldar y perfilar una copia de la base local; documentar versión y esquema real.
2. Revisar las migraciones Django frente a ese esquema y ensayar en una copia desechable; escribir reversión y validaciones de integridad.
3. Aplicar migraciones únicamente con aprobación y ventana de mantenimiento acordada para la base objetivo.
4. Ejecutar CP01–CP07 en entorno de validación y CP08 en teléfono físico; adjuntar versión, fecha, dispositivo, resultado y evidencia sin datos personales.
5. Decidir con el dueño del producto si protocolos, alertas y recuperación de contraseña pertenecen al MVP; definir requisitos antes de implementarlos.
6. Para recuperación, elegir verificación de identidad (por ejemplo correo institucional con enlace de un solo uso) y políticas anti abuso antes de codificar.
7. Definir política de retención de evidencias, copias de seguridad, despliegue HTTPS y gestión de secretos antes de uso institucional real.
8. Realizar entrevistas o piloto para validar la problemática y medir tiempos de registro, asignación y resolución.

## Conclusión

La documentación de presentación, diagramas, problemática, manual y alcance ahora está cubierta. El software contiene una base considerable de los flujos del MVP, pero no hay fundamento para calificar el producto como completamente validado o listo para producción hasta cerrar las migraciones, las pruebas en dispositivo y los requisitos operativos pendientes.
