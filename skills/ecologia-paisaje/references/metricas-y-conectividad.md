# Métricas y conectividad: herramientas y errores resueltos

## Herramientas
| Tarea | R | Otras |
|---|---|---|
| Métricas de paisaje | `landscapemetrics` (validar contra FRAGSTATS) | FRAGSTATS 4 |
| Conectividad estructural (IIC, PC, ECA, dPC) | `Makurhini`, o `terra` + `igraph` con distancias de borde a borde | Conefor 2.6 |
| Costo mínimo | `gdistance`, `leastcostpath` | Linkage Mapper |
| Circuitos | — | Circuitscape, Omniscape |
| Tendencia regional | — | MapBiomas Colombia (solo como complemento; no se mezcla con coberturas de detalle) |

## Índices (Saura y colaboradores)
- IIC: integral de conectividad (Pascual-Hortal y Saura, 2006).
- PC: probabilidad de conectividad (Saura y Pascual-Hortal, 2007), con probabilidad de dispersión decreciente con la distancia.
- ECA: área conectada equivalente (Saura et al., 2011).
- dPC por parche y sus fracciones intra, flujo y conector (Saura y Rubio, 2010).

## Escenarios típicos
- **Actual:** coberturas vigentes.
- **Con intervención:** el área intervenida pasa a la clase de la actividad (por ejemplo, minería).
- **Restaurado:** según el plan de cierre, para intervenciones temporales.
- **Sensibilidad:** variar umbrales de distancia y el tratamiento de la matriz (resistencia alta frente a barrera).

## Errores resueltos en la práctica
- **Nodos sobre la barrera.** Una rutina que devuelve resistencia 1 a toda celda con centro en hábitat deja pasos abiertos donde un río angosto toca el parche. La barrera debe imponerse al nodo.
- **Agua que parte el bosque.** El parche mayor puede pasar del 28 % al 67 % del área según se traten los ríos y su corredor como barrera o como bosque. Esa decisión se toma antes de calcular y se declara.
- **Pocos nodos grandes.** Cuando el hábitat ocupa casi todo el paisaje, el ECA lo dominan los bloques grandes y los parches chicos casi no influyen; dígalo al interpretar.
- **Resoluciones mezcladas.** Rásteres a 5 y 25 m de una capa de 10 m no aportan y confunden la comparación.
- **Parches equivalentes entre mapas.** Para comparar un mismo parche entre fuentes, empareje por índice de Jaccard y no por identificador.

## Referencias
McGarigal, Cushman y Ene (2012); Pascual-Hortal y Saura (2006); Saura y Pascual-Hortal (2007); Saura y Rubio (2010); Saura, Estreguil, Mouton y Rodríguez-Freire (2011); WWF, PNN e IAvH (2007), evaluación de integridad ecológica.
