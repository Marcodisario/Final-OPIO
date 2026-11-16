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
- **Prueba realizada:** las celdas de código de Parte I tienen resultados  
guardados en el notebook. La verificación independiente reporta una violación  
máxima de `7.11e-15`, inferior a la tolerancia `1e-7`; los escenarios  
terminaron en estado óptimo y se generaron los puentes con SHA-256.

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
- **Prueba realizada:** se comprobó que las rutas llegan a `Datos/` desde la  
raíz y desde `Parte2`, que los CSV puente existen, que sus hashes coinciden  
con los valores fijados y que sus 15 rutas, metadatos, políticas y flujos no  
negativos son consistentes con `routes.csv`. Se corrigió además el  
`KeyError: 'data_status'`. No se volvió a ejecutar la campaña completa de  
1.200 réplicas en esta sesión; el informe usa las salidas Monte Carlo  
disponibles en `outputs/`.
