# Revenue-Forecast-Comparison
# Revenue Regression Analysis

This project analyzes the relationship between company revenue and several operational/weather-related variables, then builds and evaluates two simple linear regression models to predict revenue.

## Data

Source file: `AICPA_regressionAnalysisData.csv`

Columns:
- `type` — indicates whether the row belongs to the training set (`dt4training`) or testing set (`dt4testing`)
- `date` — monthly observation date
- `revenue` — monthly revenue
- `production` — a production volume metric
- `coolDD` — cooling degree days
- `heatDD` — heating degree days

The dataset spans monthly observations from January 2011 through December 2014 (48 rows total).

## Workflow

1. **Import & clean up display** — Load the CSV with `pandas` and format floats to avoid scientific notation.
2. **Inspect the raw data** — Display the full dataset to confirm it loaded correctly.
3. **Correlation check** — Compute the correlation matrix between `revenue`, `production`, `coolDD`, and `heatDD` to see which variables are most related to revenue.
4. **Train/test split** — Split the data using the existing `type` column:
   - Training rows: 36
   - Testing rows: 12

## Models

Two ordinary least squares (OLS) models were built using `statsmodels`, each using the training data to predict `revenue` from a single explanatory variable, then evaluated on the testing data using **Mean Absolute Percentage Error (MAPE)**.

### Model 1: Revenue ~ Production
- Fitted on `production` as the sole predictor
- Coefficients: `const ≈ 4,897,663.26`, `production ≈ 18.99`
- **Testing MAPE: 25.42%**
- Training R-squared: 0.397
- p-value (production): 0.000

### Model 2: Revenue ~ coolDD
- Fitted on `coolDD` as the sole predictor
- Coefficients: `const ≈ 14,341,632.04`, `coolDD ≈ -4,113.94`
- **Testing MAPE: 29.60%**
- Training R-squared: 0.017
- p-value (coolDD): 0.448

### Comparison

| Model | MAPE | R-squared (training) | p-value (feature) |
|---|---|---|---|
| Model 1 (production) | 25.42% | 0.397 | 0.000 |
| Model 2 (coolDD) | 29.60% | 0.017 | 0.448 |

## Conclusion

Model 1 (using `production` as the predictor) outperforms Model 2 (using `coolDD`) on both fit and predictive accuracy: it has a much higher training R-squared (0.397 vs. 0.017), a statistically significant coefficient (p = 0.000 vs. p = 0.448), and a lower testing MAPE (25.42% vs. 29.60%). This suggests `production` is a meaningfully stronger predictor of revenue than `coolDD` in this dataset.

## Requirements

- Python 3
- `pandas`
- `numpy`
- `matplotlib`
- `statsmodels`

