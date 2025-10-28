# Estimating Power Outage Impacts from the February 2021 Texas Winter Storms

## About

This repository contains a geospatial analysis estimating the number of homes that lost power in the Houston metropolitan area during the February 2021 Texas winter storms. The analysis uses remotely-sensed night lights data to identify areas that experienced blackouts and investigates potential socioeconomic disparities in storm impacts.

**Analysis Objectives:**
- Identify locations that experienced power outages using VIIRS night lights data
- Estimate the number of homes affected by blackouts
- Examine whether blackout impacts were disproportionately experienced across different socioeconomic groups

## Repository Structure

```
texas-blackout-analysis/
│
├── README.md
├── .gitignore
├── texas-blackout-analysis.Rproj
├── texas_blackout.qmd
│
└── data/
    ├── VNP46A1/
    │   ├── VNP46A1.A2021038.h08v05.001.2021039064328.tif
    │   ├── VNP46A1.A2021038.h08v06.001.2021039064329.tif
    │   ├── VNP46A1.A2021047.h08v05.001.2021048091106.tif
    │   └── VNP46A1.A2021047.h08v06.001.2021048091105.tif
    ├── gis_osm_buildings_a_free_1.gpkg
    ├── gis_osm_roads_free_1.gpkg
    └── ACS_2019_5YR_TRACT_48_TEXAS.gdb/
```

**Note:** The `data/` folder is included in `.gitignore` and is not tracked by version control due to file size. See below for data access instructions.

## Data

### Access

1. Download the data folder from [this link](https://drive.google.com/file/d/1bTk62xwOzBqWmmT791SbYbHxnCdjmBtw/view?usp=drive_link)
2. Unzip the downloaded folders
3. Place the unzipped data into a `data/` folder in the root directory of this repository
4. Verify the folder structure matches the Repository Structure shown above

### Data Sources

**VIIRS Night Lights Data (VNP46A1)**
- NASA's Visible Infrared Imaging Radiometer Suite onboard the Suomi satellite
- Tiles h08v05 and h08v06 covering the Houston area
- Dates: 2021-02-07 (before storms) and 2021-02-16 (after storms)
- Source: NASA's Level-1 and Atmospheric Archive & Distribution System Distributed Active Archive Center (LAADS DAAC)
- Accessed via: [NASA Worldview](https://worldview.earthdata.nasa.gov/)

**OpenStreetMap - Roads**
- Highway and road network data for the Houston metropolitan area
- File: `gis_osm_roads_free_1.gpkg`
- Source: [Geofabrik Download Server](https://download.geofabrik.de/)

**OpenStreetMap - Buildings**
- Residential building footprints for the Houston metropolitan area
- File: `gis_osm_buildings_a_free_1.gpkg`
- Source: [Geofabrik Download Server](https://download.geofabrik.de/)

**U.S. Census Bureau - American Community Survey (ACS)**
- 5-Year estimates (2015-2019) at the census tract level for Texas
- Geodatabase: `ACS_2019_5YR_TRACT_48_TEXAS.gdb`
- Includes median household income and demographic data
- Source: [U.S. Census Bureau](https://www.census.gov/programs-surveys/acs)

## Methodology

The analysis workflow includes:

1. **Blackout Detection:** Calculate change in night light intensity between 2021-02-07 and 2021-02-16, identifying areas with drops > 200 nW cm⁻²sr⁻¹
2. **Highway Exclusion:** Remove areas within 200m of highways to avoid falsely identifying reduced traffic as power outages
3. **Home Identification:** Spatially join blackout areas with residential building data to estimate homes affected
4. **Socioeconomic Analysis:** Link impacted areas with census tract data to examine income distributions

All spatial data is reprojected to EPSG:3083 (NAD83 / Texas Centric Albers Equal Area) for accurate area calculations.

## Author

Emily Miller

[GitHub](https://github.com/yourusername)

## Course Information

This analysis was completed for **EDS 223: Geospatial Analysis and Remote Sensing** at the Bren School of Environmental Science & Management, UC Santa Barbara.

- **Instructor:** Ruth Oliver
- **Assignment:** Homework 3 - Identifying the Impacts of Extreme Weather
- **Date:** October 2025

## References

- Wikipedia. 2021. "2021 Texas power crisis." Last modified October 2, 2021. https://en.wikipedia.org/wiki/2021_Texas_power_crisis
- Assignment instructions: [EDS 223 Course Website](https://eds-223-geospatial.github.io/assignments/HW3.html)
