#   Prediction Report - Equipment Energy Consumption

This report details the approach, modeling, evaluation, and recommendations for predicting and potentially reducing equipment energy consumption.

##   Approach to the Problem

The following steps were taken to address the energy consumption prediction problem:

###   Data Preprocessing Approaches

1.  **Handling Missing Values:**
    * Imputed missing numerical values with mean/median. [cite: 1]
    * Filled categorical missing values with the most frequent category. [cite: 2]
    * Dropped rows/columns with excessive missing data. [cite: 3]

2.  **Converting Columns to Correct Data Types:**
    * Converted timestamps to datetime. [cite: 3]
    * Encoded categorical variables (Label Encoding / One-Hot Encoding). [cite: 3]

3.  **Dealing with Outliers:**
    * Identified outliers using box plots and statistical thresholds. [cite: 4]
    * Removed or capped extreme values. [cite: 4]
    * Applied log transformation for normalization. [cite: 4]

4.  **Feature Scaling:**
    * Applied StandardScaler or MinMaxScaler for normalization. [cite: 5]
    * Ensured uniform feature importance and model stability. [cite: 5]

###   Feature Engineering Approaches

5.  **Time-Based Feature Extraction:**
    * Extracted hour, day of week, and month from the timestamp. [cite: 6]

6.  **Correlation-Based Feature Selection:**
    * Identified and selected features highly correlated with the target. [cite: 7]

7.  **SHAP-Based Feature Importance (Post-modeling):**
    * Used SHAP values to interpret the model and rank top contributing features. [cite: 8]

###   Modeling & Evaluation Approaches

8.  **Grid Search for Hyperparameter Tuning:**
    * Tuned models like XGBoost using GridSearchCV with different combinations of parameters. [cite: 9]

9.  **Model Evaluation:**
    * Compared models using cross-validation scores. [cite: 10]
    * Visualized results using heatmaps and bar charts. [cite: 10]

10. **Interpretability & Recommendations:**
    * Generated insights using SHAP. [cite: 11]
    * Made recommendations based on top influential features. [cite: 11, 12]
    * Identified peak usage hours for load shifting strategies. [cite: 12]

##   Key Insights from the Data:

* **Target Variable Distribution:** `equipment_energy_consumption` is concentrated around zero with less frequent large positive/negative values, indicating mostly low consumption with occasional spikes. [cite: 13]
* **Feature Importance:** `energy_roll_mean_3h` is the most influential predictor, followed by `hour`, `energy_lag_1`, and `energy_lag_3`. [cite: 14]
* **Temporal Patterns:** Energy consumption peaks around 18:00, highlighting a period of high demand in Indore, Madhya Pradesh, India. [cite: 15]
* **Zone Characteristics:** Average humidity is highest in `zone6_humidity`, and average temperature is highest in `zone3_temperature`. [cite: 16]
* **Missing Values:** Significant missing data exists in temperature and humidity readings for several zones. [cite: 17]
* **Outliers:** Outliers are present in `equipment_energy_consumption`, `lighting_energy`, `outdoor_temperature`, and `atmospheric_pressure`. [cite: 18]
* **Correlations:** A strong positive correlation exists between `equipment_energy_consumption` and `lighting_energy`. [cite: 18]
* `timestamp` needs a datetime conversion. [cite: 19]
* `random_variable1` and `random_variable2` have low predictive importance. [cite: 20]
* Limited Impact of Zone Environmental Factors. [cite: 21]
* Potential for Load Shifting Benefits. [cite: 22]
* Need for Further Investigation of Outliers. [cite: 23]

##   Model Performance Evaluation Observations:

|   Model             |   RMSE   |   MAE    |   $R^{2}$   |
| :------------------ | :------- | :------- | :---------- |
|   Linear Regression   |   28.02  |   18.13  |   0.617     |
|   Random Forest       |   24.18  |   14.27  |   0.715     |
|   XGBoost             |   24.4   |   14.51  |   0.71      |
|   LightGBM            |   24.19  |   14.49  |   0.714     |

|   Model       |   colsample\_bytree   |   learning\_rate   |   max\_depth   |   n\_estimators   |   subsample   |   num\_leaves   |
| :---------- | :------------------ | :---------------- | :------------ | :---------------- | :---------- | :------------ |
|   XGBoost     |   0.8               |   0.1             |   6           |   100             |   1         |   N/A         |
|   LightGBM    |   N/A               |   0.1             |   -1          |   100             |   N/A       |   31          |

|   Tuned Model     |   RMSE   |   MAE    |   $R^{2}$   |
| :-------------- | :------- | :------- | :---------- |
|   Tuned XGBoost   |   24.38  |   14.61  |   0.71      |
|   Tuned LightGBM  |   24.29  |   14.57  |   0.712     |

**Key Observations:**

* Tree-based models (Random Forest, XGBoost, LightGBM) significantly outperform Linear Regression in predicting energy consumption. [cite: 28]
* The initial performance of Random Forest and LightGBM is slightly better than XGBoost. [cite: 28]
* Hyperparameter tuning provided a marginal improvement for LightGBM. [cite: 29]
* $R^{2}$ values around 0.71 indicate a reasonable predictive capability of the models. [cite: 29]

##   Recommendations for Reducing Equipment Energy Consumption

Based on the model interpretation, the following recommendations are made to potentially reduce equipment energy consumption:

1.  **Optimize energy\_roll\_mean\_3h Control Systems:** Manage operational factors influencing this key predictor to smooth energy usage. [cite: 30]
2.  **Monitor Hours During Peak Hours (Around 18:00):** Analyze and manage energy use during peak demand periods. [cite: 31]
3.  **Maintain energy\_lag\_1 Within Optimal Ranges:** Control factors leading to high past energy consumption. [cite: 32]
4.  **Consider Load Shifting:** Reschedule non-critical energy use away from the 18:00 peak. [cite: 33]


