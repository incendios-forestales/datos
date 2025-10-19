# Contorno de Costa Rica (basado en la capa de áreas de conservación)

```bash
# Lista de capas en servicio WFS del Sinac
ogrinfo WFS:"http://geos1pne.sirefor.go.cr/wfs"

# Información sobre la capa de áreas de conservación
ogrinfo -al -so WFS:"http://geos1pne.sirefor.go.cr/wfs" "PNE:areas_conservacion"

# Descarga a GPKG de la capa WFS de áreas de conservación
ogr2ogr costarica.gpkg \
  WFS:"http://geos1pne.sirefor.go.cr/wfs" \
  -t_srs EPSG:4326 \
  -dialect sqlite \
  -sql "SELECT ST_Union(MakeValid(SHAPE)) AS geom FROM 'PNE:areas_conservacion'" \
  -nln costarica \
  -nlt POLYGON
```
