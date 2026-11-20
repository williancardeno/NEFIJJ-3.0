[x] Fase 1: Documentación del PRD, arquitectura, roles y decisiones técnicas.

[x] Fase 2: Creación del backend Django y configuración para el esquema MySQL existente sin migrar ni alterar la base.

[x] Fase 3: Inicialización de Expo Go, configuración LAN por QR y selección de evidencia.

[x] Fase 4: Implementación de autenticación JWT, perfiles, cambio de contraseña, categorías, reportes, imágenes y aislamiento por organización/sede.

[x] Fase 5: Pruebas de backend en SQLite temporal y validación del bundle Android.

[x] Fase 6: Reglas iniciales de aislamiento por membresía/organización activa, transición estricta de estados y supervisión global de solo lectura para superadmin.

[x] Fase 7: Implementar API de invitaciones QR (hash, un solo uso, revocación, expiración) y pantallas móviles de escaneo/vinculación y generación.

[x] Fase 8: Crear y suspender organizaciones con API y panel móvil de superadmin; gestión completa de administradores de organización (activar/desactivar, restablecer contraseña y eliminación segura con limpieza referencial).

[ ] Pendiente de despliegue local: Revisar/aprobar las migraciones `accounts.0002_organization_invitation` e `incidents.0002_categorytechnician_and_more` antes de aplicarlas a MySQL `nefijj_db`. No ejecutar `migrate` hasta completar la revisión del esquema legado.

[ ] Fase 9: Probar el QR, cámara, permisos de roles, evidencias y conexión LAN en un teléfono físico con Expo Go.

[ ] Fase 10: Completar protocolos y alertas operativas; ya están implementadas la gestión móvil de sedes, técnicos, categorías y enrutamiento por sede.

[ ] Pendiente: Definir e implementar un mecanismo verificado de recuperación de contraseña.

[ ] Pendiente: Revisar y aprobar por separado el plan de migración de Django Admin para `nefijj_db`.

## Entregables documentales de la revisión académica

[x] README con descripción del proyecto, estado y directorio de documentación; retirado el SQL destructivo del README.

[x] Problemática, solución propuesta, usuarios objetivo y límites del alcance.

[x] Diagramas de arquitectura, modelo conceptual, ciclo de atención e invitación QR.

[x] Manual de usuario organizado por rol y problemas frecuentes.

[x] Libreto de presentación con demo sugerida, estado real y preguntas previsibles.

[x] Diagnóstico de brechas que diferencia código presente, pruebas registradas y validaciones pendientes.

[ ] Validar en dispositivo físico los flujos del CP08 y registrar resultados reales.

[ ] Revisar y aplicar las migraciones necesarias a MySQL solo después de respaldar, validar compatibilidad y aprobar el plan.
