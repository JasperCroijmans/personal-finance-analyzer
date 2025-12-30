# Project Structure

## Directory Tree
```
personal-finance-analyzer/
│
├── 📁 data/
│   ├── 📁 raw/                           # Original bank CSV (gitignored)
│   ├── 📁 processed/                     # Cleaned datasets
│   │   ├── transactions_clean.csv
│   │   ├── transactions_with_features.csv
│   │   ├── transactions_categorized.csv
│   │   ├── transactions_with_anomalies.csv
│   │   ├── spending_predictions.csv
│   │   └── detected_anomalies.csv
│   ├── 📁 models/                        # Saved ML models
│   │   ├── category_model.pkl
│   │   ├── category_model_improved.pkl
│   │   ├── tfidf_vectorizer.pkl
│   │   └── categories.pkl
│   └── 📁 powerbi/                       # Power BI data sources
│       ├── transactions_powerbi.csv
│       ├── predictions_powerbi.csv
│       └── summary_stats.csv
│
├── 📁 notebooks/                         # Jupyter analysis notebooks
│   ├── 01_data_loading.ipynb            # Initial data import
│   ├── 02_data_cleaning.ipynb           # Data cleaning & EDA
│   ├── 03_feature_engineering.ipynb     # Feature creation
│   ├── 04_categorization_model.ipynb    # ML categorization
│   ├── 05_model_improvement.ipynb       # Model tuning
│   ├── 06_spending_predictions.ipynb    # Forecast next month
│   ├── 07_anomaly_detection.ipynb       # Detect unusual transactions
│   ├── 08_final_visualizations.ipynb    # Summary dashboards
│   └── 09_powerbi_prep.ipynb            # Power BI prep
│
├── 📁 visualizations/                    # Generated charts
│   ├── 01_initial_analysis.png
│   ├── 02_feature_engineering.png
│   ├── 03_confusion_matrix.png
│   ├── 04_feature_importance.png
│   ├── 05_final_categorization.png
│   ├── 06_spending_trends.png
│   ├── 07_spending_predictions.png
│   ├── 08_anomaly_detection.png
│   ├── 09_executive_dashboard.png
│   ├── 10_time_analysis.png
│   ├── 11_merchant_analysis.png
│   ├── interactive_spending_timeline.html
│   ├── interactive_anomalies.html
│   └── interactive_category_sunburst.html
│
├── 📁 powerbi/                           # Power BI files
│   └── Personal_Finance_Dashboard.pbix
│
├── 📁 docs/                              # Documentation
│   ├── PROJECT_DOCUMENTATION.md
│   ├── PROJECT_STRUCTURE.md
│   └── statistics_report.txt
│
├── 📄 README.md                          # Main project documentation
├── 📄 requirements.txt                   # Python dependencies
├── 📄 .gitignore                         # Git ignore rules
└── 📄 LICENSE (optional)                 # License file
```

## File Descriptions

### Data Files
- **raw/**: Original CSV from bank (not in git)
- **processed/**: Clean, analysis-ready datasets
- **models/**: Trained ML models (pickle files)
- **powerbi/**: Simplified CSVs for Power BI

### Notebooks
- **01-02**: Data loading and cleaning
- **03**: Feature engineering (30+ features)
- **04-05**: ML model training and optimization
- **06**: Spending prediction models
- **07**: Anomaly detection (statistical + ML)
- **08**: Final visualizations and summary
- **09**: Power BI data preparation

### Outputs
- **visualizations/**: 11 PNG images + 3 interactive HTML
- **powerbi/**: Interactive dashboard (.pbix)
- **docs/**: Technical documentation

---

## Data Flow
```
📥 Raw CSV (Bank Export)
    ↓
🧹 Cleaning (02)
    ↓
⚙️ Features (03)
    ↓
🤖 ML Models (04-07)
    ↓
📊 Visualizations (08)
    ↓
💼 Power BI (09-10)
```

---

## Key Outputs

1. **transactions_with_anomalies.csv** (1,638 rows, 50+ columns)
   - Main analysis dataset
   - All features, predictions, and flags

2. **spending_predictions.csv** (10 rows)
   - Next month forecasts per category

3. **Personal_Finance_Dashboard.pbix**
   - Interactive Power BI dashboard
   - 2 pages: Overview + Predictions

4. **11 visualizations** + 3 interactive HTML dashboards

---
