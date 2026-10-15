# Thai-Agricultural-Export-Forecasting-Time-Series-Forecasting-in-R
Time series forecasting of monthly Thai agricultural export value (2013-2023) in R, comparing Naive, ETS, Holt-Winters, ARIMA and SARIMA with residual diagnostics and 12-month prediction intervals.

# Data 


# Business question
Can monthly agricultural export value be forecast well enough to support planning, and how much uncertainty should a planner expect around the forecast?

# Summary of Findings
- Export value is non-stationary and seasonal. One regular difference (d = 1) makes it stationary; seasonal differencing was not needed.
- ETS had the lowest holdout error (RMSE 10,277; MAPE 5.9%), but its residuals were autocorrelated, so its prediction intervals are not reliable.
- SARIMA(0,1,4)(1,0,0)[12] was the only model whose residuals passed the Ljung-Box test (p = 0.49). It was selected as the final model because its prediction intervals are statistically defensible, at the cost of lower point accuracy on the holdout.

# Results

| Model                         |   RMSE |    MAE | MAPE (%) |
|-------------------------------|-------:|-------:|---------:|
| ETS                           | 10,277 |  8,716 |     5.88 |
| Holt-Winters (additive)       | 10,500 |  8,982 |     6.05 |
| Naive                         | 13,648 | 10,097 |     6.51 |
| Seasonal Naive                | 15,335 | 13,358 |     8.79 |
| ARIMA (non-seasonal)          | 15,852 | 13,567 |     9.57 |
| SARIMA                        | 19,050 | 16,412 |    11.38 |
| Holt-Winters (multiplicative) | 24,985 | 20,881 |    14.16 |

# Residual Diagnostics
Use Ljung-Box to test residuals (residuals should be white-noise for reliable forecast)

| Model                         |             Q* |    p-value | Residuals are white noise?             |
|-------------------------------|----------------:|-----------:|-----------------------------------------|
| **SARIMA**                    |           18.54 | **0.4866** | **Yes**                                 |
| ETS                           |           61.13 |   < 0.0001 | No                                      |
| Holt-Winters (additive)       |           58.22 |     0.0001 | No                                      |
| Holt-Winters (multiplicative) |           55.20 |     0.0003 | No                                      |
| ARIMA (non-seasonal)          |           49.03 |     0.0002 | No                                      |
| Naive / Seasonal Naive        | 139.84 / 280.85 |          ~0 | No (expected for baselines)             |
