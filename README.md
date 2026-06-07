# CO₂ Emissions Forecasting — Multi-Model Analysis

From emissions data to climate insight: multi-model forecasting of national CO₂ emissions across the world's top 10 emitters (1970–2022), comparing Ridge, Random Forest, XGBoost, and kernel-tuned SVR to identify the most reliable predictor of future emissions. Delivered as an interactive Power BI dashboard translating model outputs into policy-oriented indicators.

---

## Project Objectives

| # | Objective |
|---|-----------|
| 1 | Compare linear, ensemble, and kernel-based models on long-horizon emissions data |
| 2 | Engineer temporal and structural features to capture emission dynamics across heterogeneous economies |
| 3 | Treat the SVR kernel as an optimisable hyperparameter rather than a fixed assumption |
| 4 | Identify which chemical and temporal features drive predictive accuracy across model families |
| 5 | Translate model outputs into a policy-oriented Power BI dashboard for non-technical stakeholders |
| 6 | Quantify how accurately national CO₂ trajectories can be forecasted from historical data alone |

---

## Dataset

| Source | Coverage | Granularity |
|--------|----------|-------------|
| [Global Fossil Fuel Emissions — DataHub](https://opendata.datahub.io/@datopian/global-fossil-fuel-emissions-1751-2010) | 1970–2022 | Annual, national level |

**Scope:** The analysis applies a Pareto filter, focusing on the 10 countries responsible for 80% of global cumulative CO₂ emissions:

| Country | Cumulative CO₂ (tonnes) |
|---------|------------------------|
| United States | 110,566,459 |
| China (Mainland) | 63,354,736 |
| Germany | 21,361,661 |
| United Kingdom | 21,086,112 |
| Japan | 16,504,905 |
| India | 15,256,379 |
| Russian Federation | 13,341,785 |
| France (incl. Monaco) | 10,206,852 |
| Canada | 9,004,370 |
| Poland | 7,436,925 |

---

## ⚙️ Workflow & Techniques

| Phase | Technique | Purpose |
|-------|-----------|---------|
| Data Cleaning | pandas, z-score normalisation | Handle missing values, align scales across countries |
| Feature Engineering | Lag features, rolling stats, growth rates, fuel ratios | Capture temporal autocorrelation and structural emission patterns |
| Dimensionality & EDA | seaborn, matplotlib | Surface distributional bias and country-level heterogeneity |
| ML — Ridge Regression | scikit-learn, L2 regularisation | Linear baseline; interpretable coefficient direction |
| ML — Random Forest | scikit-learn RandomForestRegressor | Non-linear interactions, intrinsic feature importance |
| ML — XGBoost | XGBRegressor | Sequential residual correction; best overall performance |
| ML — Kernel-Tuned SVR | RandomisedSearchCV over linear, poly, sigmoid, RBF | Adaptive kernel selection per country emission dynamics |
| Validation Strategy | Temporal train/val/test split (1970–2010 / 2011–2015 / 2016–2020) | Prevent data leakage, simulate real forecasting conditions |
| Dashboard | Power BI | Translate model outputs into policy-oriented emissions indicators |

---

## Key Results & Insights

### 1. Feature Engineering Drives Predictive Accuracy

Over 30 features were derived from raw variables. Lag features (1–3 years) consistently ranked as the strongest predictors across all models — confirming that emissions exhibit strong autoregressive inertia driven by infrastructure and energy system path dependence.

### 2. Model Performance Comparison

| Model | RMSE | MAE | R² |
|-------|------|-----|----|
| Ridge Regression | 0.1115 | 0.0743 | 0.9579 |
| Random Forest | 0.1240 | 0.0801 | 0.9479 |
| SVR (Kernel-Tuned) | 0.1296 | 0.1037 | 0.9430 |
| **XGBoost** | **0.1333** | **0.9976** | **0.9976** |

**Metric definitions:**
- **R²** — proportion of emission variance explained by the model (higher = better)
- **RMSE** — average prediction error, penalising large deviations extra (lower = better)
- **MAE** — average absolute error, straightforward to interpret (lower = better)

XGBoost achieves the strongest predictive performance overall. Ridge Regression — despite its simplicity — delivers a competitive R² of 0.96, reflecting the strong linear component embedded in long-run national emission trends.

### 3. Kernel Optimisation Improves SVR Generalisation

Treating the SVR kernel as a tunable hyperparameter (rather than defaulting to RBF) produced measurable improvements over fixed-kernel baselines. This allows the model to adapt its functional form to country-specific emission dynamics — particularly relevant for structurally heterogeneous economies like China vs. the UK.

### 4. Dashboard — 80% of Global CO₂: How Many Countries?

The Power BI dashboard centres on a key policy insight: a small number of countries drive the overwhelming majority of global emissions. Key views include:
- Historic emission trends by country and fuel type
- Model forecasts vs actuals (2016–2020 test period)
- Feature importance rankings across model families
- Residual diagnostics for model reliability assessment

> **Power BI Demo:** Coming Soon

---

## 📦 Repository Structure

```
CO2-Emissions-Forecasting-Multi-Model-Analysis/
│
├── CO2_Emissions_Forecasting.ipynb     # Full end-to-end analysis notebook
├── global_fossil_fuel_emissions.csv    # Dataset (source: DataHub)
├── CO2_Dashboard.pbix                  # Power BI dashboard file
└── README.md                           # Project documentation
```

---

## How to Run

1. Clone this repository
2. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost jupyter
```
3. Download the dataset from [DataHub](https://opendata.datahub.io/@datopian/global-fossil-fuel-emissions-1751-2010) if not present
4. Run `CO2_Emissions_Forecasting.ipynb` cell by cell to reproduce the full analysis

---

## References

- [Global Fossil Fuel Emissions Dataset — DataHub](https://opendata.datahub.io/@datopian/global-fossil-fuel-emissions-1751-2010)
- Kumari, S. & Singh, S.K. (2023). Machine learning-based time series models for effective CO₂ emission prediction. *Environmental Science and Pollution Research*, 30(55), 116601–116616.
- Nassef, A.M. et al. (2023). Application of artificial intelligence to predict CO₂ emissions. *Sustainability*, 15(9).

---

## 👨‍💻 Author

**Renato Silva** — Reporting and Data Analyst

[LinkedIn](https://www.linkedin.com/in/renato-silva) | [GitHub](https://github.com/RenatoMateo) | [Power Bi Dashboard](https://app.powerbi.com/groups/me/reports/355128b7-27b2-4b79-a287-8fa7cc425916/c63422a160fba0570cb9?experience=power-bi)

---
