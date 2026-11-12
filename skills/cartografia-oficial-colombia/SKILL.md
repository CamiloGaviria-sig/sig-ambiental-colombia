---
name: cartografia-oficial-colombia
description: >-
  Prepara y verifica cartografía oficial para estudios ambientales en Colombia:
  entregables en MAGNA-SIRGAS Origen Nacional (EPSG:9377), cálculo de áreas,
  cuadros de coordenadas de vértices, cruces entre capas y control de calidad
  geométrico. Úsela al generar o revisar shapefiles, GeoPackage o Excel de
  coordenadas para una autoridad ambiental, o al reportar hectáreas en un
  documento.
license: MIT
---

# Cartografía oficial en Colombia

## Reglas que no se negocian
1. **Origen Nacional.** Los entregables oficiales van en MAGNA-SIRGAS / Origen-Nacional, **EPSG:9377**.
   - La Resolución 370 de 2021 del IGAC lo estableció como sistema de proyección cartográfica oficial, y es la que cita la metodología de estudios ambientales de 2026.
   - La Resolución 471 de 2020 del IGAC, modificada por las Resoluciones 529 de 2020 y 197 de 2022, fija las especificaciones de la cartografía básica y los parámetros: Transversa de Mercator sobre GRS80, origen en 4° N y 73° W, falso este 5.000.000 m, falso norte 2.000.000 m y factor de escala 0,9992.
   - El datum es MAGNA-SIRGAS (Resolución 68 de 2005 del IGAC). La información en datum Bogotá se transforma con los parámetros que publica el IGAC.
   - Escriba «EPSG:9377» u «Origen Nacional». Algunos términos de referencia todavía dicen «CTM-12»: es el mismo sistema con un nombre informal, y en los entregables conviene usar el nombre oficial.
   - Al usar esta skill, confirme en el normograma del IGAC que no haya modificaciones posteriores.
2. **Áreas siempre en coordenadas proyectadas.** Las hectáreas oficiales se calculan en EPSG:9377. Si una capa llega en EPSG:4686 o 4326, reproyecte antes de medir; nunca calcule áreas en grados ni en Web Mercator.
3. **La geometría manda sobre el atributo.** Los campos `Shape_Area`, `AREA_HA` o similares pueden estar desactualizados después de una edición. Recalcule desde la geometría y avise si difieren.
4. **Sistema de coordenadas declarado al primer contacto.** Al abrir cada capa, informe su EPSG. Si no tiene `.prj` o es ambiguo, deténgase y resuélvalo con un punto de control conocido; no lo adivine.
5. **Coordenadas Z y M.** Elimínelas antes de unir o disolver (`st_zm()` en R).

## Cálculo y reporte de áreas
- Reporte con cuatro decimales en hectáreas (0,0001 ha = 1 m²) y coma decimal en documentos en español.
- Cuando un área se compone de partes (por método, cobertura o vereda), verifique que la suma de las partes cuadre con el total; si no, encuentre la diferencia antes de entregar (huecos, traslapes, astillas).
- Los porcentajes se calculan sobre el área de referencia declarada (el título, el área solicitada, el área de influencia).
- Si un texto cita un área que no coincide con la capa vigente, identifique la causa probable: dígitos invertidos, capa vieja o atributo sin recalcular.

## Cuadro de coordenadas de vértices
- Extraiga los vértices de cada polígono en orden, sin repetir el de cierre, con ID de polígono, número de vértice, Este y Norte en EPSG:9377.
- Si la autoridad lo pide, agregue latitud y longitud en EPSG:4686 (MAGNA-SIRGAS geográficas), en grados decimales o en grados, minutos y segundos.
- Hoja de áreas por polígono y hoja de coordenadas en el mismo Excel; metadatos del archivo con el nombre de la empresa responsable, no con el de una herramienta.

## Control de calidad antes de entregar
Corra un solo script que imprima un resumen corto (no la tabla completa):
- EPSG de cada capa y número de entidades.
- Geometrías inválidas, vacías o con anillos que se tocan a sí mismos (repare con `st_make_valid` o `RepairGeometry` en modo OGC, nunca con buffer 0).
- Traslapes y huecos entre polígonos que deberían ser contiguos, con su área total y el número de astillas.
- Diferencia entre el área de la geometría y el atributo de área.
- Registros que entran y salen de cada cruce: un cruce que duplica o pierde filas es el error más frecuente.

## Requisitos de la metodología de estudios ambientales (Resolución 0940 de 2026)
- **Escala de trabajo** es la que fijan los términos de referencia; la escala de presentación puede ajustarse para leer mejor el mapa. Muchos términos de referencia de minería piden 1:5.000 «o la más pertinente».
- **Unidad mínima cartografiable** de 4 × 4 mm llevada a la escala: 400 m² a 1:5.000; 1.600 m² a 1:10.000; 1 ha a 1:25.000; 16 ha a 1:100.000.
- **Imágenes:** resolución espacial mínima de 0,8 m para 1:5.000; 2,5 m para 1:10.000; 5 m para 1:25.000 y 15 m para 1:100.000, con una antigüedad máxima de tres años (o justificar por qué no hay insumos más recientes).
- **Consistencia geométrica:** los cuerpos de agua de la hidrografía base deben coincidir con los de la capa de coberturas; sin vacíos ni superposiciones; objetos, atributos y dominios según el modelo de almacenamiento geográfico vigente.
- **Entrega:** carpetas de archivos geográficos con léame, insumos, metadatos en la plantilla de la ANLA, mapas en PDF y plantillas de mapa o simbología. Detalle y elementos mínimos de cada mapa en `references/entrega-mgepea.md`.

## Formatos de entrega
- **Shapefile** cuando la autoridad lo exige: nombres de campo de máximo 10 caracteres, codificación UTF-8 declarada en el `.cpg`, una geometría por capa. Las capas vacías deben conservar el esquema y el tipo de geometría.
- **GeoPackage** para trabajo interno y como respaldo del shapefile.
- Comprima cada entrega en un ZIP con un `LEEME.txt` breve: sistema de coordenadas, fecha, contenido y fuente de cada capa.

## Versiones de capas
En un proyecto suele haber varias versiones de la misma capa. Antes de usar una, confirme cuál es la vigente (fecha, nombre, quién la editó) y anótelo. Nunca sobrescriba una capa de trabajo del equipo: escriba resultados en una carpeta propia.

## Eficiencia
- Lea con filtro espacial o de atributos (`st_read(query=, wkt_filter=)`) en vez de cargar capas regionales completas.
- Reproyecte una sola vez y guarde el intermedio en GeoPackage.
- Imprima conteos y sumas, no tablas completas; abra un mapa solo para confirmar un hallazgo.

Para el detalle de comprobaciones y fragmentos de código, lea `references/verificaciones.md` solo si la tarea lo requiere.
