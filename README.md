# 🎰 Casino Game Revenue Prediction

## Data Science Module 1 Capstone

![Casino Game Revenue Prediction Project Overview](images/casino_game_revenue_prediction_infographic.png)

This project is an end-to-end regression analysis that explores whether machine, game, location, and operational characteristics can be used to predict monthly gaming revenue.

The project was completed as a **Data Science Module 1 Capstone** using a synthetic dataset containing **2,000 gaming-machine observations**.

The workflow includes:

- Data validation
- Data cleaning
- Exploratory Data Analysis (EDA)
- Baseline modeling
- Linear Regression
- Random Forest Regression
- Model comparison
- Controlled experimentation
- Evaluation
- Reproducibility testing

> **Important:** All data used in this project is synthetic and was created for educational purposes. It does not contain real casino, customer, or financial information.

---

# 🎯 Project Question

**Can machine, game, and location characteristics be used to predict monthly gaming revenue?**

**Stakeholder:** Casino gaming operations management

**Machine Learning Type:** Regression

**Target Variable:** `monthly_revenue`

The purpose of the analysis is to determine whether operational and machine-level characteristics contain enough predictive information to estimate monthly gaming revenue.

---

# 📊 Dataset Overview

The synthetic dataset contains:

| Dataset Characteristic | Value |
|---|---:|
| Observations | 2,000 |
| Original Columns | 16 |
| Fictional Locations | 45 |
| Target | `monthly_revenue` |
| Data Type | Synthetic |
| Observation Period | Monthly |

Each row is treated as an individual monthly gaming-machine observation.

Important variables include:

- `game_type`
- `location_type`
- `distance_from_hq_miles`
- `days_active`
- `avg_bet`
- `payout_rate`
- `total_in`
- `total_out`
- `number_of_services`
- `machine_swapouts`
- `monthly_revenue`

The dataset also contains identifiers such as `machine_id`, `location_id`, and `store_name`.

---

# 🔍 Data Validation

Before modeling, the dataset was inspected for:

- Dataset dimensions
- Data types
- Missing values
- Exact duplicate records
- Repeated machine/location/month combinations
- Target distribution
- Potentially suspicious predictors

## Missing Data

Three columns contained small amounts of missing data:

- `distance_from_hq_miles` — 10 missing values
- `avg_bet` — 14 missing values
- `payout_rate` — 12 missing values

![Missing Data Summary](images/01_missing_data_summary.png)

The missing percentages were small, ranging from approximately **0.5% to 0.7%**.

Rather than removing observations, the missing numeric values were replaced using the **median** of each respective column.

Median imputation was selected because it preserves the observations while being less sensitive to extreme values than the mean.

## Validation After Cleaning

![Missing Values Cleaned](images/02_missing_values_cleaned.png)

After median imputation, all three affected columns contained **zero missing values**.

The dataset was then ready for exploratory analysis and predictive modeling.

---

# 📈 Exploratory Data Analysis

Exploratory Data Analysis was performed to better understand the target variable and relationships between revenue and potential predictors.

The analysis focused on:

1. Distribution of monthly revenue
2. Average revenue by game type
3. Numeric correlations with monthly revenue
4. Relationship between days active and revenue

---

## Monthly Revenue Distribution

![Monthly Revenue Distribution](images/03_monthly_revenue_distribution.png)

Monthly revenue varies substantially across observations.

The distribution contains both negative and positive values, with some observations producing considerably higher revenue than the majority of the dataset.

This variation makes monthly revenue an appropriate continuous target for regression analysis.

---

## Average Monthly Revenue by Game Type

![Average Monthly Revenue by Game Type](images/04_average_revenue_by_game_type.png)

Average monthly revenue differs across game types.

In this synthetic dataset, some game categories show higher average revenue than others.

This suggests that `game_type` may contain useful predictive information. However, these relationships should be interpreted as **associations rather than evidence of causation**.

---

## Correlation Analysis

![Revenue Correlations](images/05_revenue_correlations.png)

Several numeric variables showed meaningful relationships with monthly revenue.

Notable correlations included approximately:

| Variable | Correlation with Monthly Revenue |
|---|---:|
| `days_active` | 0.648 |
| `total_net` | 0.393 |
| `total_in` | 0.382 |
| `total_out` | 0.373 |
| `avg_bet` | 0.147 |
| `payout_rate` | -0.101 |
| `machine_swapouts` | -0.226 |
| `number_of_services` | -0.338 |

`days_active` showed the strongest positive numeric correlation with monthly revenue among the examined predictors.

Correlation alone does not establish causation, and model performance must be evaluated on unseen data.

---

## Monthly Revenue vs. Days Active

![Monthly Revenue vs Days Active](images/06_revenue_vs_days_active.png)

The scatterplot shows a visible positive relationship between the number of days a machine is active and monthly revenue.

Machines operating for more days generally have the opportunity to generate more revenue.

However, substantial variation remains at each number of active days, indicating that additional machine, game, and operational characteristics also contribute to revenue differences.

---

# 🤖 Predictive Modeling

Three predictive approaches were evaluated:

1. **DummyRegressor** — baseline
2. **Linear Regression**
3. **Random Forest Regressor**

The data was divided using an **80/20 train/test split** with a fixed random seed of `42`.

Categorical variables such as `game_type` and `location_type` were converted into numeric representations before model training.

The primary model intentionally excluded `total_net` so that its effect could later be examined in a controlled experiment.

---

# 📏 Evaluation Metrics

Three regression metrics were used:

### Mean Absolute Error (MAE)

MAE measures the average absolute difference between predicted and actual revenue.

**Lower is better.**

### Root Mean Squared Error (RMSE)

RMSE measures prediction error while penalizing larger errors more heavily.

**Lower is better.**

### R² — Coefficient of Determination

R² measures how much of the variation in the target is explained by the model on the evaluated data.

**Higher is generally better.**

---

# 🧪 Baseline Model

A `DummyRegressor` was used as the baseline.

The baseline predicts approximately the mean training revenue for every test observation.

### Baseline Results

| Metric | Result |
|---|---:|
| MAE | 441.34 |
| RMSE | 549.06 |
| R² | ~0.00 |

The baseline establishes a minimum reference point that the predictive models should outperform.

---

# 📐 Linear Regression

Linear Regression was trained using the prepared feature set.

### Linear Regression Results

| Metric | Result |
|---|---:|
| MAE | **304.91** |
| RMSE | **380.57** |
| R² | **0.5194** |

Compared with the baseline, Linear Regression reduced:

- **MAE by approximately 30.9%**
- **RMSE by approximately 30.7%**

An R² of `0.5194` means that the model explained approximately **51.9% of the variation in monthly revenue on the held-out test data**.

It does **not** mean that the model was "51.9% accurate."

---

# 🌲 Random Forest Regression

A Random Forest Regressor was also evaluated.

### Random Forest Results

| Metric | Result |
|---|---:|
| MAE | 326.80 |
| RMSE | 410.89 |
| R² | 0.4398 |

Random Forest substantially outperformed the baseline but did not outperform Linear Regression on this particular held-out test set.

This demonstrates an important machine-learning lesson:

> A more complex model does not automatically produce better predictions.

---

# 🏆 Model Comparison

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Baseline | 441.34 | 549.06 | ~0.00 |
| **Linear Regression** | **304.91** | **380.57** | **0.5194** |
| Random Forest | 326.80 | 410.89 | 0.4398 |

For this analysis, Linear Regression produced the lowest MAE and RMSE and the highest R² of the three evaluated approaches.

---

# 🧬 Controlled Experiment — `total_net`

A controlled experiment was performed to determine whether adding `total_net` improved Linear Regression performance.

The experiment kept the following conditions constant:

- Same dataset
- Same train/test methodology
- Same random seed
- Same categorical encoding process
- Same Linear Regression algorithm

The only intentional change was the addition of:

`total_net`

### Results With `total_net`

| Metric | Without `total_net` | With `total_net` |
|---|---:|---:|
| MAE | 304.91 | 304.91 |
| RMSE | 380.57 | 380.57 |
| R² | 0.5194 | 0.5194 |

At the reported precision, adding `total_net` produced **no measurable improvement**.

Therefore, `total_net` was excluded from the primary model.

The experiment also highlights the importance of considering prediction timing. Same-month financial variables can become problematic predictors if they would not actually be available when a future prediction needs to be made.

---

# 🔎 Key Findings

The analysis produced several important findings:

- Linear Regression substantially outperformed the baseline.
- Random Forest also beat the baseline but did not outperform Linear Regression.
- `days_active` had the strongest positive numeric correlation with monthly revenue among the examined predictors.
- Game type showed meaningful differences in average revenue within the synthetic dataset.
- Operational characteristics such as services and machine swapouts showed relationships with revenue.
- Adding `total_net` did not measurably improve Linear Regression at the reported precision.
- Some high-revenue observations were more difficult for the model to predict.
- Predictive relationships should not be interpreted as proof of causation.

---

# ✅ Evidence and Integrity Checks

Five explicit evidence checks were incorporated into the notebook.

## 1. Data Integrity

The dataset was checked for:

- Missing values
- Exact duplicates
- Repeated identifiers
- Dataset dimensions
- Data types

Repeated `machine_id`, `location_id`, and `month` combinations were investigated rather than automatically deleted.

Inspection showed that these repeated combinations were not identical records. They contained differences in operational characteristics, so the observations were retained.

---

## 2. Transformation Integrity

Missing values were handled using median imputation.

After cleaning, the affected columns were checked again and confirmed to contain zero missing values.

---

## 3. Analytical Integrity

Exploratory relationships were examined before modeling.

Categorical variables were encoded for machine-learning use, while identifiers and the target were excluded from the primary feature set.

---

## 4. Baseline and Conclusion Integrity

Model performance was compared against a simple baseline.

Both machine-learning models outperformed the baseline, while Linear Regression produced the strongest test-set metrics among the evaluated models.

---

## 5. Reproducibility and Failure Check

The notebook uses a fixed random seed of:

`42`

After the analysis was completed, the Jupyter kernel was restarted and **all notebook cells were successfully executed from beginning to end without errors**.

This confirmed that the documented workflow was reproducible in the current project environment.

---

# ⚠️ Limitations

This project has several important limitations.

### Synthetic Data

The dataset is synthetic and intended for educational use. Results should not automatically be generalized to real casino operations.

### Single Train/Test Split

The models were evaluated using one 80/20 split.

Future work should use cross-validation to determine whether performance remains consistent across multiple data partitions.

### Prediction Timing

Some same-month variables may not be available when a real-world revenue forecast is created.

A production model would need a clearly defined prediction point and should use only information available at that time.

### Prediction Errors

Some observations, particularly at higher revenue levels, were more difficult for the model to predict.

Future analysis could investigate these high-error observations.

---

# 🔄 Future Improvements

Future versions of the project could include:

- Cross-validation
- Additional regression algorithms
- Additional feature engineering
- Hyperparameter tuning
- Investigation of high-error observations
- Clearly defined future forecasting horizons
- Additional model diagnostics
- Real-world operational data where appropriate and authorized

A future version could specifically predict **next month's revenue**, using only information that would realistically be available before that month begins.

---

# 🛠️ Technologies Used

- Python 3
- Pandas
- NumPy
- Matplotlib
- scikit-learn
- JupyterLab
- Git
- GitHub

---

# 📁 Repository Structure

```text
casino-game-revenue-prediction/
│
├── README.md
├── casino_game_revenue_prediction.ipynb
├── casino_game_revenue_revised_with_store_names.csv
├── .gitignore
│
└── images/
    ├── casino_game_revenue_prediction_infographic.png
    ├── 01_missing_data_summary.png
    ├── 02_missing_values_cleaned.png
    ├── 03_monthly_revenue_distribution.png
    ├── 04_average_revenue_by_game_type.png
    ├── 05_revenue_correlations.png
    └── 06_revenue_vs_days_active.png
