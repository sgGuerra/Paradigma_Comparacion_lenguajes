# Tasklist para la entrega del Jueves 30 de Octubre: Comparativa Java vs Scala vs Python (automatización de pago de entradas y administración de atracciones)

## 1) Alineación y criterios
- [ ] Leer el PDF de criterios de evaluación y extraer una lista clara de puntos a medir (rendimiento, memoria, escalabilidad, concurrencia, facilidad de desarrollo, ecosistema, seguridad, testing, despliegue, costo, etc.).
- [ ] Asignar pesos a cada criterio y acordar una matriz de decisión.
- [ ] Revisar la presentación base enviada y definir la estructura de las diapositivas que se seguirá.

## 2) Definición del caso de uso y dataset
- [ ] Definir el flujo mínimo a implementar y medir:
  - [ ] Compra de entrada y pago.
  - [ ] Emisión/validación de pulsera o código.
  - [ ] Control de acceso en torniquete.
  - [ ] Gestión de filas y cupos por atracción.
  - [ ] Reembolsos/cambios básicos.
- [ ] Generar datos sintéticos y cargas de prueba:
  - [ ] Número de visitantes concurrentes, atracciones, horarios, picos.
  - [ ] Escenarios: normal, pico y estrés.
- [ ] Establecer reglas de negocio idénticas para los 3 lenguajes para asegurar paridad.

## 3) Entorno y metodología de benchmark
- [ ] Fijar versiones y tooling (sugerido: JDK 21, Scala 3.x, Python 3.12) y documentarlas.
- [ ] Estandarizar el entorno:
  - [ ] Mismo hardware/SO o contenedores Docker con límites de CPU/RAM iguales.
  - [ ] Variables de entorno y configuración comunes (BD en memoria o archivos locales, misma latencia simulada).
- [ ] Definir métricas y cómo medir:
  - [ ] Rendimiento: throughput (transacciones/seg), latencia p50/p95/p99, tiempo de ejecución total y de warm-up.
  - [ ] Uso de recursos: memoria pico y promedio, CPU.
  - [ ] Eficiencia de concurrencia: escalado con N hilos/procesos/actores.
  - [ ] Productividad: tiempo de desarrollo, LOC, complejidad.
  - [ ] Robustez: tasa de errores bajo carga.
- [ ] Elegir herramientas de medición:
  - [ ] Carga: k6/Locust/JMeter.
  - [ ] Perf: JMH para microbench en JVM; timeit/cProfile en Python.
  - [ ] Sistema: pidstat, perf, GC logs; registradores de métricas.
- [ ] Diseñar un protocolo de ejecución:
  - [ ] Runs repetidos (mín. 5) por escenario, descartar outliers, promediar.
  - [ ] Separar cold start vs steady state.

## 4) Implementación equivalente en los 3 lenguajes
- [ ] Diseñar una arquitectura mínima común (por ejemplo, un servicio REST o CLI con las mismas operaciones).
- [ ] Implementar las funciones clave con algoritmos y estructuras de datos equivalentes.
- [ ] Incorporar concurrencia según el “estilo nativo” de cada lenguaje:
  - [ ] Java: ExecutorService/hilos virtuales.
  - [ ] Scala: Futures/Akka (o estándar si se prefiere evitar frameworks pesados).
  - [ ] Python: asyncio y/o multiprocessing.
- [ ] Incorporar tests unitarios y de integración equivalentes en los tres.
- [ ] Añadir logging y métricas mínimos para medir.

## 5) Validación y paridad
- [ ] Ejecutar una suite de pruebas funcionales cruzadas que verifique que los 3 comportamientos son idénticos frente a los mismos casos de entrada/salida.
- [ ] Revisar que no existan optimizaciones sesgadas en un lenguaje que no estén en los otros.
- [ ] Realizar code review cruzado para confirmar paridad y calidad.

## 6) Ejecución de benchmarks y recolección de datos
- [ ] Correr las baterías de carga en las tres implementaciones bajo:
  - [ ] Tráfico normal, pico y estrés.
  - [ ] Concurrencia escalonada (1, 10, 100, 500, 1000 usuarios).
- [ ] Registrar numéricos:
  - [ ] Latencias p50/p95/p99, throughput, CPU, RAM, tiempo de arranque, pausas de GC, errores.
  - [ ] Métricas de productividad: LOC, complejidad, tiempo de desarrollo estimado.
- [ ] Guardar resultados crudos y scripts para reproducibilidad.

## 7) Análisis y conclusión
- [ ] Consolidar resultados en tablas y gráficos.
- [ ] Aplicar la matriz de decisión con pesos para obtener puntuación final por lenguaje.
- [ ] Analizar trade-offs: rendimiento vs productividad, ecosistema (pagos, colas, scheduling), seguridad (PCI DSS), mantenimiento, curva de aprendizaje.
- [ ] Determinar el lenguaje recomendado para la solución del parque y justificar con números y contexto.

## 8) Preparación de la presentación
- [ ] Estructurar las diapositivas (siguiendo la plantilla enviada):
  - [ ] Portada: tema, equipo, fecha.
  - [ ] Problema y requisitos del parque.
  - [ ] Criterios y pesos del PDF.
  - [ ] Metodología y entorno (versiones, hardware, herramientas).
  - [ ] Arquitectura y paridad de implementaciones.
  - [ ] Resultados numéricos por criterio (gráficos y tablas).
  - [ ] Matriz de decisión y ranking final.
  - [ ] Recomendación y plan de adopción.
  - [ ] Riesgos y mitigaciones.
  - [ ] Conclusiones y Q&A.
- [ ] Incluir capturas/resumen de código representativo, sin sobrecargar.
- [ ] Ensayar presentación y tiempos; preparar respuestas a preguntas.

## 9) Entregables
- [ ] Repositorio con:
  - [ ] Código de las 3 implementaciones, tests y scripts de benchmark.
  - [ ] Dockerfiles o instrucciones de despliegue.
  - [ ] Dataset sintético y generadores.
  - [ ] README con pasos de reproducción y especificaciones de entorno.
- [ ] Carpeta de resultados:
  - [ ] CSV/JSON con métricas, gráficos y notas de ejecución.
  - [ ] Bitácora de runs y configuraciones.
- [ ] Presentación final en el formato solicitado.

## 10) Gestión y cronograma
- [ ] Asignar responsables por lenguaje y por benchmarking/presentación.
- [ ] Hitos:
  - [ ] Día 1: criterios + diseño de benchmark + setup.
  - [ ] Día 2-3: implementación y tests.
  - [ ] Día 4: validación de paridad.
  - [ ] Día 5: benchmarks y recolección de datos.
  - [ ] Día 6: análisis + presentación.
  - [ ] Día 7: ensayo + ajustes finales.
- [ ] Plan B: si un lenguaje no llega a paridad a tiempo, limitar alcance pero mantener comparabilidad de métricas clave.

## Notas importantes
- [ ] Todas las comparaciones deben incluir números concretos y reproducibles, con método documentado.
- [ ] Evitar dependencias externas que alteren la comparabilidad; si se usan (p. ej., framework web), usar equivalentes mínimos.
- [ ] Mantener trazabilidad entre criterios del PDF y secciones de la presentación.


----
> [!NOTE]
> Buenas, para los que no alcanzaron a ir a clase el día Jueves, un recorderis de la entrega del próximo Jueves 30 de Octubre:
Realizar comparaciones de los 3 lenguajes (Java, Scala, Python), bajo el funcionamiento de una solución de automatización de pago de entradas y administración de atracciones de un parque de atracciones como el parque del café.
Para ello, realizar una presentación donde:
> - Compare los 3 lenguajes e indicar cuál es el mejor para la solución al problema planteado, además de tener presente los diferentes puntos a evaluar descritos en la pdf. Tener presente que se debe realizar comparaciones numéricas, ejemplo Java ejecuta el ejercicio en 3 segundos, Vs Scala que lo hace en 5. Y así con cada punto que puedan comparar.
> - Tener presente la presentación enviada, con el fin que se tome como base para los diferentes puntos que deben ser evaluados.

> [!TIP]
> ASFD
---