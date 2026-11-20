# Problemática y solución — NEFIJJ

## Problema que atiende

En una institución con varias sedes, los reportes de daños y fallas pueden llegar por conversaciones, llamadas o mensajes dispersos. Esa dispersión dificulta reunir evidencia, saber quién reportó, asignar el trabajo al equipo correcto y consultar el avance. También puede hacer que personal de una sede consulte información que pertenece a otra.

Este planteamiento es la problemática objetivo del proyecto; no se presenta como resultado de una encuesta o medición institucional, porque esos datos no están documentados en el repositorio.

## Solución propuesta

NEFIJJ centraliza el ciclo básico de una incidencia en una app móvil conectada a una API:

1. Un estudiante o usuario autenticado queda vinculado a una organización y sede mediante una invitación QR de un solo uso.
2. Reporta una incidencia con título, descripción, categoría, prioridad y una foto opcional.
3. La API relaciona el reporte con su cuenta, sede y organización y, cuando hay una ruta configurada, lo asigna al técnico correspondiente.
4. El técnico consulta incidencias de su sede y actualiza las que tiene asignadas siguiendo el flujo permitido.
5. El administrador gestiona categorías, sedes, técnicos e invitaciones de su organización. El superadministrador mantiene organizaciones y consulta incidencias de forma global.

La autorización se valida en el backend con el rol, las membresías activas y el estado de la organización y sede. El móvil no decide por sí solo qué datos puede ver una cuenta.

## Beneficios esperados

- Reunir reportes y evidencia en un mismo flujo.
- Dar visibilidad del estado de atención a las personas con permisos.
- Facilitar la asignación por categoría y sede.
- Separar los datos por organización, sede y rol.
- Mantener evidencia fuera de la base de datos y entregarla con autorización.

Son beneficios esperados del diseño; su impacto debe medirse en un piloto real.

## Usuarios

| Usuario | Necesidad | Uso de NEFIJJ |
|---|---|---|
| Estudiante/usuario (`user`) | Reportar y consultar sus propios casos | Acepta invitación, registra incidencias y consulta su historial |
| Técnico (`technician`) | Atender los casos de su sede que le asignaron | Consulta incidencias y avanza su estado |
| Administrador de organización (`organization_admin`) | Organizar la atención en su institución | Gestiona sedes, personal, categorías, asignaciones e invitaciones |
| Superadministrador (`superadmin`) | Administrar la plataforma | Crea/suspende organizaciones y supervisa incidencias globales en modo lectura |

## Límites del alcance

El producto no reemplaza canales institucionales de emergencia, un sistema de mantenimiento especializado ni un sistema de notificaciones. La recuperación de contraseña, las alertas y los protocolos operativos están pendientes. La operación física conectada a MySQL requiere validar y aplicar de forma controlada las migraciones necesarias.
