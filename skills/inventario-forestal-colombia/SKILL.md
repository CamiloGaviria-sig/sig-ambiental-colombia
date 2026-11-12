---
name: inventario-forestal-colombia
description: >-
  Procesa y revisa inventarios forestales y de regeneración natural para
  estudios ambientales y permisos de aprovechamiento forestal en Colombia:
  nomenclatura, suficiencia de muestreo, estructura, diversidad, volúmenes,
  individuos a aprovechar y su coherencia con la cartografía y el formato de
  solicitud. Úsela al trabajar con Excel de inventario, al calcular volúmenes o al
  redactar la caracterización de flora o la demanda de aprovechamiento.
license: MIT
---

# Inventario forestal y aprovechamiento

## Primero, entender la tabla
- Identifique la unidad de registro: **individuo, fuste o punto GPS**. Un individuo con varios fustes tiene varias filas; un punto GPS puede no tener número correlativo con el individuo. Cuente individuos por su identificador de muestreo, no por filas ni por puntos GPS, y reporte ambos cuando difieran.
- Revise unidades: DAP en cm o en m, altura en m, área basal en m², volumen en m³.
- Imprima un resumen corto (filas, individuos, especies, rango de DAP y altura, vacíos) antes de calcular.

## Nomenclatura
Valide cada nombre científico contra una fuente taxonómica (Catálogo de Plantas y Líquenes de Colombia, World Flora Online o POWO) antes de cualquier análisis. Errores frecuentes de digitación: *Phitecelobium* por *Pithecellobium*, *Espondias* por *Spondias*, *espectabilis* por *spectabilis*, *micranthum* por *micrantha* (en *Trema*), *rombifolia* por *rhombifolia* (en *Sida*). Unifique sinónimos y documente cada cambio en una tabla de correcciones.

## Suficiencia y error de muestreo
- Curva de acumulación de especies por parcela; declare si se estabiliza.
- Para inventarios estadísticos, reporte el error de muestreo con su probabilidad. El Decreto 1076 de 2015 exige un error de muestreo no superior al 15 % con una probabilidad del 95 % en los aprovechamientos forestales persistentes (art. 2.2.1.1.4.5) y únicos (art. 2.2.1.1.5.7). El art. 2.2.1.1.4.5 también exige, según la superficie, un inventario al 100 % de las especies a aprovechar; confirme en el texto vigente (Función Pública o SUIN-Juriscol) el umbral de superficie y el momento de presentación antes de citarlo.
- Los aprovechamientos de árboles aislados no requieren plan de aprovechamiento (parágrafo del art. 2.2.1.1.7.4) ni un error de muestreo normativo. En la práctica se censan todos los individuos a aprovechar; confirme con la autoridad ambiental de la jurisdicción qué información exige.

## Análisis de la vegetación
- **Estructura horizontal:** abundancia, frecuencia y dominancia absolutas y relativas, e índice de valor de importancia (IVI).
- **Estructura vertical:** estratos y posición sociológica; perfiles fisonómicos cuando aporten.
- **Clases diamétricas y altimétricas** con intervalos declarados.
- **Diversidad:** riqueza, Shannon, Simpson y Margalef por cobertura, con la advertencia de que el tamaño de muestra condiciona la comparación.
- Interprete por cobertura; no mezcle pastos arbolados con vegetación secundaria en un mismo promedio.

## Regeneración natural
Use las categorías del protocolo del proyecto y verifique que cada registro las cumpla. Un esquema común es: brinzal o categoría I (altura menor a 0,30 m), categoría II (0,30 a 1,5 m) y latizal o categoría III (más de 1,5 m y DAP menor a 10 cm). Un registro de categoría III con DAP de 10 cm o más es fustal, no regeneración. Informe cuántos registros no cumplen y no los corrija sin consultar.

## Volúmenes
- Fórmula y parámetros declarados: por ejemplo, V = (π/4) · DAP² · H · ff, con el factor de forma (ff) y su fuente. No cambie de fórmula entre tablas.
- Diferencie volumen total y comercial si la autoridad lo pide.
- Sume por especie y verifique que el total coincida en el inventario, la capa de puntos de aprovechamiento y el formato de solicitud.

## Aprovechamiento forestal
- Defina primero el tipo: árboles aislados fuera de cobertura de bosque natural, aprovechamiento único, persistente o doméstico (Decreto 1076 de 2015, Libro 2, Parte 2, Título 2, Capítulo 1). El Decreto 1532 de 2019 modificó ese capítulo en lo relativo a plantaciones forestales. La regulación de árboles aislados ha tenido ajustes y se aplica con criterios de cada autoridad: al usar esta skill, confirme el texto vigente y los requisitos de la autoridad competente. La cobertura real del sitio decide el tipo: árboles dispersos en potrero son árboles aislados aunque una capa de coberturas diga bosque fragmentado. En ese caso, corrija la capa, no el permiso.
- Solo se aprovechan individuos dentro del área de intervención vigente y con DAP igual o mayor al límite del protocolo (habitualmente 10 cm).
- Las especies amenazadas o en veda se excluyen o se tramitan aparte (ver `especies-amenazadas-vedas`). Informe a qué distancia del área quedan.
- Si el área de intervención se redujo y ya no hay individuos a aprovechar, dígalo de forma explícita y revise si el permiso ya se radicó (puede requerirse un desistimiento).
- Revise el formato de solicitud campo por campo: titular, predio (nombre del certificado de tradición, no el código del proyecto), matrícula y cédula catastral, área, especies y volúmenes, costo del proyecto y firma. Cifras copiadas de otro proyecto son un error frecuente.

## Eficiencia
- Calcule todo con un solo script por inventario y guarde las tablas de salida; no recalcule para cada pregunta.
- Lea los Excel por hoja y rango; si traen encabezados de varias filas, detecte la fila del encabezado en lugar de leer todo.
