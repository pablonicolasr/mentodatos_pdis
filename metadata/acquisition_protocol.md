# Protocolo de adquisición - Salar de Olaroz

## Área de estudio
Salar de Olaroz, departamento de Susques, provincia de Jujuy, Argentina.

## Fuente de datos
Microsoft Planetary Computer STAC API.

## Colección
`sentinel-2-l2a`

## Producto
Sentinel-2 Level-2A Surface Reflectance.

## Criterios de búsqueda
- AOI: `labels/olaroz_aoi.geojson`
- Rango temporal: `2025-06-01/2025-09-30`
- Nubosidad máxima: `20%`
- Bandas exportadas: `B01,B02,B03,B04,B05,B06,B07,B08,B8A,B09,B11,B12,SCL`
- Resolución de trabajo: 20 metros
- Criterio de selección: escena candidata con menor `eo:cloud_cover`

## Archivos generados
- Raster multibanda: `raster/olaroz_sentinel2_l2a_seca_2024_multiband.tif`
- Escenas candidatas: `metadata/sentinel2_olaroz_candidate_scenes.csv`
- Escena seleccionada CSV: `metadata/selected_sentinel2_olaroz_scene.csv`
- Escena seleccionada STAC JSON: `metadata/selected_sentinel2_olaroz_item.json`
- AOI: `labels/olaroz_aoi.geojson`

## Uso previsto
Este dataset se utilizará para una práctica de análisis de datos y aprendizaje automático clásico.
Los alumnos podrán extraer valores espectrales e índices desde el raster usando polígonos GeoJSON etiquetados.
