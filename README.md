# Thai-Agricultural-Export-Forecasting-Time-Series-Forecasting-in-R
Time series forecasting of monthly Thai agricultural export value (2013-2023) in R, comparing Naive, ETS, Holt-Winters, ARIMA and SARIMA with residual diagnostics and 12-month prediction intervals.

# Data 


# Business question
Can monthly agricultural export value be forecast well enough to support planning, and how much uncertainty should a planner expect around the forecast?

# Summary of Findings
- Export value is non-stationary and seasonal. One regular difference (d = 1) makes it stationary; seasonal differencing was not needed.
- ETS had the lowest holdout error (RMSE 10,277; MAPE 5.9%), but its residuals were autocorrelated, so its prediction intervals are not reliable.
- SARIMA(0,1,4)(1,0,0)[12] was the only model whose residuals passed the Ljung-Box test (p = 0.49). It was selected as the final model because its prediction intervals are statistically defensible, at the cost of lower point accuracy on the holdout.

