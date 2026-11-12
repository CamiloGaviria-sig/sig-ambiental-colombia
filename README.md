# SIG ambiental Colombia

Conjunto de skills para el trabajo SIG y del medio biótico en estudios ambientales de Colombia: estudios de impacto ambiental (EIA), planes de manejo, permisos de aprovechamiento forestal, sustracciones de reservas y respuestas a requerimientos de autoridades.

Nació de la práctica en proyectos de minería aluvial en el Bajo Cauca antioqueño. Recoge lo que suele aprenderse a fuerza de errores: dónde se rompen las entregas de la ANLA, por qué una cobertura no se valida con los mismos puntos que la construyeron y cómo evitar que un inventario contradiga a su propia capa de aprovechamiento.

> **Versión 0.2.0.** Las normas de cartografía, modelo de datos, inventario forestal, vedas y metodología de estudios ambientales se contrastaron con fuentes oficiales en noviembre de 2026, incluidas la Metodología General para la Elaboración y Presentación de Estudios Ambientales (Resolución 0940 de 2026) y los términos de referencia de pequeña minería (TdR-032, 2026). Como cambian con el tiempo, cada skill indica qué debe confirmar el profesional al usarla.

## Skills

| Skill | Úsela para |
|---|---|
| `cartografia-oficial-colombia` | Entregables en MAGNA-SIRGAS Origen Nacional (EPSG:9377), cálculo de áreas, cuadros de coordenadas, control de calidad geométrico |
| `coberturas-clc-colombia` | Interpretar, editar y validar coberturas con la leyenda Corine Land Cover adaptada para Colombia; Sentinel-2 y ortofotos; cambio entre fechas |
| `modelo-datos-anla` | Llenar y validar la GDB del modelo de almacenamiento geográfico de la ANLA (aprovechamiento forestal, muestreo de flora y demás capas) |
| `inventario-forestal-colombia` | Inventarios, suficiencia de muestreo, estructura, regeneración natural, volúmenes, aprovechamiento forestal y su formato de solicitud |
| `especies-amenazadas-vedas` | Categorías de amenaza nacionales e internacionales, CITES, vedas nacionales y regionales y endemismos, siempre contra el listado y las vedas vigentes |
| `ecologia-paisaje` | Fragmentación, métricas de paisaje y conectividad, con decisiones que dependen del paisaje y de la especie evaluada |
| `tramites-ambientales-colombia` | Sustracciones, respuestas a requerimientos, consulta previa y redacción técnica para autoridades |

## Principios comunes

**Rigor.** El sistema de coordenadas se declara siempre; las áreas se miden en coordenadas proyectadas; cada cruce informa cuántos registros entran y cuántos salen; las unidades van en el nombre de los campos; ningún dato se inventa y los faltantes se declaran.

**Eficiencia.** Las skills están escritas para gastar pocos tokens y poco cómputo:
- Inspeccionar antes de leer: esquema, campos, conteos y sistema de coordenadas, nunca el archivo completo.
- Resolver con scripts que imprimen resúmenes cortos, no con volcados de tablas.
- Recortar temprano al área de interés y guardar los resultados intermedios para no recalcularlos.
- Extraer el texto de documentos pesados a un archivo y buscar por sección.
- Usar imágenes solo cuando aportan, y a la resolución necesaria.
- Pesar el esfuerzo contra el efecto antes de afinar un resultado.
- No volver a verificar lo que ya se verificó y quedó registrado con fecha.

**Contexto.** Las reglas ecológicas no son universales. Qué es hábitat, qué es barrera o cuál es la escala adecuada depende del paisaje y de la especie o el proceso evaluado. Las skills piden que esas decisiones se declaren y se justifiquen en cada proyecto.

## Instalación

En Claude Code:

```
/plugin marketplace add CamiloGaviria-sig/sig-ambiental-colombia
/plugin install sig-ambiental-colombia@sig-ambiental-colombia
```

En claude.ai o la aplicación de escritorio: comprima cada carpeta de `skills/` y súbala en *Customize → Skills → Upload a skill*.

## Requisitos

R (`sf`, `terra`, `readxl`, `openxlsx`) o Python (GeoPandas, Rasterio). ArcGIS Pro o QGIS son opcionales. Ninguna skill requiere servicios de pago.

## Privacidad

Ningún ejemplo contiene datos de proyectos reales, titulares, predios ni personas. Al usar estas skills con información de clientes, esa información no debe salir del equipo ni copiarse en ejemplos públicos.

## Atribuciones

Los principios generales de calidad geoespacial se adaptaron de *GeoAI Skills* (muend/geoai-skills, licencia MIT). Ver `ATRIBUCIONES.md`.

## Licencia

MIT. Ver `LICENSE`.
