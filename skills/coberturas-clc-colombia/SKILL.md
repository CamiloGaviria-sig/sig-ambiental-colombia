---
name: coberturas-clc-colombia
description: >-
  Interpreta, clasifica, edita y valida coberturas de la tierra con la leyenda
  Corine Land Cover adaptada para Colombia, desde Sentinel-2 u ortofotos, y
  compara coberturas entre fechas. Úsela al producir o corregir una capa de
  coberturas, al evaluar su exactitud, al cruzarla con áreas de intervención o
  cuando una cobertura del mapa no coincide con lo observado en campo.
license: MIT
---

# Coberturas Corine Land Cover adaptada para Colombia

## Leyenda y escala
- Use la Leyenda Nacional de Coberturas de la Tierra, metodología Corine Land Cover adaptada para Colombia (IDEAM, 2010, o versiones oficiales posteriores), con códigos jerárquicos (p. ej. 2.3.1 pastos limpios, 2.3.2 pastos arbolados, 2.3.3 pastos enmalezados, 3.1.x bosques, 3.2.3 vegetación secundaria o en transición, 4.1.1 zonas pantanosas, 5.1.1 ríos). Puede detallar niveles inferiores, pero los niveles 1, 2 y 3 no se modifican.
- La escala de trabajo la fijan los términos de referencia (en pequeña minería, 1:5.000 o la más pertinente). La unidad mínima cartografiable (UMC) que fija la metodología de estudios ambientales de 2026 (Resolución 0940) es de 4 × 4 mm a la escala: 400 m² a 1:5.000; 1.600 m² a 1:10.000; 1 ha a 1:25.000; 16 ha a 1:100.000.
- La resolución de la imagen debe corresponder a la escala: como mínimo 0,8 m para 1:5.000; 2,5 m para 1:10.000; 5 m para 1:25.000 y 15 m para 1:100.000, con una antigüedad máxima de tres años salvo justificación. Sentinel-2 (10 m) no alcanza el mínimo para 1:25.000: úselo para análisis de paisaje o multitemporales, declarando y justificando la escala, y no como insumo único de una cobertura de detalle. Una ortofoto de 1 m alcanza para 1:10.000, pero no para 1:5.000.
- Los cuerpos de agua de la capa de coberturas deben coincidir con los de la hidrografía base del estudio.
- Las clases se definen por lo que se ve, no por el nombre que conviene. **Árboles dispersos en potrero son 2.3.2 pastos arbolados, no bosque fragmentado (3.1.3)**; llamar bosque a un parche de pocos árboles sobredimensiona el impacto y contradice el inventario.

## Insumos y su jerarquía
1. Imagen de la fecha de referencia (ortofoto, Sentinel-2 L2A, imagen de alta resolución).
2. Interpretación visual experta, por contexto y no píxel a píxel.
3. Datos de campo.
4. Capas oficiales (IDEAM, POMCA, autoridad ambiental) como contexto, no como verdad del sitio.

**El campo no es verdad absoluta.** Un punto de campo representa un sitio y un momento; a veces es un rótulo por zonas. Acéptelo donde la imagen concuerda; donde no, proponga el cambio polígono por polígono y deje la decisión al profesional responsable. Las capas regionales antiguas (por ejemplo, de humedales) pueden no reflejar el territorio actual: si campo y una imagen reciente coinciden en contradecirlas, documéntelo con evidencia.

## Sentinel-2
- Use el mismo nivel de procesamiento (L2A o TOA armonizado) en todas las fechas que compare.
- La máscara de nubes de la escena (SCL) no detecta la neblina delgada: compárela con el azul de otra fecha cercana.
- Rellene vacíos de nubes solo con otra imagen real de fecha cercana y el mismo nivel, y registre la fecha de origen por píxel. Lo que no se pueda rellenar se declara como faltante, en hectáreas.
- Con 10 m, bosque fragmentado y vegetación secundaria no se separan con confianza: agrúpelos o declare la limitación.
- Los rótulos de oficina derivados de la misma imagen no validan el modelo que los reproduce.

## Ortofoto RGB (sin infrarrojo)
- Normalice el brillo entre hojas antes de clasificar; si no, aparecen bordes rectos.
- Agua turbia y grava de playones no se separan con tres bandas: corríjalos a mano.
- Bosque y vegetación secundaria se separan mejor por la distancia a lo abierto que por la textura: declare la franja como estimada.
- Sombras profundas y dosel rugoso indican árboles grandes (bosque), no secundaria.

## Edición y limpieza
- Elimine «sal y pimienta» absorbiendo los polígonos bajo la UMC en el vecino de borde más largo, con una pasada final sin exclusiones para no dejar restos.
- En una zona de explotación activa, la clase de minería se impone al cauce dentro del bloque minero.
- Marque cada polígono editado a mano (`EDITADO = 1`, `MOTIVO`). Sin esa marca, el efecto de la edición no se puede medir.
- Respalde la capa antes de cada escritura y escriba en la base solo con una instrucción explícita de publicar.

## Validación de exactitud
- **Independencia.** Los puntos que ayudaron a construir o corregir la capa no la validan. Corregir con lo aprendido de una matriz de confusión invalida esa muestra.
- **Diseño.** Muestreo estratificado por clase del mapa; guarde el ráster de estratos y sus áreas el mismo día. Si el mapa cambia después del sorteo, use el estimador de Stehman (2014); si no, el de Olofsson et al. (2014).
- **Interpretación a ciegas** sobre la imagen de la fecha, sin ver la capa clasificada. Interprete la clase dominante en una ventana del tamaño de la UMC.
- **Orden.** Primero se edita y después se interpretan los puntos; durante la edición, la capa de puntos va apagada.
- Reporte exactitud global con intervalo de confianza, y exactitudes de usuario y de productor por clase. Un umbral habitual de aceptación es 85 %, pero pese el esfuerzo contra el efecto: no fuerce décimas con trabajo de poco retorno.

## Cambio entre fechas
- Compare solo coberturas con el mismo sensor, nivel, leyenda y UMC. Nunca compare una capa de Sentinel-2 con coberturas detalladas de ortofoto.
- Un desacuerdo entre fuentes mezcla escala, método y cambio real: sepárelos antes de atribuirlo a cambio. Muchos desacuerdos están a pocos metros del borde de la clase.
- Para el detalle del flujo con Google Earth Engine, NDVI y su postproceso, lea `references/sentinel2-gee-ndvi.md` solo si la tarea lo requiere.

## Cruce con áreas de intervención
Reporte las hectáreas por cobertura dentro de cada área (por método de explotación, por obra) con cuatro decimales, verifique que la suma cuadre con el área total y explique qué coberturas naturales se pierden.

## Eficiencia
- Clasifique y valide sobre una ventana de prueba antes de procesar la imagen completa.
- Calcule estadísticas zonales en el servidor (Earth Engine) o por bloques; descargue solo los productos finales.
- No vuelva a correr un paso que ya produjo su salida: verifique la fecha del archivo.
- Revise visualmente solo los polígonos que un criterio numérico marca como sospechosos.
