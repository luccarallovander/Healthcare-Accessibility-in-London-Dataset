# The Quality & Accessibility of London Hospitals (Dataset & Analysis)

This project builds an end-to-end, multi-level dataset, from web-scraped and API-retrieved data to analyses and visualisations assessing hospital **quality** and **accessibility** across London’s 33 boroughs.  
It integrates **Google Maps API data**, **spatial analysis**, and **public transport simulation** to provide actionable insights for the **Greater London Authority (GLA)** on how service quality and accessibility interact across the city.

---

## Overview

Public concern around NHS waiting times and transport affordability has grown in recent years.  
This analysis develops a **borough–hospital dataset** combining information on hospital operationality, ratings, and travel accessibility:

- **Hospital quality:** Scraped via Google Maps Places API, including name, operational status, rating, and review count.  
- **Accessibility:** Simulated public transport journeys from random borough points to the nearest hospital, recording distance, duration, and fare.

---

## Skills Used

- Web scraping (**RSelenium**) and API integration (**Google Maps Places**, **Distance Matrix**)  
- Spatial data analysis (`sf`, `geopandas`, `shapely`)  
- Random point generation and geospatial filtering  
- Data wrangling and aggregation in **R** (`tidyverse`, `sf`, `dplyr`)  
- Geospatial visualization and mapping (choropleths, accessibility surfaces)  
- Database construction and export (CSV / SQLite)

---

## Contributions

- **Built** a reproducible pipeline integrating Google Maps APIs with borough-level GIS data.  
- **Collected and validated** a dataset of **507 hospitals** across 33 London boroughs (down from 1,089 raw entries).  
- **Simulated** public transport journeys (20 random origins per borough) to measure **mean distance, duration, and fare** to the nearest hospital.  
- **Produced** borough-level indicators for hospital quality and accessibility:
  - `borough_mean_hospital_rating`  
  - `borough_hospital_count`  
  - `borough_operational_per` (% operational)  
  - `mean_fare_gbp`, `mean_duration_mins`, `mean_distance_km`  
- **Delivered** visualization-ready data and mapping outputs for urban policy analysis.

---

