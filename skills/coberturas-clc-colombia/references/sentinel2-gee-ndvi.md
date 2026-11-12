# Coberturas históricas y NDVI con Sentinel-2

Úselo cuando un análisis exige dos temporalidades (por ejemplo, fragmentación para una sustracción) y no hay coberturas históricas.

## Flujo
1. **Insumos.** Área de interés con un buffer suficiente para el análisis de paisaje (por ejemplo 5 km), polígonos de entrenamiento desde las coberturas actuales con una erosión interna de 15 m para evitar bordes, y todo en EPSG:4326 para subirlo a Earth Engine.
2. **En Earth Engine.**
   - Sentinel-2 armonizado, el mismo nivel de procesamiento en todas las fechas.
   - Máscara Cloud Score+ (por ejemplo `cs_cdf ≥ 0,60`).
   - Mediana de época seca para reducir nubes y diferencias fenológicas.
   - Random Forest (unos 300 árboles), reserva de validación y matriz de confusión.
   - NDVI de T1 y T2 y su diferencia; serie anual por zona.
   - Exporte en un sistema proyectado y reproyecte a EPSG:9377 en el postproceso.
3. **Postproceso.** Generalice con filtro modal 3×3 y eliminación de manchas bajo la UMC, vectorice, etiquete con el código Corine y compruebe que el área del vector coincida con la del ráster.

## Reglas
- T1 de Sentinel-2 se compara con Sentinel-2 actual, nunca con coberturas detalladas.
- La reserva de validación sale de la misma fuente que el entrenamiento y es optimista: agregue una validación independiente sobre imágenes históricas de alta resolución.
- Si hay pocas áreas de entrenamiento para T1, pida al profesional que digitalice puntos adicionales sobre imágenes históricas.

## Productos NDVI
- Mapas de NDVI T1, T2 y ΔNDVI.
- Estadísticas por zona (área de intervención, entorno inmediato, paisaje) y por clase.
- Porcentaje del área con |ΔNDVI| mayor a un umbral declarado (por ejemplo 0,15).
- Serie anual de época seca con banda de percentiles 10–90.

Sirven como evidencia del estado y la tendencia de la vegetación, para identificar agentes de cambio y como línea base de seguimiento de la restauración.

## Referencias
Breiman (2001); Drusch et al. (2012); Pasquarella et al. (2023), Cloud Score+; Rouse et al. (1974); Olofsson et al. (2014); Stehman (2014).
