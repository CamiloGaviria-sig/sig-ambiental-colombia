---
name: modelo-datos-anla
description: >-
  Llena y valida la geodatabase del modelo de almacenamiento geográfico de la
  ANLA para estudios ambientales en Colombia, en especial las capas y tablas
  del medio biótico (aprovechamiento forestal, puntos y resultados de muestreo
  de flora, coberturas, ecosistemas). Úsela al preparar entregas de GDB o
  shapefiles con ese esquema, al revisar dominios y unidades, o al comprobar
  que la GDB sea coherente con el inventario y los documentos.
license: MIT
---

# Modelo de almacenamiento geográfico de la ANLA

## Antes de llenar
1. Consiga la plantilla de GDB y el **diccionario de datos** de la versión vigente del modelo (ANLA; *verificar vigencia de la resolución que lo adopta y de su última actualización*). El diccionario manda sobre cualquier ejemplo, incluido este.
2. Lea del diccionario solo las capas que va a llenar: nombre exacto, campos obligatorios, tipo, longitud, unidades y dominios.
3. Defina con el equipo qué capas aplican al proyecto. Una capa que no aplica se entrega vacía **con su esquema**, o según indique la autoridad.

## Capas bióticas frecuentes
| Capa o tabla | Qué contiene | Errores típicos |
|---|---|---|
| `AprovechaForestalPT` | Un punto por individuo a aprovechar, con especie, DAP, altura y volumen | Incluir individuos en veda o fuera del área de intervención; volúmenes que no suman lo del formato de solicitud |
| `AprovechaForestalPG` | Polígonos del área de aprovechamiento, con cobertura, ecosistema, individuos y volumen | Polígono que no coincide con el área de intervención vigente; `INDIVIDUOS` y volumen en unidades distintas a las del diccionario (por ejemplo, por hectárea) |
| `PuntoMuestreoFlora` | Parcelas o puntos de muestreo | Coordenadas que no coinciden con el inventario |
| `MuestreoFloraFustalTB`, `MuestreoFloraRegeneracionTB` | Registros individuales del inventario | Categorías de regeneración incoherentes con altura y DAP |
| `MuestreoFloraResultadosTB` | Resultados por cobertura y especie | Dominio de categoría de amenaza mal asignado; nombres de cobertura distintos a los de la capa de coberturas |

## Dominios y categorías
- Asigne los códigos de dominio desde el diccionario, nunca de memoria. Ejemplo verificado en una versión del diccionario: en `CATE_MINIS`, 324 correspondía a En Peligro (EN) y 330 a no amenazada. Confírmelo en la versión que use.
- Contraste cada especie con el listado nacional vigente (ver la skill `especies-amenazadas-vedas`). Un error frecuente es dejar como «no amenazada» una especie que el listado vigente incluye.
- Los nombres de cobertura en las tablas deben ser idénticos a los de la capa de coberturas (código y nombre).

## Coherencia entre productos
Antes de entregar, compruebe con un solo script que cuadren:
- Número de individuos y volumen de `AprovechaForestalPT` = lo declarado en el formato de solicitud de aprovechamiento y en el capítulo de demanda de recursos.
- Todos los puntos de `AprovechaForestalPT` caen dentro de `AprovechaForestalPG`, y este dentro del área de intervención vigente.
- `AprovechaForestalPG` usa la misma cobertura que la capa de coberturas vigente en ese polígono.
- `MuestreoFloraResultadosTB` suma el mismo número de individuos y especies que el inventario de campo.
- Si el área de intervención cambió y ya no hay aprovechamiento, las capas de aprovechamiento se entregan vacías con su esquema y el texto lo explica.

## Edición segura
- Trabaje sobre copias y escriba los resultados en una carpeta propia; las capas del equipo pueden estar en uso o desactualizadas.
- Si debe corregir un campo en un `.dbf`, hágalo con una herramienta que respete el esquema, y verifique después leyendo el archivo de nuevo.
- Las entregas parciales (por título o por profesional SIG) se empaquetan con un `LEEME.txt` que diga qué cambió y en qué sistema de coordenadas está.

## Eficiencia
- Lea el diccionario de datos por hoja y filtrado por capa; no lo cargue completo.
- Valide con un script que imprima solo las discrepancias, no todos los registros.
- Para GDB de archivo grandes, liste primero las capas y su número de entidades, y abra solo las necesarias.
