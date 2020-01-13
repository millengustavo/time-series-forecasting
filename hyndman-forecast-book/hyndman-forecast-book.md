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
Used when:
- no available data
- data available, statistical forecasts are generated, and these are then adjusted used judgement
- data available, statistical and judgmental forecasts are generated independently and then combined

Accuracy of judmental forecasting (lack of historical data) increases when the forecaster has:
- important domain knowledge
- more timely, up-to-date information

JF is subjective and comes with limitations. But implementing systematic and well-structured approachs can confine these limitations and markedly improve forecast accuracy

## Limitations
- Subjective
- Can be inconsistent
- Depends heavily on human cognition (be aware of the multiple cognitive biases)
- Anchoring effect -> subsequent forecasts tend to converge or be close to an inital familiar reference point (create systematic bias)

## Key principles
- Set the forecasting task clearly and concisely (avoid emotive terms and irrelevant information)
- Implement a systematic approach
- Document and justify (accountability -> reduces bias)
- Systematically evaluate forecasts
- Segregate forecasters and users

## The Delphi method
Forecasts from a group are generally more accurate than those from individuals -> construct consensus forecasts from a group of experts in a structured iterative manner

## Forecasting by analogy
Thinking and discussing analogous products or situations can generate useful information (e.g., market value of a house by comparing it to similar properties sold in the area)

## Scenario forecasting
Generate forecasts based on plausible scenarios (e.g.: "best", "middle", "worst")

## New product forecasting
- Sales force composite: aggregate forecast for each outlet/branch/store of a company generated by salespeople
- Executive opinion (remember accountability!)
- Customer intentions: questionnaires, beware of varying correlation between intention and behaviour

## Judgemental adjustments
- Use adjustments sparingly
- Apply a structure approach

# 5. Time series regression models
Forecast the time series of interest assuming it has a linear relationship with other time series

## Linear Regression
Assumptions about the errors:
- mean = 0, otherwise forecasts systematically biased
- not autocorrelated, otherwise there is still information to be exploited
- unrelated to the predictor vars, otherwise more info should be included in the systematic part of the model

### Goodness-of-fit
**Coefficient of determination (R²)**: proportion of variation in the forecast variable that is accounted by the regression model. Range between 0 (worst) and 1 (best)

> Validating performance on the test data is much better than measuring R² on the training data

### Standard error of the regression
"Residual standard error"

### Evaluating the regression model
Residuals (training-set errors): difference between observed and fitted values. Average of the residuals = 0 and correlations between residuals and predictor = 0

#### ACF plot of residuals
If there is autocorrelation in the residuals -> info left over which should be accounted in the model -> usually have larger prediction intervals

**Breusch-Godfrey**: Lagrange Multiplier (LM) test for serial correlation -> similar to Ljung-Box test, but specifically for regression models

#### Histogram of residuals
Check whether the residuals are normally distributed, not essential, but makes the calculation of prediction intervals easier

#### Residual plots against predictors
If the scatterplots show a pattern, the relationship may be nonlinear and the model will need to be modified

> Also plot the residuals against predictors that are **not** in the model -> if show pattern, the corresponding predictor may need to be added to the model

#### Residual plots against fitted values
If pattern is observed, there may be "heteroscedasticity" in the errors -> variance of the residuals may not be constant -> transformation of the forecast variable (e.g., logarithm or square root)

#### Outliers and influential observations
- outliers -> obs with extreme values compared to the majority of the data
- influential observations -> obs that have a large influence on the estimated coeff of a regression model

#### Spurious regression
More often than not, time series data are "non-stationary" -> values do not fluctuate around a constant mean or with a constant variance

Regressing non-stationary time series can lead to spurious regressions. Signs: High R², high residual autocorrelation

#### Some useful predictors
- Trend
- Dummy variables: when a predictor is a categorical variable
- Intervention variables: when the effect lasts only for one period -> "spike" variable
- Trading days
- Distributed lags
- Fourier series: alternative to seasonal dummy vars, especially for long seasonal periods. Regression model containing Fourier terms -> **harmonic regression**

## Selecting predictors

### Not recommended
- Plot forecast var against a particular predictor -> not always possible to see a relationship without accounting for other predictors
- Multiple linear regression with all predictors and disregard vars with high p-value

### Recommended
- Adjusted R² (tends to select too many predictors)
- **Cross-validation (CV)**
- Akaike's Information Criterion (AIC)
- **Corrected Akaike's Information Criterion (AICc)**
- Schwarz's Bayesian Information Criterion (BIC)

> Best subset regression: fit all potential regression models and choose the best (based on the criteria above) -> "all possible subsets" regression

### Stepwise regression

- **Backwards stepwise regression**: starts with all predictors, remove one at a time, keep the model if improves, iterate until no further improvement -> bad if n_predictors is very large
- **Forward stepwise regression**: starts with one, add one at a time, the one the most improves is kept, iterate...

> Not guaranteed to lead to the best possible model

### Ex-ante vs ex-post forecasts
- Ex-ante: made using only info available in advance
- Ex-post: made using later info on the predictors (not genuine forecasts, but useful for studying the behaviour of forecasting models)

### [Matrix formulation](https://otexts.com/fpp2/regression-matrices.html)

### Correlation, causation and forecasting
> It is important not to confuse correlation with causation, or causation with forecasting

Correlations are useful for forecasting, even when there is no causal relationship. Often a better model is possible if a causal mechanism can be determined.

#### Confounded predictors
Two vars are **confounded** when their effects on the forecast variable cannot be separated

> Confounding: not a problem for forecasting. However, it becomes a problem with scenario forecasting -> take account of the relationships between predictors. Also a problem if some historical analysis of the contributions of various predictors is required.

#### Multicollinearity and forecasting
**Multicollinearity**: when similar info is provided by 2+ predictors in a multiple regression (e.g., dummy var trap). Generally not a problem if you are not interested in the specific contributions of each predictor, except when there is perfect correlation

# 6. Time series decomposition

Three types of time series patterns:
- trend-cycle (or just trend)
- seasonality
- remainder (anything else in the time series)

## Time series components
- **Additive decomposition**: if the magnitude of the seasonal fluctuations, or the variation around the trend-cycle, does not vary with the level of the time series
- **Multiplicative decomposition**: when the variation in the seasonal pattern or the variation around the trend-cycle, appears to be proportional to the level of the time series -> common with economic time series

> Alternative to using multiplicative: first transform the data -> variation appears to be stable over time -> use additive

**Seasonally adjusted data**: if the seasonal component is removed from the original data

> Seasonally adjusted series contain the remainder component as well as the trend-cycle. Therefore, they are not “smooth”, and “downturns” or “upturns” can be misleading. If the purpose is to look for turning points in a series, and interpret any changes in direction, then it is better to use the trend-cycle component rather than the seasonally adjusted data.

## Moving averages
First step in classical decomposition -> using MA to estimate the trend-cycle. The order of the moving average determines the smoothness of the trend-cycle estimate (larger order = smoother curve).

Odd order -> symmetric MA

Applying MA to a MA -> symmetric MA

Most common use of centred MAs -> estimating the trend-cycle form seasonal data

> A 2×12-MA can be used to estimate the trend-cycle of monthly data and a 7-MA can be used to estimate the trend-cycle of daily data with a weekly seasonality. Other choices for the order of the MA will usually result in trend-cycle estimates being contaminated by the seasonality in the data.

### Weighted moving averages
Combinations of moving averages result in weighted moving averages

Advantage: yield a smoother estimate of the trend-cycle

## Classical decomposition (*not recommended*)
Starting point for most other methods of time series decomposition
- don't estimate trend-cycle/remainder for first and last few observations
- tends to over-smooth rapid rises and falls
- unable to capture seasonal changes over time
- not robust to unusual values

## X11 decomposition
for quarterly and monthly data

## SEATS decomposition
"Seasonal Extraction in ARIMA Time Series": works only with quarterly and monthly data

## STL decomposition
"Seasonal and Trend decomposition using Loess"

- handle any type of seasonality
- seasonal component is allowed to change over time
- smoothness of the trend-cycle can be controlled by the user
- can be robust to outliers
- doesn't handle trading day or calendar variation automatically

## Measuring strength of trend and seasonality
Useful when you have a large collection of time series and you need to find the series with the most trend or the most seasonality

## Forecasting with decomposition
Decomposition is primarily useful for studying time series data and exploring historical changes over time, but can also be used in forecasting

Forecast the seasonal component and the seasonally adjusted component separately:
- assume the seasonal component is unchanging (or changing slowly) -> seasonal naïve method
- to forecast the seasonally adjusted component -> any non-seasonal forecasting method may be used


# 7. Exponential smoothing
> Forecasts produced using exponential smoothing methods are weighted averages of past observations, with the weights decaying exponentially as the observations get older. In other words, the more recent the observation the higher the associated weight

## Simple exponential smoothing (SES)
For data with no clear trend or seasonal pattern

### Optimisation
Exponential smoothing method requires the smoothing parameters and the initial values to be chosen
- subjective manner
- estimate from observed data -> minimising the SSE (sum of squared errors)

## Trend methods
### Holt's linear trend method
Extends simple exponential smoothing to allow the forecasting of data with a trend

### Damped trend methods
Introduce a parameter that "dampens" the trend to a flat line some time in the future

> As forecasting tasks can vary by many dimensions (length of forecast horizon, size of test set, forecast error measures, frequency of data, etc.), it is unlikely that one method will be better than all others for all forecasting scenarios. What we require from a forecasting method are **consistently sensible forecasts**, and these should be frequently evaluated against the task at hand.

## Holt-Winters' seasonal method
Extends Holt's method to capture seasonality
- Additive
- Multiplicative

Additive preferred when the seasonal variations are roughly constant. Multiplicative preferred when the seasonal variations are changing proportional to the level of the series

## A taxonomy of exponential smoothing methods
By considering variations in the combinations of the trend and seasonal components, nine exponential smoothing methods are possible

## Innovations state space models for exponential smoothing
Statistical models generate point forecasts, but can also generate forecast intervals -> stochastic (or random) data generating process that can produce an entire forecast distribution

**State space models**: model consists of a measurement equation (observed data) and state equations (unobserved components or states: level, trend, seasonal change over time)
- ETS(A,N,N): simple exponential smoothing with additive errors
- ETS(M,N,N): simple exponential smoothing with multiplicative errors
- ETS(A,A,N): Holt’s linear method with additive errors
- ETS(M,A,N): Holt’s linear method with multiplicative errors
- Other ETS models

## Estimation and model selection
### Estimating ETS models
- minimize SSE
- maximize "likelihood" (probability of the data arising from the specified model)

### Model selection
Information criteria can be used for model selection on the ETS statistical framework
- AIC
- AICc
- BIC

## Forecasting with ETS models
ETS point forecasts are equal to the medians of the forecast distributions

### Prediction intervals
Big advantage: prediction intervals can also be generated 

# 8. ARIMA models
Exponential smoothing -> describe the trend and seasonality 

ARIMA -> describe the autocorrelations

## Stationarity and differencing
**Stationary time series**: properties do not depend on the time at which the series is observed. Time series with trends, or with seasonality, are not stationary. White noise is stationary

Stationary time series will have no predictable patterns in the long-term -> time plot roughly horizontal, with constant variance

### Differencing
Differencing: computing the differences between consecutive observations = "first differences" -> one way to make a non-stationary time series stationary

Transformations such as logarithms can help to stabilise the variance of a time series. Differencing can help stabilise the mean of a time series by removing changes in the level of a time series, and therefore eliminating (or reducing) trend and seasonality.

> **ACF Plot**: For a stationary time series, the ACF will drop to zero relatively quickly, while the ACF of non-stationary data decreases slowly.

### Random walk model
Widely used for non-stationary data -> financial, economic data

y_t = y_(t-1) + white_noise_t

Typically have:
- long periods of apparent trends up or down
- sudden and unpredictable changes in direction

Underpins naïve forecasts

### Second-order differencing
When difference data not appear stationary. "Change in the changes". Almost never necessary to go beyond second-order.

### Seasonal differencing
Seasonal difference: difference between an observation and the previous observation from the same season

> There is a degree of subjectivity in selecting which differences to apply. It is important that if differencing is used, the differences are interpretable.

### Unit root tests
Statistical hypothesis tests of stationarity that are designed for determining whether differencing is required.

- Kwiatkowski-Phillips-Schmidt-Shin (KPSS) test: null hypothesis = data stationary -> `p-value < 0.05` -> differencing is required

## Backshift notation
`L` -> "lag"

`B` -> "backshift"

B¹²y_t = y_(t-12)

## Autoregressive models
Forecast the variable of interest using a linear combination of *past values of the variable*

**AR(p) model**: an autoregressive model of order p

## Moving average models
Uses past forecast errors in a regression-like model

**MA(q) model**: a moving average model of order q

> Moving average models should not be confused with the moving average smoothing. A moving average model is used for forecasting future values, while moving average smoothing is used for estimating the trend-cycle of past values

MA model is called **invertible**

## Non-seasonal ARIMA models
Combine differencing with autoregression and a moving average model

**ARIMA(p,d,q) model**
- p = order of the autoregressive part
- d = degree of first differencing involved
- q = order of the moving average part

### ACF and PACF plots
Sometimes used to determine appropriate values for `p` and `q`

Extensible explanation [here](https://otexts.com/fpp2/non-seasonal-arima.html)

## Estimation and order selection
### Maximum likelihood estimation (MLE)
Finds the values of the parameters which maximise the probability of obtaining the data that we have observed

## Information Criteria
Good models are obtained by minimising the Akaike's Information Criterion (AIC) or AICc or BIC

Tend not to be good for selecting `d`, but only for selecting `p` and `q`

## Forecasting
> The prediction intervals for ARIMA models are based on assumptions that the residuals are uncorrelated and normally distributed. If either of these assumptions does not hold, then the prediction intervals may be incorrect. For this reason, always plot the ACF and histogram of the residuals to check the assumptions before producing prediction intervals.

## Seasonal ARIMA models
Formed by including additional seasonal terms in the ARIMA models

The seasonal part of the model consists of terms that are similar to the non-seasonal components of the model, but involve backshifts of the seasonal period

> The seasonal part of an AR or MA model will be seen in the seasonal lags of the PACF and ACF

Good examples in the book [here](https://otexts.com/fpp2/seasonal-arima.html)

## ARIMA vs ETS
> Myth: ARIMA models are more general than exponential smoothing

All ETS models are non-stationary, while some ARIMA models are stationary

ETS models with seasonality or non-damped trend or both have two unit roots (i.e., they need two levels of differencing to make them stationary). All other ETS models have one unit root (they need one level of differencing to make them stationary).

# 9. Dynamic regression models
# 10. Forecasting hierarchical or grouped time series
# 11. Advanced forecasting methods
# 12. Some practical forecasting issues
