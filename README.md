# National Electricity Consumption Forecasting — EDF Partnership

**Competition:** Kaggle — CentraleSupélec x EDF | **Result:** 1st place among student teams | **Grade:** 19/20

---

## Overview

Forecasting national electricity consumption (Load), solar production, and wind production using real EDF datasets. The competition was run on Kaggle as part of the CentraleSupélec curriculum.

The main takeaway from this project: feature engineering had a much larger impact on RMSE than model selection or hyperparameter tuning. Most of the work went into building and selecting relevant features.

---

## Approach

**1. Model selection** — we tested several models (Linear Regression, Random Forest, XGBoost, LightGBM, CatBoost). Gradient boosting methods worked best; CatBoost was selected for the final submission.

**2. Feature engineering** — the core of the project. We iteratively built 50+ features across three categories:
- Temporal cycles (sine/cosine encoding of time-of-day, month, time-of-year)
- Weather proxies (thermal stress, PV yield, wind density effect, solar index)
- Behavioral indicators (peak hours, weekend, energy crisis of 2022, friday evening)

**3. Feature selection** — via cross-covariance analysis. We tested several approaches before settling on a cross-covariance threshold of 0.15 per target.

**4. Multi-target modeling** — one model per target (Load, Solar, Wind), evaluated separately and combined as: `Balance = Load - Solar - Wind`

---

## Results

| Model | RMSE Balance |
|---|---|
| CatBoost | 2425.1 |
| XGBoost | 2480.2 |
| LightGBM | 2498.8 |
*Evaluated on a 1% local validation split (shuffle=False to preserve time ordering).  

## Result on Kaggle's test dataset:

| Model | RMSE Balance |
|---|---|
| CatBoost | 2173.0 |
---

## Stack

```
pip install numpy pandas scikit-learn seaborn matplotlib xgboost lightgbm catboost
```

---

## Authors

Developed by a team of four CentraleSupélec engineering students — June 2025.

**Félix Marquezy** — [LinkedIn](https://www.linkedin.com/in/félix-marquezy/) · [GitHub](https://github.com/felixmarquezy9-prog)
