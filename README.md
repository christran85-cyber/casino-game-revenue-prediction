# Casino Game Revenue Prediction

## Data Science Module 1 Capstone

This project is an end-to-end regression analysis that explores whether machine, game, location, and operational characteristics can be used to predict monthly gaming revenue.

The project was completed as a Data Science Module 1 capstone using a **synthetic dataset of 2,000 gaming-machine observations**. The workflow includes data validation, cleaning, exploratory data analysis, baseline modeling, model comparison, controlled experimentation, evaluation, and reproducibility testing.

> **Note:** All data used in this project is synthetic and was created for educational purposes. It does not contain real casino, customer, or financial information.

---

## Project Question

**Can machine, game, and location characteristics be used to predict monthly gaming revenue?**

**Stakeholder:** Casino gaming operations management

**Target Variable:** `monthly_revenue`

---

## Dataset

The synthetic dataset contains:

- 2,000 observations
- 16 original columns
- 45 fictional locations
- Machine, game, location, operational, and financial characteristics
- Monthly revenue as the regression target

Initial data validation included:

- Dataset structure and data-type inspection
- Missing-value analysis
- Duplicate-record checks
- Record-grain validation
- Target distribution analysis

Small amounts of missing data were identified in `distance_from_hq_miles`, `avg_bet`, and `payout_rate`. These values were handled using median imputation.

---

## Exploratory Data Analysis

Exploratory analysis was used to examine:

- Monthly revenue distribution
- Average revenue by game type
- Correlations between numeric predictors and revenue
- Relationship between days active and monthly revenue

The analysis showed meaningful variation in revenue across observations and identified several variables with potential predictive value.

---

## Predictive Modeling

Three approaches were evaluated:

1. DummyRegressor baseline
2. Linear Regression
3. Random Forest Regression

All models were evaluated using the same 80/20 train/test methodology.

### Model Results

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 441.34 | 549.06 | ~0.00 |
| Linear Regression | 304.91 | 380.57 | 0.5194 |
| Random Forest | 326.80 | 410.89 | 0.4398 |

Linear Regression produced the strongest results on the held-out test data.

Compared with the baseline, Linear Regression reduced:

- **MAE by approximately 30.9%**
- **RMSE by approximately 30.7%**

Its R² of 0.5194 indicates that the model explained approximately 51.9% of the variation in monthly revenue within the held-out test data.

---

## Controlled Experiment

A controlled experiment tested whether adding `total_net` improved Linear Regression performance.

The same train/test methodology, random seed, encoding process, and regression algorithm were retained while `total_net` was added as an additional predictor.

The reported performance metrics remained unchanged:

- MAE: 304.91
- RMSE: 380.57
- R²: 0.5194

This indicates that `total_net` did not provide measurable additional predictive value at the reported precision. The variable was therefore excluded from the primary model.

---

## Key Findings

- Linear Regression substantially outperformed the baseline.
- Random Forest improved over the baseline but did not outperform Linear Regression on the held-out test set.
- A more complex model did not automatically produce better predictions.
- Adding `total_net` did not measurably improve Linear Regression performance.
- The Actual vs. Predicted analysis showed that some high-revenue observations were underpredicted.
- Model results should be interpreted as predictive relationships rather than evidence of causation.

---

## Limitations

This project uses synthetic educational data, so the results should not be assumed to represent real casino operations.

Model evaluation also used a single 80/20 train/test split. Future analysis could incorporate cross-validation and additional regression approaches.

Prediction timing is another important consideration. Same-month financial variables may not be available if the objective is to forecast revenue before the month begins. A production model would need to use only information available at the actual prediction time.

---

## Reproducibility

A fixed random seed of `42` was used for reproducibility.

After completing the analysis, the Jupyter notebook was restarted from a clean kernel and all cells were successfully executed from beginning to end without errors.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- scikit-learn
- JupyterLab
- Git
- GitHub

---

## Repository Contents

- `casino_game_revenue_prediction.ipynb` — Complete analysis, modeling, evaluation, and documentation
- `casino_game_revenue_revised_with_store_names.csv` — Synthetic dataset used for the project
- `README.md` — Project overview and results

---

## Future Improvements

Future versions of this project could include:

- Cross-validation
- Additional regression models
- Feature engineering
- Investigation of high-error observations
- A clearly defined future forecasting horizon
- Real-world operational data, where appropriate and authorized

---

## Project Status

**Capstone analysis complete.**