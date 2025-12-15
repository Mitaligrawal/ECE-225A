Global Food Security Analysis and Prediction

This project aims to analyze key factors that influencing global food security under climate induced supply chain disruptions, integration environmental, trade, socioeconomic variables to identify main drivers using datasets from kaggle and predict future risk hotspots, we do it by analyzying data country wise and then build a prediction machine , where with given values of supply chain disruption, socioeconomic factor , climate stress it can tell you what ranking it has inturn telling if its a hotspot or not

Project Overview

This project uses a **Random Forest Regressor** to predict global food security rankings by integrating three critical dimensions:

1. **Climate Stress Analysis** - Environmental impact on food production
2. **Socio-Economic Factors (FSECI)** - Economic capacity to maintain food access
3. **Supply Chain Performance (LPI)** - Logistics and distribution efficiency

Key Features

- **Multi-dimensional Analysis**: Combines climate, economic, and logistics data
- **Custom FSECI Index**: Food Security Economic Capacity Index with 4 sub-components
- **Machine Learning Model**: Random Forest with 100 estimators for robust predictions
- **Comprehensive Visualizations**: Interactive plots and correlation matrices
- **Country-level Insights**: 82+ countries analyzed with detailed metrics

---

Project Structure

```
ECE-225A/
├── model.ipynb                                    # Main prediction model
├── predictions.csv                                # Model output
├── analyzed_climate_stress_by_country.csv        # Processed climate data
├── analyzed_food_security_by_country.csv         # Food security rankings
├── analyzed_FSECI_by_country.csv                 # Economic capacity scores
├── analyzedLPI_by_country.csv                    # Supply chain performance
│
├── analysis/
│   ├── climate_stress_analysis.ipynb             # Climate impact analysis
│   ├── socio_economic_factors.ipynb              # FSECI calculation
│   ├── supply_chain.ipynb                        # LPI data processing
│   ├── climate_stress_by_country.csv
│   ├── FSECI_SocioEconomic_Indicator.csv
│   ├── Global_Food_Security_Index.csv
│   └── LPI_by_country.csv
│
└── datasets/
    ├── climate-stress/
    │   └── climate_change_dataset.csv
    ├── socio-economic/
    │   └── AnnualValue.csv
    └── supply_chain_disruptions/
        └── International_LPI.xlsx
```

---

 Methodology

### 1. Data Processing Pipeline

#### Climate Stress Index
- **Source**: [climate_stress_analysis.ipynb](analysis/climate_stress_analysis.ipynb)
- **Output**: [analyzed_climate_stress_by_country.csv](analyzed_climate_stress_by_country.csv)
- **Metrics**: Temperature anomalies, precipitation changes, extreme weather events
- **Range**: 0.45 - 0.55 (normalized stress score)

FSECI (Food Security Economic Capacity Index)
- **Source**: [socio_economic_factors.ipynb](analysis/socio_economic_factors.ipynb)
- **Output**: [analyzed_FSECI_by_country.csv](analyzed_FSECI_by_country.csv)
- **Components**:
  - **Purchasing Power Score**: Economic capacity to buy food
  - **Stability Score**: Financial system resilience
  - **Food Independence Score**: Domestic production capability
  - **Crisis Resilience Score**: Ability to withstand shocks
- **Range**: 41.7 - 64.0 (composite vulnerability score)
- **Categories**: Critical (0-25), High (25-50), Moderate (50-75), Low (75-100)

LPI (Logistics Performance Index)
- **Source**: [supply_chain.ipynb](analysis/supply_chain.ipynb)
- **Output**: [analyzedLPI_by_country.csv](analyzedLPI_by_country.csv)
- **Metrics**: Customs efficiency, infrastructure quality, shipment tracking
- **Range**: 1.9 - 4.3 (World Bank score)



**Training Configuration**:
- Train/Test Split: 80/20
- Feature Set: [`LPI Score`, `FSECI`, `Climate Stress Index`]

---

Model Performance

Metrics (from [model.ipynb](model.ipynb))

| Metric | Training Set | Test Set |
|--------|-------------|----------|
| **R² Score** | ~0.95+ | ~0.85+ |
| **RMSE** | ~5-8 ranks | ~10-15 ranks |
| **MAE** | ~4-6 ranks | ~8-12 ranks |

### Feature Importance

Based on the Random Forest feature importance analysis:

1. **LPI Score**: ~40-50% (Strongest predictor)
2. **FSECI**: ~30-40% (Economic resilience)
3. **Climate Stress Index**: ~10-20% (Environmental pressure)

**Correlation Matrix**: Saved as `correlation_matrix.png` showing relationships between all variables.



### Output Files

After running [model.ipynb](model.ipynb), you'll generate:

1. **predictions.csv**: Country-wise predictions with actual vs predicted ranks
2. **rf_model_results.png**: 4-panel visualization showing:
   - Feature importance bar chart
   - Actual vs Predicted scatter plot
   - Residual analysis
   - Error distribution histogram
3. **correlation_matrix.png**: Heatmap of feature correlations

---

Key Insights

Global Food Security Patterns

- **Top Performers**: Countries with high LPI scores (>4.0) and low climate stress
- **Vulnerable Nations**: Low FSECI (<50) combined with high climate stress (>0.52)
- **Critical Finding**: Supply chain efficiency (LPI) is the strongest predictor of food security rankings

FSECI Vulnerability Categories

From [FSECI_SocioEconomic_Indicator.csv](analysis/FSECI_SocioEconomic_Indicator.csv):
- **Critical**: FSECI 0-25 (immediate intervention needed)
- **High**: FSECI 25-50 (high vulnerability)
- **Moderate**: FSECI 50-75 (manageable risk)
- **Low**: FSECI 75-100 (strong economic buffers)

---

Understanding the Data

### Input Features Explained

**LPI Score (Logistics Performance Index)**:
- Measures supply chain efficiency and infrastructure quality
- Higher scores = better food distribution capability
- Data source: World Bank International LPI

**FSECI (Food Security Economic Capacity Index)**:
- Custom composite indicator developed in this project
- Measures economic resilience to food price shocks
- Calculated from purchasing power, trade balance, and production data

**Climate Stress Index**:
- Normalized score of climate change impacts on agriculture
- Accounts for temperature, precipitation, and extreme weather
- Higher values = greater environmental pressure

### Target Variable

**Rank**: Global Food Security Index ranking (1 = best, 113 = worst)
- Source: [Global_Food_Security_Index.csv](analysis/Global_Food_Security_Index.csv)

