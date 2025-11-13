# Cement Demand Forecasting Across Multiple Sites

## Project Overview
This project implements a machine learning solution for forecasting cement demand across multiple construction sites. The system analyzes historical operational data, weather patterns, and site characteristics to predict future cement consumption and optimize inventory management.

## Business Problem
Construction sites face challenges in cement inventory management due to:
- Variable demand patterns across different sites
- Weather-dependent construction activities
- Different site behaviors (aggressive vs conservative)
- Storage capacity constraints
- Cost implications of stockouts vs excess inventory

## Dataset Description
The project uses a SQLite database (`MIG_Cement_Records.db`) containing three main tables:

### Sites Table
- `site_id`: Unique site identifier
- `region`: Geographic region (North, South, East)
- `silo_capacity`: Storage capacity in tonnes
- `behavior`: Site ordering behavior (aggressive, conservative)

### CementTypes Table
- `cement_type`: Type of cement (CEM_I, CEM_II, CEM_III)

### Operations Table
- `date`: Transaction date
- `site_id`: Site identifier
- `cement_type`: Type of cement used
- `planned_pour_tonnes`: Planned cement usage
- `consumed_tonnes`: Actual cement consumption
- `opening_inventory_tonnes`: Starting inventory
- `deliveries_tonnes`: Cement deliveries received
- `closing_inventory_tonnes`: Ending inventory
- `rain_mm`: Daily rainfall
- `avg_temp_c`: Average temperature
- `silo_capacity`: Site storage capacity

## Key Features
- **Multi-site Analysis**: Forecasting across different geographic regions
- **Weather Integration**: Incorporates rainfall and temperature data
- **Behavioral Patterns**: Accounts for site-specific ordering behaviors
- **Inventory Optimization**: Balances demand forecasting with storage constraints
- **Performance Tracking**: Model evaluation and KPI monitoring

## Project Structure
```
Cement_Demand_Forecasting_Across_Multiple_Sites/
├── Cement_Demand_Forecasting.ipynb    # Main analysis notebook
├── MIG_Cement_Records.db              # SQLite database
├── requirements.txt                   # Python dependencies
├── cement_forecast_results.parquet    # Forecast outputs
├── Model_performance_summary.csv      # Model evaluation metrics
├── historical_kpi_summary.csv         # Historical KPI analysis
├── feature_importance_dt.png          # Feature importance visualization
├── run_app.bat                        # Application launcher
└── anaconda_projects/                 # Project environment
```

## Technical Implementation

### Data Processing
1. **Data Ingestion**: SQLite database connection and table exploration
2. **Data Integration**: JOIN operations combining operational and site data
3. **Feature Engineering**: Creating time-based and derived features
4. **Data Cleaning**: Handling missing values and outliers

### Machine Learning Pipeline
- **Algorithms**: Decision Trees, Time Series models (ARIMA)
- **Features**: Historical consumption, weather data, site characteristics
- **Target Variable**: Future cement demand (consumed_tonnes)
- **Validation**: Time-series cross-validation for temporal data

### Key Metrics
- **Forecast Accuracy**: MAPE, RMSE, MAE
- **Inventory KPIs**: Stockout frequency, excess inventory costs
- **Operational Metrics**: Delivery optimization, capacity utilization

## Installation & Setup

### Prerequisites
- Python 3.8+
- Jupyter Notebook
- SQLite3

### Dependencies
```bash
pip install -r requirements.txt
```

Key packages:
- pandas
- sqlite3
- scikit-learn
- matplotlib
- seaborn
- numpy

### Running the Project
1. Clone the repository
2. Install dependencies: `pip install -r requirements.txt`
3. Open Jupyter Notebook: `jupyter notebook Cement_Demand_Forecasting.ipynb`
4. Run all cells to execute the complete pipeline

## Usage

### Data Exploration
```python
import sqlite3
import pandas as pd

# Connect to database
conn = sqlite3.connect("MIG_Cement_Records.db")

# Load and explore data
query = """
SELECT o.*, s.region, s.behavior 
FROM Operations o 
JOIN Sites s ON o.site_id = s.site_id
"""
df = pd.read_sql_query(query, conn)
```

### Model Training
The notebook includes complete pipeline for:
- Feature engineering
- Model selection and training
- Hyperparameter tuning
- Performance evaluation

### Forecasting
Generate predictions for future cement demand across all sites with confidence intervals and inventory recommendations.

## Results & Insights

### Model Performance
- Achieved forecast accuracy metrics stored in `Model_performance_summary.csv`
- Feature importance analysis shows weather and historical consumption as key predictors
- Site behavior patterns significantly impact demand variability

### Business Impact
- Optimized inventory levels across sites
- Reduced stockout incidents
- Improved delivery scheduling
- Enhanced capacity utilization

## File Descriptions

| File | Description |
|------|-------------|
| `Cement_Demand_Forecasting.ipynb` | Main analysis notebook with complete ML pipeline |
| `MIG_Cement_Records.db` | SQLite database with historical operational data |
| `cement_forecast_results.parquet` | Generated forecasts and predictions |
| `Model_performance_summary.csv` | Model evaluation metrics and performance |
| `historical_kpi_summary.csv` | Historical KPI analysis and trends |
| `feature_importance_dt.png` | Visualization of feature importance |
| `requirements.txt` | Python package dependencies |

## Future Enhancements
- Real-time data integration
- Advanced time series models (LSTM, Prophet)
- Multi-step ahead forecasting
- Automated model retraining
- Dashboard development for stakeholders
- Integration with ERP systems