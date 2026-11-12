---
name: ecologia-paisaje
description: >-
  Analiza fragmentación, métricas de paisaje y conectividad estructural o
  funcional para estudios ambientales en Colombia (EIA, sustracciones,
  compensaciones), con decisiones de hábitat, barreras, resistencias y escala
  que se definen según el paisaje y la especie o el proceso evaluado. Úsela al
  calcular métricas con FRAGSTATS o landscapemetrics, al modelar conectividad
  (IIC, PC, dPC, ECA, costo mínimo, circuitos) o al comparar escenarios con y
  sin intervención.
license: MIT
---

# Ecología del paisaje

## Principio: el paisaje y la especie deciden
No hay una regla universal sobre qué es hábitat, qué es barrera o qué escala usar. Esas decisiones dependen del paisaje en cuestión y del organismo o proceso que se evalúa, y son las que más cambian los resultados. Antes de calcular, defina y documente con el profesional responsable:

| Decisión | Preguntas que la definen | Ejemplos de cómo puede variar |
|---|---|---|
| **Objeto del análisis** | ¿Conectividad para qué especie, grupo funcional o proceso? | Un primate arborícola, un ave de borde, un anfibio y un pez dan redes distintas sobre el mismo mapa |
| **Hábitat** | ¿Qué coberturas usa la especie para vivir o moverse? | Para especies de bosque, pastos no son hábitat por el efecto de borde y por ser otro ecosistema; para especies de áreas abiertas o de borde pueden serlo |
| **Ríos y cuerpos de agua** | ¿Su ancho, caudal, dinámica y dosel impiden el paso? | Un río ancho, dinámico y con sedimentos puede ser barrera para fauna terrestre; un caño angosto bajo dosel cerrado puede no serlo para una especie arborícola; un bosque de galería puede ser el corredor principal; para fauna acuática el río es el hábitat |
| **Matriz y resistencias** | ¿Cuánto cuesta cruzar cada cobertura? | Minería, vías y zonas urbanas pueden ser resistencia alta o barrera según la especie |
| **Distancias** | ¿Cuál es la distancia de dispersión o el ámbito de hogar? | Si no hay datos publicados para la especie, use un rango de umbrales y declárelo |
| **Escala** | ¿Qué resolución y extensión corresponden a la pregunta? | La extensión debe superar la distancia máxima de dispersión evaluada para no sesgar por el borde del mapa |

Registre cada decisión con su justificación (literatura, datos del sitio, criterio experto) y haga análisis de sensibilidad sobre las más inciertas. Si el equipo no tiene la información, presente escenarios en lugar de fijar un valor.

## Fragmentación
- Métricas de parche, clase y paisaje (McGarigal et al., 2012): por ejemplo CA, PLAND, NP, LPI, ED, ENN, GYRATE, FRAC, área núcleo y SHDI. Elija las que responden la pregunta o las que exige el término de referencia; no reporte decenas de métricas sin interpretarlas.
- Calcule sobre la misma leyenda, resolución y extensión en todas las fechas o escenarios que compare.
- Las métricas de adyacencia (AI, COHESION, CONTAG) cambian con el tamaño de celda: no las compare entre resoluciones distintas.
- Si una herramienta no trae una métrica (por ejemplo PROX en `landscapemetrics`), calcúlela con la definición de FRAGSTATS y dígalo.
- Identifique los agentes de cambio con una matriz de transición entre fechas.

## Conectividad
- **Estructural:** IIC, PC, ECA y la importancia de cada parche (dPC y sus fracciones intra, flujo y conector), con Conefor, Makurhini o una implementación propia validada.
- **Funcional:** superficies de resistencia, rutas de costo mínimo o teoría de circuitos (Circuitscape, Omniscape) cuando la pregunta es por dónde se mueve la especie.
- Compare escenarios: actual, con intervención y, si aplica, después de la restauración. La conectividad con intervención no puede ser mayor que la actual: si lo es, revise los insumos.
- Compruebe que dPCintra + dPCflux + dPCconnector sumen el dPC.

## Cuando dos mapas dan resultados muy distintos
Antes de explicar la diferencia, ubique **dónde** ocurre en el terreno. Una explicación que parece obvia puede ser falsa: por ejemplo, un nodo de hábitat que pisa una barrera en la rasterización abre pasos que no existen. La barrera debe mandar sobre el nodo cuando se rasteriza.

## Insumos y su extensión
Las coberturas deben cubrir, en todas las fechas y a la misma escala, la unión del área de intervención con un buffer mayor que la distancia máxima de dispersión, el área protegida o reserva relevante y el área de influencia biótica. Si la intervención queda cerca del borde de las coberturas, adviértalo.

## Eficiencia
- Rasterice a la resolución que exige la pregunta, no a la más fina disponible: el tiempo de cálculo crece con el cuadrado de la resolución.
- Calcule distancias de costo una vez por escenario y guárdelas; reutilícelas para todos los umbrales.
- Pruebe la configuración en una ventana pequeña antes de correr el paisaje completo.
- Exporte los archivos de nodos y enlaces para repetir el cálculo en Conefor sin rehacer la preparación.

Para fórmulas, herramientas y errores resueltos, lea `references/metricas-y-conectividad.md` solo si la tarea lo requiere.
