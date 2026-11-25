# Auditoría pedagógica sistemática — TeachYourself

Fecha: 25-11-2026

## Alcance ejecutado

- 113 clases registradas.
- 1281 generadores de ejercicios, distribuidos en 113 clases.
- 10 instanciaciones por generador: 12810 muestras dinámicas, sin errores de generación.
- Se revisaron automáticamente estructura, consigna, tipo de ejercicio, solución, presencia de reenseñanza y estructura por etapas.
- Se extrajeron las 113 clases completas: 926 pasos de enseñanza, con texto de introducción, regla, explicación y bloques visuales/estructurados.
- Esto es un barrido estructural y dinámico; NO equivale a validación semántica humana de cada consigna/solución ni a prueba con estudiantes.

## Hallazgos medibles

- Generadores con reenseñanza alternativa propia: 17/1281 (1.3%).
- Generadores con formato por etapas: 134/1281 (10.5%).
- Muestras que son opción múltiple: 5100 (39.8%).
- Muestras numéricas: 5110 (39.9%).
- Muestras por etapas: 1340 (10.5%).
- Muestras abiertas/autoevaluadas: 550 (4.3%).
- Muestras con consigna de 8 palabras o menos (requieren revisión contextual): 2761 (21.6%).

## Cobertura por semana

| Semana | Generadores | Con reenseñanza | Por etapas |
|---:|---:|---:|---:|
| 1 | 70 | 2 | 2 |
| 2 | 82 | 15 | 9 |
| 3 | 43 | 0 | 0 |
| 4 | 38 | 0 | 0 |
| 5 | 43 | 0 | 1 |
| 6 | 18 | 0 | 0 |
| 7 | 30 | 0 | 2 |
| 8 | 37 | 0 | 0 |
| 9 | 28 | 0 | 0 |
| 10 | 28 | 0 | 1 |
| 11 | 35 | 0 | 0 |
| 12 | 35 | 0 | 0 |
| 13 | 45 | 0 | 3 |
| 14 | 64 | 0 | 5 |
| 15 | 129 | 0 | 16 |
| 16 | 60 | 0 | 5 |
| 17 | 65 | 0 | 6 |
| 18 | 77 | 0 | 9 |
| 19 | 60 | 0 | 5 |
| 20 | 93 | 0 | 15 |
| 21 | 111 | 0 | 23 |
| 22 | 90 | 0 | 32 |

## Auditoría estructural de las clases

- Las 113 clases tienen los campos introductorios, regla y explicación presentes en sus 926 pasos; esto comprueba integridad de estructura, no comprensión real.
- 197 de 926 pasos (21,3%) superan 180 palabras en esos tres campos. La concentración está en las semanas 15–22; varias clases de Análisis, Álgebra, Física e IPC promedian más de 200 palabras por paso. Es una señal de posible sobrecarga y de que conviene dividir desarrollos largos en unidades de pensamiento más pequeñas, no una prueba automática de que cada paso esté mal.
- Las semanas 1–6 promedian aproximadamente 76–80 palabras por paso. Las semanas 15–22 promedian aproximadamente 169–213 palabras por paso según la semana.
- Solo 49 pasos incluyen un objeto `check` explícito dentro del contenido de la clase. No significa que las demás clases carezcan de ejercicios: sus bancos están fuera de ese objeto; sí indica que hay pocas comprobaciones incrustadas en el desarrollo de la explicación.
- El contenido íntegro de los 926 pasos quedó exportado para revisión por unidad en `auditoria_clases_113.json` y `auditoria_contenido_clases_113.csv`.

## Pruebas técnicas existentes ejecutadas

- Fase A: 14/14 aprobadas.
- Motor de ejercicios: 83/83 aprobadas.
- Grafo de habilidades: 95/95 aprobadas.
- Total: 192/192 aprobadas. Estas pruebas verifican persistencia, estructura, generadores, cálculos derivados, atribución de habilidades y criterios de dominio; no certifican claridad pedagógica ni transferencia de aprendizaje.

## Problemas de arquitectura detectados en el código

1. La retroalimentación normal tras error suele mostrar la solución paso a paso y un mensaje genérico; no exige comprobar que el alumno entendió ni propone una transferencia equivalente.
2. La reenseñanza alternativa depende de que el generador tenga `reteach`; el muestreo detecta que esa cobertura es excepcional y está concentrada en las primeras semanas.
3. En ejercicios `steps`, un error de etapa llama `attachReteachAfter(..., ex)`: la reenseñanza se toma del ejercicio completo, no de la etapa `st`. Las etapas tampoco tienen un contrato obligatorio de explicación alternativa.
4. La batería `lexExerciseSane` valida forma y consistencia básica, y las pruebas del motor verifican ciertos resultados derivados; el propio comentario del código declara que no valida el significado de todos los enunciados ni de todas las soluciones.
5. Los porcentajes de tipos describen el formato, no el valor pedagógico. La alta proporción de opción múltiple/numérico no es automáticamente un defecto, pero requiere equilibrio con explicación, producción de razonamiento y transferencia.

## Prioridades de corrección global

1. Contrato pedagógico obligatorio para cada generador: objetivo, prerequisitos, interpretación en lenguaje llano, procedimiento razonado, error probable, explicación alternativa y ejercicio de transferencia.
2. Motor de retroalimentación en capas: diagnosticar el error; cambiar la representación/explicación; guiar un paso; volver a comprobar; después transferir a un caso nuevo.
3. Contrato específico por etapa: explicación y pistas ligadas a la etapa, no solo al ejercicio padre.
4. Pruebas automáticas semánticas para operaciones derivables, y revisión humana por muestreo estratificado de cada unidad/tema, no solo de Semana 1–2.
5. Evaluación final del aprendizaje: ítems nuevos y transferencia diferida, no reutilizar únicamente los mismos patrones generados.

## Archivos de evidencia

- `auditoria_pedagogica_muestras.json`: 12.810 instancias muestreadas.
- `auditoria_clases_113.json` y `auditoria_contenido_clases_113.csv`: extracción de los 926 pasos de las 113 clases.
- `auditoria_pedagogica_sistematica.csv`: inventario por generador con muestra de consigna y alertas.
- Este informe resume cobertura estructural; no certifica que las 113 clases estén pedagógicamente correctas.
