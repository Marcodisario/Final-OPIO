# Trabajo Integrador de Optimización e Investigación Operativa

## Propósito

El trabajo se divide en dos partes. En la Parte I se formula y resuelve un
modelo lineal para planificar envíos desde los centros de origen a los destinos,
considerando oferta, capacidad de las rutas y faltantes. En la Parte II se
evalúan los planes resultantes mediante una cadena de Markov y simulación Monte
Carlo, sin reoptimizar una vez observado cada futuro simulado.

## Uso de agentes de IA

El agente se utiliza después del modelado humano para crear un esqueleto,
traducir estructuras a Python, proponer pruebas, revisar legibilidad o detectar
casos de borde. El equipo debe poder explicar el modelo y revisar cada
sugerencia antes de incorporarla.

Toda intervención se registra con fecha, herramienta, objetivo, prompt,
archivos afectados, decisión de aceptar, modificar o rechazar, y prueba
realizada. En cada puesta en común se mostrará una sugerencia útil del agente y
otra que el equipo haya corregido o rechazado. No se evalúa la cantidad de
consultas, sino la calidad de la revisión y la capacidad de explicar el
resultado.

## Registro de intervenciones

### 2026-11-09 — Implementación propuesta para la Parte I

- **Herramienta:** OpenAI Codex, asistente de IA.
- **Objetivo:** preparar código claro para los puntos 4 a 7 de la Parte I,
  usando OR-Tools para el modelo lineal, agregando una verificación
  independiente, resolviendo el caso nominal y los escenarios, y exportando los
  planes puente con sus hashes SHA-256.
- **Prompt:** solicitud de implementar esos puntos en forma simple, concisa e
  interpretable, sin editar el notebook y dejando el código preparado para
  ejecutarlo cuando estén disponibles los datos faltantes.
- **Archivos afectados:** este README. No se editaron los notebooks ni se
  generaron archivos de salida; el código se compartió en la conversación para
  que el equipo lo revise y lo pegue.
- **Decisión:** pendiente de revisión del equipo. El uso de OR-Tools responde a
  la elección solicitada por el equipo, aunque el notebook original menciona
  `scipy.optimize.linprog`. La firma de las funciones se amplió para recibir
  rutas y penalizaciones como argumentos, porque se necesitan para construir
  el modelo y recalcular el objetivo sin depender de variables globales.
- **Sugerencia útil para presentar:** pasar explícitamente los datos que usa
  cada función ayuda a que el modelo sea reproducible y evita que dependa de
  valores globales modificables.
- **Sugerencia corregida/adaptada para presentar:** el contrato inicial de
  `solve_transport` del notebook no incluía rutas ni penalizaciones entre sus
  argumentos. Se adaptó la firma para incluirlos. El equipo debe confirmar que
  esta decisión coincide con su Ficha de Modelo Acordado y actualizar el
  registro si la modifica.
- **Prueba realizada:** no se ejecutó el código. Faltan `origins.csv` y
  `diccionario_datos.csv`; además, todavía hay que revisar que los nombres de
  columnas de esos archivos coincidan con los usados al preparar los
  argumentos. La validación computacional queda pendiente.

## Próximo paso de registro

Cuando el equipo revise y ejecute el código, actualice la intervención anterior
con su decisión final y el resultado de la prueba. Para nuevas intervenciones,
copie este formato:

### AAAA-MM-DD — Título de la intervención

- **Herramienta:**
- **Objetivo:**
- **Prompt:**
- **Archivos afectados:**
- **Decisión:** aceptar / modificar / rechazar, con breve justificación.
- **Sugerencia útil:**
- **Sugerencia corregida o rechazada:**
- **Prueba realizada y resultado:**
