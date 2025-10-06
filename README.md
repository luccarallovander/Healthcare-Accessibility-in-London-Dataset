# The Quality & Accessibility of London Hospitals (Dataset & Analysis)

_An end-to-end, multi-level dataset and analysis for the Greater London Authority (GLA) assessing hospital **quality** (Google ratings/operationality) and **accessibility** (travel time, distance, fare) across London’s 33 boroughs._

---

## Overview

Public dissatisfaction with NHS waiting times and rising transport costs has grown in recent years.  
This project builds a **borough–hospital multi-level dataset** to help the GLA understand how **service quality** and **transport accessibility** interact:

- **Hospital-level quality:** Google Maps Places data (name, status, rating, reviews, coordinates).  
- **Borough-level accessibility:** Public transport **distance, duration, and fare** to the **nearest hospital**, averaged from simulated journeys across each borough.

**Outputs**
- Cleaned hospital-level and borough-level tables (CSV & SQLite).  
- Reproducible R code to **scrape**, **georeference**, **query APIs**, and **visualize**.  
- Borough maps of hospital counts, mean ratings, mean travel time, and mean fare.

---

## Methodology

### 1) Primary Data (Hospitals: Quality & Location)
- **Source:** Google Maps Places API (Text Search, per borough).  
- **Fields:** `name`, `business_status` (operational), `formatted_address`, `rating`, `user_ratings_total`, `lat`, `lng`.  
- **Cleaning:** Remove records outside true borough boundaries (see georeferencing).

> Raw Google results can bleed across borders due to relevance heuristics—hence strict boundary checks below.

### 2) Georeferencing to Borough Boundaries
- **Boundary source:** London GIS borough shapefiles (scraped from data.london.gov.uk via **RSelenium**).  
- **Process:** Convert to `EPSG:4326`, cast hospital results to `sf`, and **filter strictly** by polygon inclusion.  
- **Effect:** Hospitals reduced from **1,089 → 507** after boundary enforcement.

### 3) Secondary Data (Accessibility via Public Transport)
- **Journey simulation:** Generate **20 random origin points per borough**.  
- **Nearest facility:** For each origin, match to **nearest hospital within the borough** (distance approximation, then confirmed via API).  
- **API queries:** Google **Distance Matrix API** (mode = `transit`) for **distance**, **duration**, **fare** for each origin–hospital pair.
- **Aggregation:** Compute borough-level means: `mean_distance_km`, `mean_duration_mins`, `mean_fare_gbp`.

### 4) Multi-Level Merge & Transformations
- Merge hospital-level with borough aggregates → **multi-level analytic table**.  
- Add derived indicators:
  - `borough_mean_hospital_rating`  
  - `borough_hospital_count`  
  - `borough_operational_count`  
  - `borough_operational_per` (% operational)

---
