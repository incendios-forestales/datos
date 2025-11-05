# Datos

## Áreas de conservación

```bash
# Lista de capas en servicio WFS del Sinac
ogrinfo WFS:"http://geos1pne.sirefor.go.cr/wfs"

# Información sobre la capa de áreas de conservación
ogrinfo -al -so WFS:"http://geos1pne.sirefor.go.cr/wfs" "PNE:areas_conservacion"

# Descarga en formato GPKG
ogr2ogr areas-conservacion.gpkg \
  WFS:"http://geos1pne.sirefor.go.cr/wfs" "PNE:areas_conservacion" \
  -nln areas-conservacion \
  -t_srs EPSG:4326 \
  -makevalid
```

## Áreas silvestres protegidas (ASP)

```bash
# Lista de capas en servicio WFS del Sinac
ogrinfo WFS:"http://geos1pne.sirefor.go.cr/wfs"

# Información sobre la capa de ASP
ogrinfo -al -so WFS:"http://geos1pne.sirefor.go.cr/wfs" "PNE:areas_silvestres_protegidas"

# Descarga en formato GPKG
ogr2ogr asp.gpkg \
  WFS:"http://geos1pne.sirefor.go.cr/wfs" "PNE:areas_silvestres_protegidas" \
  -nln asp \
  -t_srs EPSG:4326 \
  -makevalid
```

## Contorno de Costa Rica (basado en la capa de áreas de conservación)

```bash
# Lista de capas en servicio WFS del Sinac
ogrinfo WFS:"http://geos1pne.sirefor.go.cr/wfs"

# Información sobre la capa de áreas de conservación
ogrinfo -al -so WFS:"http://geos1pne.sirefor.go.cr/wfs" "PNE:areas_conservacion"

# Descarga en formato GPKG
ogr2ogr costarica.gpkg \
  WFS:"http://geos1pne.sirefor.go.cr/wfs" \
  -t_srs EPSG:4326 \
  -dialect sqlite \
  -sql "SELECT ST_Union(MakeValid(SHAPE)) AS geom FROM 'PNE:areas_conservacion'" \
  -nln costarica \
  -nlt POLYGON
```
