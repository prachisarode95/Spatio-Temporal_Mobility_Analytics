# NYC Bike Rush — Spatio-Temporal Mobility Analytics

> Analyzing New York City bike-share demand patterns during rush hours using spatial databases, census boundaries, and interactive visualizations.

---

## Project Overview

This project explores **when and where bike demand spikes** across New York City during rush hours. Using real-world bike station and trip data from September 17, 2024, I built a spatial data pipeline that maps trip patterns, links them to NYC census tracts, and surfaces actionable insights for smarter bike repositioning.

**Key question answered:** *Which neighborhoods face the highest bike demand during morning and evening rush hours — and how can operators respond strategically?*

---

## Datasets Used

| Dataset | Description |
|---|---|
| `stations.csv` | Bike station IDs with latitude and longitude |
| `trip_data.csv` | Individual trip records with start/end times, bike type, and station IDs |
| NYC 2020 Census Tract Boundaries | Official boundary file from the US Census Bureau containing borough names and tract IDs |

> **Why Census Tracts?** They provide standardized, consistent geographic units that make it easy to compare demand across neighborhoods — more reliable than informal neighborhood names.

---

## Tools & Technologies

| Tool | Role |
|---|---|
| **PostgreSQL** | Database for storing and querying tabular data |
| **PostGIS** | Adds spatial capabilities to PostgreSQL (geometry, distance, joins) |
| **QGIS** | Interactive map visualization and time-based animation |
| **Python** | Data processing and chart generation (Pandas, Matplotlib) |

---

## What I Built

### Database & Spatial Setup
- Created `stations` and `trip_data` tables with geometry columns
- Enabled the PostGIS extension and reprojected all coordinates to **UTM Zone 18N (EPSG:32618)** for accurate distance calculations in New York

### Spatial & Time Analysis
- Grouped trip start times into **30-minute intervals** using `DATE_TRUNC()` and `EXTRACT()`
- Used **`ST_Within()`** to spatially join each bike station to its census tract
- Aggregated trip counts by census tract and time interval to find demand hotspots
- Identified the **busiest stations** and used buffer analysis to locate nearby stations that could cover overflow demand

### Visualizations
- **Animated choropleth map** in QGIS showing how trip counts change across census tracts throughout the day
- **Bar chart** in Python showing trip volume per 30-minute window

---

## Visualizations

### Animated Trip Count Map (QGIS Time Manager)

https://github.com/user-attachments/assets/c84d7930-4373-4533-92cc-fbde3ea1ac22

### Trip Counts by Half-Hour Interval (Python)

![Bar Chart](https://github.com/user-attachments/assets/92d38bc1-800b-4215-a213-8737afc1149c)

---

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/prachisarode95/Spatio-Temporal_Mobility_Analytics.git
cd Spatio-Temporal_Mobility_Analytics
```

### 2. Set Up PostgreSQL with PostGIS
```sql
CREATE DATABASE nyc_bike_trips;
\c nyc_bike_trips;
CREATE EXTENSION postgis;
```

### 3. Install Python Dependencies
```bash
pip install -r requirements.txt
```

### 4. Load Data
- Open **QGIS DB Manager** and load `stations.csv`, `trip_data.csv`, and `nyct2020.geojson`

### 5. Run SQL Analysis Scripts
- Execute the scripts in `PostGIS_Queries/` via QGIS DB Manager

### 6. Generate Visualizations
```bash
python scripts/visualization.py
```
Or open the ready-to-use QGIS project: `QGIS_Project/spatio_temporal_analysis.qgs`

---

## Project Structure

```
├── Data/
│   ├── Raw/                  # Original input files
│   └── Processed/            # CSV outputs from SQL queries
├── PostGIS_Queries/          # SQL scripts for each analysis step
├── QGIS_Project/             # Ready-to-use QGIS project file
├── Data_Visualization/       # Python-generated plots
├── Docs/                     # Project methodology and notes
└── requirements.txt          # Python package list
```

---

## Results & Takeaways

- Mapped NYC rush hour bike demand down to the census tract level
- Identified **peak demand windows** and the stations that drive them
- Proposed a **buffer-based repositioning strategy** to move bikes proactively before demand spikes
- Produced map animations and charts ready for use in planning dashboards or presentations

---

## Skills Demonstrated

`PostgreSQL` · `PostGIS` · `Spatial SQL` · `QGIS` · `Python` · `Pandas` · `Matplotlib` · `Geospatial Data Modeling` · `Census Data Integration` · `Urban Mobility Analysis`

---

*Built by [Prachi Sarode](https://github.com/prachisarode95)*
