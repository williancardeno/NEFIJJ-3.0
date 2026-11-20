# Libreto de presentación — NEFIJJ 3.0

**Duración sugerida:** 5–7 minutos.  
**Nota para quien expone:** mostrar una demo únicamente si el backend, la configuración y la base local están disponibles. No presentar una prueba no realizada como resultado verificado.

**Presentación visual:** [Abrir presentación HTML](presentacion_nefijj.html) (navegable con teclado y controles en pantalla).

## 1. Apertura y problemática (45 segundos)

“Buenos días. Presentamos NEFIJJ, una aplicación para la gestión de incidencias en instituciones con varias sedes. El problema que abordamos es la dispersión de reportes de daños y fallas: cuando llegan por distintos canales, cuesta reunir evidencia, identificar responsables y conocer el avance. NEFIJJ propone centralizar ese flujo y mantener separado el acceso según organización, sede y rol.”

## 2. Solución y usuarios (60 segundos)

“La solución conecta una aplicación móvil con una API. El estudiante inicia sesión, se vincula a su sede mediante una invitación QR y registra un reporte con categoría, prioridad, descripción y una foto opcional. El técnico consulta los casos de su sede y avanza los que tiene asignados. El administrador organiza sedes, técnicos, categorías y rutas. El superadministrador administra organizaciones y puede consultar incidencias globales sin intervenir en su operación.”

## 3. Funcionamiento técnico (60 segundos)

“El cliente está construido con React Native y Expo. El backend usa Django REST Framework y autenticación JWT; MySQL es la base prevista para el entorno local. Las reglas de acceso se aplican en la API, no se confía en el identificador de organización enviado por el móvil. Las fotos se guardan como archivos y se entregan mediante una consulta autenticada. La invitación guarda un hash del código, permite revocación y solo puede aceptarse una vez.”

## 4. Recorrido de demostración (2–3 minutos)

1. “Primero iniciamos sesión con una cuenta de usuario ya provisionada.”
2. “Mostramos el ingreso de una invitación QR y la vinculación a una sede.”
3. “Creamos una incidencia, elegimos categoría y prioridad, y adjuntamos una fotografía.”
4. “Entramos con una cuenta técnica y vemos el reporte dentro de su sede. Si está asignado, avanzamos su estado de pendiente a en proceso y después a resuelto.”
5. “Si la configuración está lista, mostramos la administración de categorías y la asignación de un técnico por sede.”
6. “Finalmente, enseñamos el panel del superadministrador para gestionar organizaciones y explicamos que su acceso a incidencias es de lectura.”

Si la conectividad MySQL no está validada o la migración local está pendiente, reemplazar el paso afectado con capturas identificadas como ilustrativas o una explicación del flujo; no simular una confirmación real.

## 5. Estado y límites (45 segundos)

“El repositorio contiene código para autenticación, reportes, evidencia, membresías, invitaciones y administración. Las pruebas funcionales con SQLite temporal aparecen registradas en la documentación del proyecto. La comprobación física integral con Expo Go y la aplicación segura de las migraciones pendientes a la base MySQL existente aún requieren completarse. También están pendientes los módulos de protocolos, alertas y recuperación de contraseñas.”

## 6. Cierre (20 segundos)

“NEFIJJ busca dar trazabilidad al reporte y atención de incidencias en instituciones con varias sedes, manteniendo el acceso limitado al ámbito de cada usuario. El siguiente paso es completar la validación en un dispositivo y con una base compatible, y luego medir el resultado en un piloto institucional. Gracias.”

## Preguntas previsibles

- **¿Qué problema resuelve?** Centraliza los reportes, evidencia, asignación y seguimiento, reduciendo la dependencia de canales dispersos.
- **¿Cómo evita que una sede vea otra?** La API valida membresías, rol y estados de organización/sede y limita los querysets y operaciones.
- **¿El QR inicia sesión?** No. Es una invitación de un solo uso que vincula una cuenta ya autenticada a una sede.
- **¿Está desplegado en producción?** La documentación describe un entorno local de desarrollo. No hay evidencia documental de despliegue productivo.
- **¿Qué falta para declarar el MVP validado?** Revisar/aplicar con control las migraciones MySQL necesarias y completar la prueba física end-to-end, además de resolver los pendientes funcionales identificados.
