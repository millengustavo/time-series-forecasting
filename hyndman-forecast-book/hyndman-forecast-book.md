# Forecasting: Principles and Practice
Authors: Rob J Hyndman and George Athanasopoulos

![book-cover](https://images-na.ssl-images-amazon.com/images/I/51zRKFL9jbL._SX346_BO1,204,203,200_.jpg)

[Available for free here (online)](https://otexts.com/fpp2)

# 1. Getting Started
> Forecasting is difficult. Businesses that do it well have a big advantage over those whose forecasts fail

- Important aid to effective and efficient planning

predictability:
- how well we understand the factors
- how much data we have
- our forecasts affect the thing?

> **Naïve method**: using the most recent observation as a forecast

### Qualitative x Quantitative forecasting
- **qualitative**: no data available
- **quantitative**: numerical info about the past is available; reasonable to assume that some aspects of the past will continue in the future

> *Explanatory models* / mixed models / dynamic regression models / longitudinal models / transfer function models / linear system models: incorporates information about other vars rather than only historical values of the variable to forecast

Drawbacks of explanatory models:
- system may not be understood
- necessary to know/forecast the future values of various predictors
- main concern may be only to predict what, not why
- time series model may give more accurate forecasts

### Basic steps of a forecasting task
1. Problem definition
2. Gathering information
3. Preliminary (exploratory) analysis
4. Choosing and fitting models
5. Using and evaluating a forecasting model

# 2. Time series graphics

Graphs enable:
- patterns
- unusual observations
- changes over time
- relationships between vars

> **Time plot**: observations against time of observation

- **trend**: long-term increase/decrease in the data
- **seasonal**: always of a fixed and known frequency (factors: time of the year and/or day of the week)
- **cyclic**: rises/falls that are not of a fixed frequency

### Correlation
Ranges between -1 and 1

Correlation coefficient only measures the strenght of the *linear* relationship

> Scatterplot matrix: relationships between all pairs of variables

### Autocorrelation Function (ACF)
Measures the relationship between *lagged* values of a time series

> **Correlogram**: autocorrelation coefficients plot

Data with trend, ACs for small lags -> large and positive because observations nearby in time are also nearby in size. So the ACF of trended time series -> positive values that slowly decrease as the lags increase.

Data seasonal, the ACs will be larger for the seasonal lags (at multiples of the seasonal frequency) than for other lags.

Data are both trended and seasonal -> combination of these effects

> **White noise**: time series that show no autocorrelation. 95% of the spikes in the ACF lie within `+-2/sqrt(T)` where `T` is the length of the time series

# 3. The forecaster's toolbox

### Simple methods (benchmarks mostly)
- **Average method**: future values are equal to the average (or "mean")
- **Naïve method**: equal to the value of the last observation -> optimal when data follow a random walk = **random walk forecasts**
- **Seasonal naïve method**: equal to the last observed value from the same season of the year
- **Drift method**: drawing a line between the first and last observations, and extrapolating it into the future

Any forecasting methods we develop will be compared to these simple methods -> test if it is worth considering

### Transformations and adjustments
Adjusting the data can lead to simpler forecasting task

- **Calendar adjustments**: e.g., removing variation of days between months (use average per day instead of monthly)
- **Population adjustments**: data affected by population changes, it is best to use per-capita data rather than the totals
- **Inflation adjustments**: data affected by the value of money are best adjusted before modelling (price indexes, Consumer Price Index - CPI)
- **Mathematical transformations**: data show variation that increases/decreases with the level of the series, math transf. can be useful. e.g., log transformation (interpretable), power transformations, *Box-Cox transformations*. Often no transformation is needed. Transformations sometimes make little difference to the forecasts but have a large effect on prediction intervals

### Residuals
What is left over after fitting a model
- Residuals are uncorrelated. Or there is information left in the residuals -> should be used in computing forecasts
- Residuals have zero mean. Or the forecasts are biases. (easy to fix)
- Residuals have constant variance
- Residuals are normally distributed

> **Portmanteau test**: test for a group of autocorrelations. e.g., *Box-Pierce test*, *Ljung-Box test*

### Training and Test sets
**Size of the test set (hold-out set or out-of-sample data)**: about 20% of the total sample. Ideally be at least as large as the maximum forecast horizon required
- residuals are calculated in the training set
- forecast errors are calculated in the test set

**Forecast errors**
- **Scale-dependent errors**: forecast errors are on the same scale as the data. e.g., MAE, RMSE.
- **Percentage errors**: unit-free, freq. used to compare forecast performance between data sets. e.g., MAPE (mean absolute percentage error), sMAPE (not recommended by Hyndman)
- **Scaled errors**: scale the errors based on the training MAE -> MASE (mean absolute scaled error)

### Time series cross-validation
Series of test sets, each consisting of a single observation. Corresponding training set consists only of observations that occurred *prior* to the observation that forms the test set -> forecast accuracy computed by avg over the test sets -> "evaluation on a rolling forecasting origin"

> A good way to choose the best forecasting model is to find the model with the smallest RMSE computed using time series cross-validation.

### Prediction intervals
- **One-step**: stdev of the forecast distribution ~= stdev of the residuals
- **Multi-step**: intervals increase in length as the forecast horizon increases 
- From **bootstrapped residuals**: when a normal distribution for the forecast errors is an unreasonable assumption -> use bootstrapping (only assume errors are uncorrelated)
- With **transformations**: should be computed on the transformed scale

# 4. Judgemental forecasts
# 5. Time series regression models
# 6. Time series decomposition
# 7. Exponential smoothing
# 8. ARIMA models
# 9. Dynamic regression models
# 10. Forecasting hierarchical or grouped time series
# 11. Advanced forecasting methods
# 12. Some practical forecasting issues
