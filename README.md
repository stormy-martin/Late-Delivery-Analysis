# Late Delivery Analysis (WGU Data Analytics Capstone)

What drives late deliveries for an e-commerce shipping company? This analysis uses 10,999 shipment records, 59.67% of which arrived late, to test which factors are associated with lateness and how well they predict it.

## Questions
1. Is product importance associated with late delivery?
2. Which factors (discount offered, package weight, product importance) predict whether a shipment arrives late?

## Data quality
- Checked structure, data types, missing values (none), and duplicate rows (none) before analysis
- Verified the target coding: in `Reached.on.Time_Y.N`, **1 means late** and 0 means on time, the reverse of what the column name suggests

## Methods and results
**Chi-square test of independence (product importance vs. late delivery)**
- χ² = 12.21 (df = 2), p = 0.00223: the association is statistically significant
- Cramér's V = 0.0333: the effect is negligible in practical terms
- High-importance shipments were late most often (65.0%, vs. 59.3% for low and 59.0% for medium)

**Binary logistic regression (discount offered, weight, product importance)**
- All predictors significant (p < .001); pseudo R² = 0.1845
- **Discount size was the strongest predictor:** a 10-unit increase in discount raised the odds of a late delivery by a factor of 3.24
- Heavier packages were *less* likely to be late
- Multicollinearity check: all VIFs below 5

**Model evaluation**
| Metric | Value |
|---|---|
| Accuracy | 63.4% (vs. 59.67% baseline of predicting "late" for every shipment) |
| Precision | 0.698 |
| Recall | 0.682 |
| ROC-AUC | 0.717 |

## Business takeaway
Accuracy alone is misleading here, because always predicting "late" already scores 59.67%. The useful question is the tradeoff between false alarms (flagging on-time shipments as late) and missed late shipments. Where to set the classification threshold is a business decision based on what each kind of error costs.

## Data
E-commerce shipping dataset (`Train.csv`, 10,999 rows), available on Kaggle: [Customer Analytics / E-Commerce Shipping Data](https://www.kaggle.com/datasets/prachi13/customer-analytics). Download `Train.csv` into this folder to rerun the notebook.

## Tools
Python · pandas · NumPy · statsmodels · SciPy · scikit-learn · Matplotlib · Jupyter
