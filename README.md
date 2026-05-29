🗺️ Spatial Vaccination Networks
 From County Adjacency to Network-Based Forecasting

![R](https://img.shields.io/badge/R-4.x-276DC3?logo=r)
![Shiny](https://img.shields.io/badge/Shiny-Dashboard-blue)
![CDC Data](https://img.shields.io/badge/Data-CDC%20%2B%20Census-green)
![Course](https://img.shields.io/badge/STAT%20636-Applied%20Multivariate%20Analysis-maroon)

📌 What This Project Does

COVID-19 vaccination rates across U.S. counties don't exist in isolation — they cluster spatially.
Counties that share borders tend to share healthcare infrastructure, commuter flows, and public
health environments. Most models ignore this. We didn't.

This project builds a **county-level adjacency network** (~3,100 nodes, ~30,000 edges) from
U.S. Census TIGER shapefiles and asks: *does treating counties as a graph — not as independent
rows — improve our ability to forecast vaccination coverage?*

The answer is yes. Network-aware forecasting cut RMSE nearly in half compared to the baseline.

🏆 Key Results

| Model | RMSE |
|---|---|
| Baseline (no network) | 11.387 |
| Network-aware (neighbour mean vax) | **7.484** |
| Baseline — missing county simulation | 14.044 |
| Network smoother — missing county simulation | **7.766** |

**The spatial signal is real and measurable.**

🧠 Methods

Data Sources
- CDC County-Level COVID-19 Vaccination Reports
- U.S. Census TIGER/Line Shapefiles (county polygons + adjacency)
- Social Vulnerability Index (SVI)
- Metro/rural classification + population data

Network Construction
Built a **queen adjacency graph** — two counties are connected if they share a geographic
boundary. Simple, principled, and it works.

Node Features (per county)
- Fully vaccinated %
- Booster coverage %
- Social Vulnerability Index (SVI)
- Metro vs. rural classification
- Population
- Neighbour-averaged vaccination % (spatial smoothing feature)

Graph Metrics Computed
- Degree, Betweenness, Closeness
- Community detection via Louvain algorithm

Forecasting
- **Baseline model:** county features only, no network
- **Network-aware model:** adds neighbour vaccination average as a feature
- **Missing county simulation:** hides counties, estimates via spatial smoothing, compares error

Dashboard (8 Modules)
Built in R Shiny with Leaflet and interactive plots:
1. County Explorer
2. Spatial Map (choropleth)
3. Network Graph (force-directed)
4. Feature Explorer
5. Model & Forecast
6. Unobserved Counties (simulation)
7. Insights & Summary
8. Downloads

🚀 Run It Yourself

### Requirements
```r
install.packages(c(
  "shiny", "igraph", "sf", "leaflet", "ggplot2",
  "dplyr", "tidyr", "spdep", "DT", "plotly"
))
```

Run the dashboard
```r
# Open Vaccine_Project_Network_GNN_Final.Rmd in RStudio
# Knit or run chunk by chunk
# The Shiny dashboard launches from the final section
```


🔮 Future Work

This project exports a **GNN-ready dataset** (`nodes.csv`, `edges.csv`) for future modeling:
- Graph Convolutional Networks (GCN)
- GraphSAGE for inductive learning on new counties
- Graph Attention Networks (GAT)
- Temporal models (DCRNN, TGAT) for time-series vaccination trends
- Richer networks using real mobility or healthcare facility data

📊 Project Snapshots

| County Explorer | Spatial Choropleth Map |
|---|---|
| Filter by state, county, degree | Interactive U.S. vaccination map |

| Network Graph | Model Performance |
|---|---|
| Force-directed, colored by community | Baseline vs. network-aware RMSE |

👥 Team

Name

 Saher Thekedar,
 Eduardo Macchi,
 Asmita Shivling Desai 

*Texas A&M University — STAT 636: Applied Multivariate Analysis*

---
 📚 References

- CDC COVID-19 Vaccinations: https://data.cdc.gov
- U.S. Census TIGER Shapefiles: https://www.census.gov
- Kipf & Welling (2016) — Graph Convolutional Networks
- Newman (2010) — Networks: An Introduction
- Li et al. (2018) — DCRNN for spatial-temporal forecasting

