# Reporte de curación - Práctico 2 M10

Run ID: `run_20260820_212410`

## Dataset

- Filas originales: 21,507
- Columnas originales: 22
- Filas curadas: 21,507
- Columnas curadas: 30

## Integridad

| dataset            |   rows |   columns |   missing_total |   missing_cells_pct |   infinite_total |   exact_duplicates |   duplicated_sample_xy_class | constant_columns           |
|:-------------------|-------:|----------:|----------------:|--------------------:|-----------------:|-------------------:|-----------------------------:|:---------------------------|
| pixels_raw         |  21507 |        22 |               0 |                   0 |                0 |                  0 |                            0 | season, confidence, source |
| pixels             |  13878 |        22 |               0 |                   0 |                0 |                  0 |                            0 | season, confidence, source |
| features           |  13878 |        31 |               0 |                   0 |                0 |                  0 |                            0 | season, confidence, source |
| clean_reference    |  13878 |        31 |               0 |                   0 |                0 |                  0 |                            0 | season, confidence, source |
| balanced_reference |   8025 |        31 |               0 |                   0 |                0 |                  0 |                            0 | season, confidence, source |

## Decisiones

| issue                              | evidence                                                                                           | action                                             | justification                                                                        |   affected_rows | affected_columns                                                                                   |
|:-----------------------------------|:---------------------------------------------------------------------------------------------------|:---------------------------------------------------|:-------------------------------------------------------------------------------------|----------------:|:---------------------------------------------------------------------------------------------------|
| Valores faltantes                  | 0 celdas nulas                                                                                     | No imputar                                         | No corresponde imputar donde no hay faltantes.                                       |               0 |                                                                                                    |
| Variables constantes               | season, confidence, source                                                                         | Excluir como predictoras                           | No aportan varianza al modelo.                                                       |               0 | season, confidence, source                                                                         |
| Fuga por dependencia entre píxeles | Múltiples píxeles por sample_id                                                                    | Usar split agrupado por sample_id                  | Evita que píxeles del mismo polígono caigan en train y test simultáneamente.         |               0 | sample_id                                                                                          |
| Variable SCL                       | Control de calidad Sentinel-2                                                                      | Mantener como control, no como predictor principal | Puede representar el filtro de extracción y no una propiedad física de la cobertura. |               0 | scl                                                                                                |
| Categorías textuales               | Posibles espacios invisibles                                                                       | Aplicar strip a strings                            | Evita categorías duplicadas por formato.                                             |               0 |                                                                                                    |
| Ingeniería geoespacial             | x_centered, y_centered, dist_to_global_centroid, angle_to_global_centroid, dist_to_sample_centroid | Crear variables derivadas de x/y                   | Permite modelar patrones espaciales con validación cuidadosa.                        |               0 | x_centered, y_centered, dist_to_global_centroid, angle_to_global_centroid, dist_to_sample_centroid |
| Outliers multivariados             | IsolationForest                                                                                    | Crear flag, no eliminar automáticamente            | En salares los extremos pueden ser ambientalmente válidos.                           |            5855 | flag_outlier_iso                                                                                   |

## Salidas

- CSV curado: `C:\Users\pablonicolasr\Desktop\pablonicolas\educacion_formal\mentodatos2026\repo\mentodatos_pdis\data\processed\olaroz_samples_curated_practico2.csv`
- SQLite ETL: `C:\Users\pablonicolasr\Desktop\pablonicolas\educacion_formal\mentodatos2026\repo\mentodatos_pdis\data\warehouse\m10_practico2_etl.sqlite`
- Decision log: `C:\Users\pablonicolasr\Desktop\pablonicolas\educacion_formal\mentodatos2026\repo\mentodatos_pdis\data\quality\decision_log_practico2.csv`
