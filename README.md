## Background

The Center for Linkage and Acquisition of Data (CLAD) developed the CLAD Hex Environmental Linkage (CHEL) dataset for the All of Us Research Program to help researchers study the relationship between where people live and their health. CHEL draws on the CDC’s Environmental Justice Index (EJI), which includes data from government and commercial sources on environmental conditions, social vulnerability, community health, and climate hazards. We translate these measures into a common geographic grid so we can link them to participant health data.

CHEL uses H3, a geographic indexing system developed by Uber that divides the world into a grid of cells that are primarily hexagonal. H3 has multiple resolutions, with higher resolution numbers representing smaller cells. We selected resolution 3 (Hex3) because it provides a consistent, standardized geography for environmental variables and supports data sharing when researchers cannot access more detailed location information. CHEL combines this geographic aggregation with additional privacy safeguards to reduce the risk of identifying participants.

## Example: Linking Participants to Different CHEL Datasets by Year

This example demonstrates how to:

1. Link CHEL tabular data (`CHEL_2022.csv`, `CHEL_2024.csv`) to a hex grid (`hex3_grid_with_h3.gpkg`) using `hex_id`
2. Assign participants to the correct CHEL dataset based on `start_date`

- Participants enrolled **2015 to 2018** → linked to `CHEL_2022`
- Participants enrolled **2019 to 2022** → linked to `CHEL_2024`

### Python Example

```python
import pandas as pd
import geopandas as gpd

# -------------------------------------------------------------------
# 1. Load hex grid and CHEL CSVs, then join on hex_id
# -------------------------------------------------------------------
hex_grid = gpd.read_file("data/hex3_grid_with_h3.gpkg")

chel_2022_csv = pd.read_csv("data/CHEL_2022.csv")
chel_2024_csv = pd.read_csv("data/CHEL_2024.csv")

# Join tabular CHEL data to hex geometries
chel_2022 = hex_grid.merge(chel_2022_csv, on="hex_id", how="left")
chel_2024 = hex_grid.merge(chel_2024_csv, on="hex_id", how="left")

# -------------------------------------------------------------------
# 2. Example participant data
# -------------------------------------------------------------------
participant_locations = [
    {"participant_id": 1, "lat": 40.4406, "lon": -79.9959, "start_date": "2023_05_14 08:30:00"},
    {"participant_id": 2, "lat": 41.4993, "lon": -81.6944, "start_date": "2023_11_02 14:10:00"},
    {"participant_id": 3, "lat": 39.9612, "lon": -82.9988, "start_date": "2024_01_15 09:00:00"},
    {"participant_id": 4, "lat": 42.3314, "lon": -83.0458, "start_date": "2024_07_22 16:45:00"},
]

participant_df = pd.DataFrame(participant_locations)

participant_df["start_date"] = pd.to_datetime(
    participant_df["start_date"].str.replace("_", "-"),
    format="%Y-%m-%d %H:%M:%S",
    errors="coerce"
)

participant_gdf = gpd.GeoDataFrame(
    participant_df,
    geometry=gpd.points_from_xy(participant_df["lon"], participant_df["lat"]),
    crs="EPSG:4326",
)

# Ensure CRS matches
chel_2022 = chel_2022.to_crs(participant_gdf.crs)
chel_2024 = chel_2024.to_crs(participant_gdf.crs)

# -------------------------------------------------------------------
# 3. Split participants by year
# -------------------------------------------------------------------
participants_2022 = participant_gdf[(participant_gdf["start_date"].dt.year >= 2015) & (participant_gdf["start_date"].dt.year <= 2018)]
participants_2024 = participant_gdf[(participant_gdf["start_date"].dt.year >= 2019) & (participant_gdf["start_date"].dt.year <= 2022)]

# -------------------------------------------------------------------
# 4. Spatial join to appropriate CHEL dataset
# -------------------------------------------------------------------
joined_2022 = gpd.sjoin(participants_2022, chel_2022, how="left", predicate="intersects")
joined_2024 = gpd.sjoin(participants_2024, chel_2024, how="left", predicate="intersects")

# Optional: record which CHEL dataset was used
joined_2022["chel_year"] = 2022
joined_2024["chel_year"] = 2024

# -------------------------------------------------------------------
# 5. Combine results
# -------------------------------------------------------------------
output = pd.concat([joined_2022, joined_2024], ignore_index=True)
output = gpd.GeoDataFrame(output, geometry="geometry", crs=participant_gdf.crs)

if "index_right" in output.columns:
    output = output.drop(columns="index_right")

print(output.head())
```

### Result

Each participant will be assigned attributes from the correct CHEL dataset
based on the year of their `start_date`. Columns that only exist in one
CHEL dataset will appear as `NaN` for rows linked to the other dataset.
