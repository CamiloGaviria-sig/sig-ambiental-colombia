# Verificaciones cartográficas (R con sf)

## Resumen de una capa
```r
library(sf); sf_use_s2(FALSE)
resumen <- function(ruta) {
  x <- st_zm(st_read(ruta, quiet = TRUE))
  x9377 <- st_transform(x, 9377)
  ha <- as.numeric(st_area(x9377)) / 1e4
  cat(basename(ruta), "| EPSG", st_crs(x)$epsg, "| n", nrow(x),
      "| inválidas", sum(!st_is_valid(x)), "| ha", round(sum(ha), 4), "\n")
  invisible(x9377)
}
```

## Atributo de área frente a geometría
```r
dif <- abs(x$AREA_HA - as.numeric(st_area(x)) / 1e4)
if (any(dif > 0.001)) message("Atributo de área desactualizado en ", sum(dif > 0.001), " entidades")
```

## Traslapes y huecos entre polígonos contiguos
```r
u <- st_union(x)
traslape_ha <- (sum(st_area(x)) - st_area(u)) / 1e4          # > 0 indica traslapes
huecos <- st_difference(st_convex_hull(u), u)                    # revisar visualmente
```
Para astillas, cuente las partes menores a un umbral (por ejemplo 0,01 ha) después de `st_cast(..., "POLYGON")`, y compare el área total antes y después del `st_cast`: si baja, se perdieron partes.

## Conteo en cruces
```r
n_in <- nrow(a); z <- st_intersection(a, b); cat("entran", n_in, "salen", nrow(z), "\n")
```
Si salen más filas de las esperadas, hay polígonos de `b` que se traslapan o geometrías duplicadas.

## Vértices para el cuadro de coordenadas
```r
v <- st_coordinates(st_cast(x9377, "POLYGON"))
v <- as.data.frame(v)
v <- v[!duplicated(v[, c("L2", "X", "Y")]) | !duplicated(v$L2, fromLast = TRUE), ]
```
Revise que el número de vértices por polígono coincida con el de la geometría menos el de cierre.

## Shapefile vacío con esquema
Al escribir una capa sin entidades, fije el tipo de geometría (`layer_options = "SHPT=POINT"` o `"SHPT=POLYGON"`) para que el visor no la tome como de otro tipo.

## Errores frecuentes
- Unir por un identificador que se repite entre muestras duplica filas.
- `st_cast` directo a POLYGON puede perder partes sin dar error: compare áreas.
- En ArcGIS, las tablas zonales con OID no consecutivos se unen por el campo de zona que crea la herramienta, no por `OBJECTID`.
