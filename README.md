# Logistics Network Delay Intelligence
### A Graph-Theoretic Approach to ETA Optimization

> **Consulting & Analytics Club — IIT Guwahati**

---

## Overview

This project builds a graph-based intelligence system for Delhivery's logistics network — India's largest fully-integrated logistics provider. The core idea is to model the entire delivery network as a directed graph (facilities as nodes, corridors as edges) and use this structure to produce smarter ETA predictions, surface bottleneck hubs, and generate actionable recommendations for network operations.

The standard OSRM routing engine Delhivery uses assumes clean traffic and shortest paths — but real-world logistics is far messier. This project demonstrates that a graph-aware model significantly outperforms the OSRM baseline by capturing facility dwell time, route-type constraints, and network cascading effects.

---

## Project Structure

```
IITG_project/
│
├── final_project_4.ipynb          # Main notebook — all phases end to end
├── delivery_data.csv              # Raw input data (download separately)
│
├── data/
│   ├── trip_legs_processed.csv    # Cleaned & feature-engineered trip legs
│   ├── route_corridors.csv        # Graph edges with delay metrics
│   ├── facility_scores.csv        # Hub-level betweenness & SLA scores
│   ├── chronic_corridors.csv      # Corridors with >20% chronic delay flag
│   └── predictions_output.csv    # Final predictions from all 3 models
│
├── visualizations/
│   ├── network.html               # Interactive logistics network graph
│   └── bottlenecks_pro.html       # Bottleneck hub visualization
│
├── memo/
│   ├── strategy_memo.pdf          # Network Operations Strategy Memo
│   └── strategy_memo.tex          # LaTeX source for the memo
│
└── README.md
```

---

## How to Run

### 1. Install dependencies

```bash
pip install pandas numpy networkx matplotlib seaborn scikit-learn pyvis node2vec torch torch-geometric
```

> **Note:** For Windows users, install `node2vec` via conda to avoid compiler issues:
> ```bash
> conda install -c conda-forge node2vec
> ```

### 2. Download the dataset

Download `delivery_data.csv` from the dataset link provided in the problem statement and place it in the root project folder.

### 3. Run the notebook

Open `final_project_4.ipynb` in Jupyter and run:

```
Kernel → Restart & Run All
```

This will regenerate all CSVs, visualizations, and model outputs.

---

## Notebook Structure

| Phase | Description |
|-------|-------------|
| **Phase 0** | Imports and library setup |
| **Phase 1** | Data pipeline — cleaning, feature engineering, CSV export |
| **Phase 2** | EDA — delay distribution, heatmaps, route-type analysis |
| **Phase 3** | Graph construction — directed weighted graph, Node2Vec embeddings |
| **Phase 4** | Bottleneck audit — betweenness centrality, SLA breach attribution, visualizations |
| **Phase 5** | ETA prediction — Baseline vs Node2Vec vs GraphSAGE benchmarking |
| **Phase 6** | FTL vs Carting decision framework |

---

## Key Results

### Model Performance (Test Set)

| Model | MAE (min) | Within 15% | Within 20% |
|-------|-----------|------------|------------|
| Baseline (Tabular) | 50.2 | 28.0% | 35.9% |
| Node2Vec Enhanced | 37.0 | 37.7% | 46.8% |
| **GraphSAGE (GNN)** | **37.4** | **37.6%** | **47.2%** |

GraphSAGE reduces MAE by **26%** over the baseline. SLA compliance at the 15% accuracy threshold improves by **35%**.

### Top 5 Bottleneck Hubs

| Rank | Facility | City | Delay Share |
|------|----------|------|-------------|
| 1 | Bilaspur HB | Gurgaon | 14.7% |
| 2 | Mankoli HB | Bhiwandi | 6.3% |
| 3 | Nelmangala H | Bangalore | 5.5% |
| 4 | Tathawde H | Pune | 2.6% |
| 5 | Dankuni HB | Kolkata | 2.4% |

Top 3 hubs combined drive **26.5%** of all national lateness.

### Network Stats
- **1,657** facilities (nodes)
- **2,783** corridors (edges)
- **98.2%** of trips arrive later than OSRM predicts
- **2.06×** median actual time vs OSRM estimate

---

## Deliverables

- ✅ Well-documented notebook with clean, reproducible code
- ✅ Interactive graph visualizations with bottleneck highlighting
- ✅ Model benchmarking (Baseline vs Node2Vec vs GraphSAGE)
- ✅ FTL vs Carting decision framework
- ✅ Network Operations Strategy Memo (PDF)

---

## Author

**Sumit Jain** | IIT Kanpur  
*Submitted to the Consulting & Analytics Club, IIT Guwahati*
