# Prediction Report - Equipment Energy Consumption

This report details the approach, modeling, evaluation, and recommendations for predicting and potentially reducing equipment energy consumption.

## Approach to the Problem

The following steps were taken to address the energy consumption prediction problem:

### Data Preprocessing Approaches

1.  **Handling Missing Values:**
    * Numerical missing values were imputed using the mean or median.
    * Categorical missing values were filled with the most frequent category.
    * Rows or columns with excessive missing data were dropped.

2.  **Converting Columns to Correct Data Types:**
    * Timestamps were converted to the datetime format.
    * Categorical variables were encoded using Label Encoding or One-Hot Encoding.

3.  **Dealing with Outliers:**
    * Outliers were identified using box plots and statistical thresholds.
    * Extreme values were either removed or capped.
    * Log transformation was applied for normalization where appropriate.

4.  **Feature Scaling:**
    * StandardScaler or MinMaxScaler was applied for normalization to ensure uniform feature importance and model stability.

### Feature Engineering Approaches

5.  **Time-Based Feature Extraction:**
    * Hour, day of the week, and month were extracted from the timestamp data.

6.  **Correlation-Based Feature Selection:**
    * Features highly correlated with the target variable (energy consumption) were identified and selected.

7.  **SHAP-Based Feature Importance (Post-modeling):**
    * SHAP values were used to interpret the model and rank the top contributing features after model training.

### Modeling & Evaluation Approaches

8.  **Grid Search for Hyperparameter Tuning:**
    * Models like XGBoost were tuned using GridSearchCV with various combinations of parameters.

9.  **Model Evaluation:**
    * Models were compared using cross-validation scores.
    * Results were visualized using heatmaps and bar charts.

10. **Interpretability & Recommendations:**
    * Insights were generated using SHAP values.
    * Recommendations were formulated based on the top influencing factors.

## Model Performance Evaluation Observations:

| Model             | RMSE  | MAE   | $R^{2}$ |
| ----------------- | ----- | ----- | ------- |
| Linear Regression | 28.02 | 18.13 | 0.617   |
| Random Forest     | 24.18 | 14.27 | 0.715   |
| XGBoost           | 24.4  | 14.51 | 0.71    |
| LightGBM          | 24.19 | 14.49 | 0.714   |

| Tuned Model      | RMSE  | MAE   | $R^{2}$ |
| ---------------- | ----- | ----- | ------- |
| Tuned XGBoost    | 24.38 | 14.61 | 0.71    |
| Tuned LightGBM   | 24.29 | 14.57 | 0.712   |

| Model      | colsample\_bytree | learning\_rate | max\_depth | n\_estimators | subsample | num\_leaves |
| ---------- | ----------------- | -------------- | ---------- | ------------- | --------- | ----------- |
| XGBoost    | 0.8               | 0.1            | 6          | 100           | 1         | N/A         |
| LightGBM   | N/A               | 0.1            | -1         | 100           | N/A       | 31          |

**Key Observations:**

* Tree-based models (Random Forest, XGBoost, LightGBM) significantly outperform Linear Regression in predicting energy consumption.
* The initial performance of Random Forest and LightGBM is slightly better than XGBoost.
* Hyperparameter tuning provided a marginal improvement for LightGBM.
* $R^{2}$ values around 0.71 indicate a reasonable predictive capability of the models.

## Recommendations for Reducing Equipment Energy Consumption

Based on the model interpretation, the following recommendations are made to potentially reduce equipment energy consumption:

1.  **Optimize energy\_roll\_mean\_3h Control Systems:** Carefully manage operational factors that influence this key predictor to achieve smoother energy usage patterns.
2.  **Monitor Hours During Peak Hours (Around 18:00):** Analyze and manage energy consumption specifically during peak demand periods, which appear to be around 6 PM.
3.  **Maintain energy\_lag\_1 Within Optimal Ranges:** Control factors that contribute to high past energy consumption (energy\_lag\_1).
4.  **Consider Load Shifting:** Explore the possibility of rescheduling non-critical energy-consuming activities away from the 18:00 peak to reduce strain and potentially lower overall consumption.

