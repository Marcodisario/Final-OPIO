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
  interpretable, inicialmente para que el equipo pegara el código en el
  notebook y, posteriormente, para integrarlo directamente.
- **Archivos afectados:** `Parte1/part1_primal.ipynb` (celdas de código de los
  puntos 4–7) y este README. Se generaron los dos CSV puente en `outputs/`.
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
- **Prueba realizada:** las celdas de código de Parte I tienen resultados
  guardados en el notebook. La verificación independiente reporta una violación
  máxima de `7.11e-15`, inferior a la tolerancia `1e-7`; los escenarios
  terminaron en estado óptimo y se generaron los puentes con SHA-256.
- **Estado de datos actualizado:** ya están disponibles los CSV requeridos. El
  diccionario actual se llama `Datos/diccionario_de_datos.csv` (no
  `diccionario_datos.csv`). La oferta de `origins.csv` está identificada en el
  diccionario como valor didáctico propuesto.

### 2026-11-11 — Implementación y correcciones de la Parte II

- **Herramienta:** OpenAI Codex, asistente de IA.
- **Objetivo:** completar la carga de datos y puentes, la estimación de Markov,
  el simulador semanal, los controles, el piloto y la comparación Monte Carlo
  emparejada; corregir errores reportados al ejecutar la celda de carga.
- **Prompt:** solicitud de completar los códigos de la Parte II, validar las
  rutas de datos y corregir los errores de carga detectados.
- **Archivos afectados:** `Parte2/part2_markov_montecarlo.ipynb` (celdas de
  código de carga, Markov, simulación, piloto y campaña) y
  `outputs/informe_ejecutivo.html`.
- **Decisión:** cambios incorporados al notebook. Se reemplazaron las rutas
  incorrectas por una búsqueda compatible con ejecución desde `Parte2` o la
  raíz del proyecto. Se actualizaron los hashes esperados de los puentes
  regenerados y se quitó la dependencia de `data_status`, columna que no existe
  en el archivo actual de parámetros de estado.
- **Sugerencia útil para presentar:** generar un mismo entorno aleatorio por
  réplica y evaluar ambas políticas en él permite estimar directamente la
  diferencia resguardo menos nominal con números aleatorios comunes.
- **Sugerencia corregida/adaptada para presentar:** los hashes fijados
  anteriormente no correspondían a los puentes actuales, y la celda intentaba
  leer una columna opcional inexistente. Se actualizaron los hashes luego de
  verificar los archivos y se validan ahora las columnas que el simulador
  realmente utiliza.
- **Prueba realizada:** se comprobó que las rutas llegan a `Datos/` desde la
  raíz y desde `Parte2`, que los CSV puente existen, que sus hashes coinciden
  con los valores fijados y que sus 15 rutas, metadatos, políticas y flujos no
  negativos son consistentes con `routes.csv`. Se corrigió además el
  `KeyError: 'data_status'`. No se volvió a ejecutar la campaña completa de
  1.200 réplicas en esta sesión; el informe usa las salidas Monte Carlo
  disponibles en `outputs/`.
- **Supuestos documentados en el código:** demanda Poisson con media ajustada
  por estado y disponibilidad Bernoulli por ruta, independientes
  condicionalmente al estado. Los multiplicadores de estado son valores
  didácticos propuestos según el diccionario actual.
- **Pendiente de reconciliar:** el contrato H3 dice que el piloto corresponde a
  las primeras 200 de las 1.200 réplicas, mientras que el código separa las
  secuencias de semillas del piloto y la campaña final. Alinear el protocolo y
  regenerar las salidas antes de la entrega final.

## Próximo paso de registro

Para nuevas intervenciones, copie este formato:

### AAAA-MM-DD — Título de la intervención

- **Herramienta:**
- **Objetivo:**
- **Prompt:**
- **Archivos afectados:**
- **Decisión:** aceptar / modificar / rechazar, con breve justificación.
- **Sugerencia útil:**
- **Sugerencia corregida o rechazada:**
- **Prueba realizada y resultado:**
