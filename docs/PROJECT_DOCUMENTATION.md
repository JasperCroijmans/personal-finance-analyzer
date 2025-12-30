# Project Documentation - Personal Finance Analyzer

## 📊 Data Pipeline Overview
```
Raw CSV (Rabobank)
    ↓
Data Loading & Validation
    ↓
Data Cleaning (dates, amounts, duplicates)
    ↓
Feature Engineering (30+ features)
    ↓
ML Models (Categorization, Predictions, Anomalies)
    ↓
Visualizations (Python + Power BI)
    ↓
Insights & Recommendations
```

---

## 🗂️ Data Schema

### Raw Data (from bank)
- **Source**: Rabobank CSV export
- **Format**: CSV with comma separator, latin-1 encoding
- **Columns**: 26 columns including IBAN, Date, Amount, Counterparty, Descriptions

### Processed Data
**File**: `data/processed/transactions_with_anomalies.csv`

| Column | Type | Description |
|--------|------|-------------|
| Date | datetime | Transaction date |
| Amount | float | Transaction amount (negative = expense) |
| Balance | float | Account balance after transaction |
| Counterparty | string | Merchant/person name |
| Final_Category | string | Assigned category (keyword or ML) |
| Is_Anomaly | int | 1 if flagged as anomaly, 0 otherwise |
| ML_Confidence | float | Model confidence score (0-1) |

---

## 🤖 Machine Learning Models

### 1. Transaction Categorization
**Model**: Random Forest Classifier  
**Purpose**: Automatically categorize transactions  
**Training Data**: Labeled transactions via keyword matching  
**Features**: TF-IDF vectorization of text (Counterparty + Descriptions)  

**Parameters**:
```python
RandomForestClassifier(
    n_estimators=100,
    max_depth=10,
    random_state=42
)
```

**Performance**:
- Accuracy: 72.09%
- Confidence: 82.6% average
- Categories: 16 unique categories

**Saved as**: `data/models/category_model_improved.pkl`

---

### 2. Spending Predictions
**Model**: Linear Regression (per category)  
**Purpose**: Forecast next month spending  
**Features**: Month number (time-based)  
**Training**: Historical monthly aggregated spending  

**Performance**:
- MAE: €[YOUR_MAE] average across categories
- Categories predicted: 10 top spending categories

**Output**: `data/processed/spending_predictions.csv`

---

### 3. Anomaly Detection
**Methods**: 
1. **Statistical (Z-score)**: Transactions > 3 standard deviations
2. **ML (Isolation Forest)**: Pattern-based anomaly detection

**Isolation Forest Parameters**:
```python
IsolationForest(
    contamination=0.05,  # Expect 5% anomalies
    random_state=42,
    n_estimators=100
)
```

**Results**:
- Statistical anomalies: 40
- ML anomalies: 76
- High-confidence (both methods): 40
- Total flagged: 5.0% of transactions

---

## 🎨 Visualizations

### Python Visualizations (11 total)

**Static (matplotlib/seaborn)**:
1. Initial data analysis (4 panels)
2. Feature engineering summary (6 panels)
3. Confusion matrix (categorization)
4. Feature importance
5. Spending trends
6. Spending predictions comparison
7. Anomaly detection (4 panels)
8. Executive dashboard (9 panels)
9. Time-based analysis (4 panels)
10. Merchant analysis (2 panels)

**Interactive (Plotly - HTML)**:
1. `interactive_spending_timeline.html` - Daily spending by category
2. `interactive_anomalies.html` - Scatter plot with anomalies
3. `interactive_category_sunburst.html` - Category breakdown

---

### Power BI Dashboard

**Page 1: Overview**
- 4 KPI Cards (Income, Expenses, Net, Balance)
- Line chart: Balance over time
- Pie chart: Spending by category
- Bar chart: Monthly spending trends
- Bar chart: Top 10 merchants
- Table: Detected anomalies
- Slicers: Date range, Category filter

**Page 2: Predictions**
- Predicted vs Average comparison
- Change percentage by category
- Total predicted amount card
- Detailed predictions table

---

## 📈 Key Features Created

### Date Features (10)
- Year, Month, Month_Name, Day, Day_Name
- Day_of_Week, Week_of_Year, Quarter
- Is_Weekend, Day_Period

### Amount Features (5)
- Is_Income, Is_Expense
- Amount_Abs (absolute value)
- Amount_Category (binned)
- Amount_Log (for ML models)

### Text Features (16 categories via keywords)
- supermarket, restaurant, transport, online
- subscription, health, bar_cafe, clothing
- electronics, fitness, other_shops, rent
- salary, atm, transfer, insurance

### Counterparty Features (2)
- Counterparty_Frequency
- Is_Recurring

### Time-based Features (4)
- Days_Since_Last
- Balance_Change
- Transactions_Per_Day
- Days_From_Start

**Total**: 30+ engineered features

---

## 🔄 Reproducibility

### To reproduce this analysis:

1. **Export bank data** as CSV (1 year recommended)
2. **Place in** `data/raw/transactions.csv`
3. **Run notebooks** in order (01 through 09)
4. **Open Power BI** and load files from `data/powerbi/`

### Customization Points:
- **Keywords** in `03_feature_engineering.ipynb` - adjust to your spending patterns
- **Categories** - add/remove as needed
- **Prediction timeframe** - change from monthly to weekly/quarterly
- **Anomaly threshold** - adjust contamination parameter

---

## ⚠️ Important Notes

### Data Privacy
- Raw transaction data is **not** committed to GitHub (in `.gitignore`)
- Only processed, anonymized data can be shared
- Never commit files containing IBANs or personal details

### Limitations
- Model trained on personal spending patterns (not generalizable)
- Predictions assume stable spending behavior
- Works best with 6+ months of historical data
- Category keywords are Netherlands-specific

### Known Issues
- Some merchants have inconsistent naming (e.g., "ALBERT HEIJN 1382" vs "AH 3245")
- Transfers between own accounts can skew income/expense calculations
- Large one-time purchases affect predictions

---

## 🔧 Troubleshooting

### Common Issues:

**Problem**: CSV encoding errors  
**Solution**: Use `encoding='latin-1'` when loading Dutch bank CSVs

**Problem**: Date parsing fails  
**Solution**: Specify format: `pd.to_datetime(df['Date'], format='%Y-%m-%d')`

**Problem**: Power BI shows wrong numbers  
**Solution**: Ensure CSV uses period (.) as decimal separator, not comma (,)

**Problem**: Model accuracy too low  
**Solution**: Add more keywords or manually label more training examples

---

## 📚 References

- **scikit-learn documentation**: https://scikit-learn.org/
- **Pandas documentation**: https://pandas.pydata.org/
- **Plotly documentation**: https://plotly.com/python/
- **Power BI documentation**: https://docs.microsoft.com/power-bi/

---



