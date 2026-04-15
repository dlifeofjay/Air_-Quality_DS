# 🌿 Salford Air Quality Monitoring Project

A spatial and statistical analysis of indoor and outdoor air quality across the University of Salford campus, conducted using two professional-grade sensor devices — the **Temtop AIRING 2000** and the **Temtop M2000**.

---

## 📌 Project Overview

This project investigates particulate matter (PM2.5, PM10), CO₂ concentration, temperature, and humidity across **10 sampling points** on the University of Salford campus. Raw sensor readings are cleaned, statistically grouped, benchmarked against international health standards, and visualised both through static charts and an interactive geospatial map.

The work is structured as a **Jupyter Notebook** (`AIR QUALITY.ipynb`) and is accompanied by a full written research report and a presentation.

---

## 📂 Repository Structure

```
Air Quality/
│
├── AIR QUALITY.ipynb                               # Main analysis notebook
├── SALFORD AIR QUALITY MONITORING PROJECT.docx     # Full written report
├── SALFORD AIR QUALITY MONITORING PROJECT.pdf      # PDF version of the report
├── Spatial Analysis of Air Quality Across          # Presentation slides
│   Salford University.pptx
│
└── Images/                                         # All generated visualisations
    ├── All Air Qual.png
    ├── campus plot.png
    ├── PM2.5 AIRING 2000.png
    ├── PM10 AIRING 2000.png
    ├── Humidity AIRING 2000.png
    ├── PM2.5 & PM10.png
    ├── PM2.5 & Humidity.png
    ├── PM10 & Humidity.png
    ├── Correlation Matrix (Airing 2000).png
    ├── M2000 all col.png
    ├── M2000 PM2.5 AIRING 2000.png
    ├── M2000 PM10 AIRING 2000.png
    ├── M2000 Humidity.png
    ├── M2000 PM2.5 & PM10.png
    ├── M2000 PM2.5 & CO2(ppm).png
    ├── M2000 PM2.5 & Temperature.png
    ├── M2000 PM2.5 & Humidity.png
    ├── M2000 PM10 & CO2(ppm).png
    ├── M2000 PM10 & Temperature.png
    ├── M2000 PM10 & Humidity.png
    ├── M2000 CO2 & Temperature.png
    ├── M2000 CO2 & Humidity.png
    ├── M2000 Temperature & Humidity.png
    └── Correlation Matrix (M2000).png
```

---

## 🔬 Methodology

### Instruments Used

| Device | Metrics Captured |
|---|---|
| **Temtop AIRING 2000** | PM2.5 (µg/m³), PM10 (µg/m³), Humidity (%RH) |
| **Temtop M2000** | PM2.5 (µg/m³), PM10 (µg/m³), CO₂ (ppm), Temperature (°C), Humidity (%) |

### Sampling Design

- **10 fixed sampling points** across the University of Salford campus
- Points span a mix of areas including indoor corridors, open outdoor spaces, and traffic-adjacent zones
- Multiple repeat readings taken at each location; data aggregated by mean per sampling point

### Analysis Pipeline

The notebook follows this sequential workflow:

```
1. Data Loading           → Read Excel file (two sheets: AIRING 2000 / M2000)
2. Data Cleaning          → Strip whitespace from column headers
3. Grouping & Aggregation → Mean readings per (AREA, SAMPLING POINT)
4. Visualisation          → Bar charts, scatter plots, and correlation heatmaps
5. Benchmarking           → Compare PM2.5 against WHO & EU thresholds
6. Geospatial Mapping     → Convert OS National Grid / DMS coordinates → WGS84
                            → Interactive Plotly scatter_mapbox over OpenStreetMap
```

---

## 📊 Key Analyses

### AIRING 2000 Series
- **Overall distribution** of PM2.5, PM10, and Humidity across all 10 sampling points
- **PM2.5 benchmark chart** comparing readings against:
  - 🟢 WHO guideline: **5 µg/m³**
  - 🔴 EU 2020 limit: **20 µg/m³**
  - ⚫ EU 2040 target: **10 µg/m³**
- **PM10 & Humidity** distribution by sampling unit
- **Scatter analysis**: PM2.5 vs PM10, PM2.5 vs Humidity, PM10 vs Humidity
- **Correlation matrix** (PM2.5, PM10, Humidity)

### M2000 Series
- **Full multi-metric comparison** across all 5 variables per sampling point
- **PM2.5 benchmarked** against WHO and EU standards
- **Cross-variable scatter plots** for all permutations:
  - PM2.5 & PM10 · PM2.5 & CO₂ · PM2.5 & Temperature · PM2.5 & Humidity
  - PM10 & CO₂ · PM10 & Temperature · PM10 & Humidity
  - CO₂ & Temperature · CO₂ & Humidity · Temperature & Humidity
- **Full 5×5 correlation matrix** (PM2.5, PM10, CO₂, Temperature, Humidity)

### Geospatial Analysis
- Sampling point coordinates converted from:
  - **OS National Grid (EPSG:27700)** → WGS84 (EPSG:4326) via `pyproj`
  - **DMS (Degrees, Minutes, Seconds)** → Decimal Degrees for points with GPS coords
- Interactive campus map with colour-scaled PM2.5 bubbles (`plotly.express.scatter_mapbox`)

---

## 🗺️ Campus Map

![Salford Campus Air Quality Map](Images/campus%20plot.png)

---

## 📈 Sample Visualisations

| Chart | Description |
|---|---|
| ![](Images/All%20Air%20Qual.png) | Overall AIRING 2000 readings across all sampling points |
| ![](Images/M2000%20all%20col.png) | Full M2000 multi-metric comparison |
| ![](Images/Correlation%20Matrix%20(M2000).png) | M2000 full correlation matrix |
| ![](Images/PM2.5%20AIRING%202000.png) | PM2.5 levels benchmarked against WHO & EU thresholds |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| `Python 3` | Core programming language |
| `pandas` | Data loading, cleaning, and grouping |
| `numpy` | Numerical operations |
| `matplotlib` | Static bar charts and visualisations |
| `seaborn` | Scatter plots and correlation heatmaps |
| `plotly.express` | Interactive geospatial map |
| `pyproj` | Coordinate reference system transformation (OSGB → WGS84) |

---

## ▶️ Running the Notebook

### Prerequisites

```bash
pip install numpy pandas matplotlib seaborn plotly pyproj openpyxl
```

> **Note:** The raw data file (`AIr Quality Data - RDD 2026.xlsx`) is not included in this repository due to its size. To reproduce the analysis, place the file in a local path and update the `pd.read_excel(...)` path in cells 1 and 23 of the notebook.

### Launch

```bash
jupyter notebook "AIR QUALITY.ipynb"
```

---

## 📋 Health Benchmarks Referenced

| Standard | PM2.5 Limit | Source |
|---|---|---|
| WHO Air Quality Guideline | 5 µg/m³ | WHO 2021 |
| EU Current Limit | 20 µg/m³ | EU Directive 2008/50/EC |
| EU 2040 Target | 10 µg/m³ | EU Zero Pollution Action Plan |

---

## 📄 Report & Presentation

Full findings, methodology, recommendations, and a proposed follow-on study are documented in:

- 📘 [`SALFORD AIR QUALITY MONITORING PROJECT.pdf`](SALFORD%20AIR%20QUALITY%20MONITORING%20PROJECT.pdf)
- 📊 [`Spatial Analysis of Air Quality Across Salford University.pptx`](Spatial%20Analysis%20of%20Air%20Quality%20Across%20Salford%20University.pptx)

---

## 👤 Author

**Jay** — Data Science Portfolio  
University of Salford | 2026  
[GitHub Profile](https://github.com/dlifeofjay)
