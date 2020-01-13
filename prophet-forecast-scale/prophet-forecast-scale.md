# Forecasting at Scale
Authors: Sean J. Taylor and Benjamin Letham

[Source](https://peerj.com/preprints/3190.pdf)

# 1. Introduction

- Analysts who can produce high quality forecasts are quite rare because forecasting is a specialized skill requiring substantial experience

- Time series model flexible enough for a wide range of business time series, yet configurable by people with little knowledge about time series models and methods

- Automated means of evaluating and comparing forecasts, as well as detecting when they are likely to be performing poorly

# 2. Features of Business Time Series

- Auto ARIMA: prone to large trend errors and fail to capture any seasonality
- Exponential smoothing and seasonal naive: capture weekly seasonality, but miss longer-term seasonality

> Tuning these methods requires a thorough understading of how the underlying time series models work

# 3. The Prophet Forecasting Model

- Designed to have intuitive parameters that can be adjusted without knowing the details of the underlying model
- Decomposable time series model with three main model components: trend, seasonality and holidays
- Also an error term: any idiosyncratic changes which are not accomodated by the model (assumption: normally distributed)
- Similar to a generalized additive model (GAM): class of regression models with potentially non-linear smoothers applied to the regressors
- Frame the forecasting problem as a curve-fitting exercise != time series models that explicitly account for the temporal dependence structure in the data

**Practical advantages**
- Flexibility
- Measurements do not need to be regularly spaced and do not need to interpolate missing values (e.g., remove outliers)
- Fitting is fast
- Easily interpretable parameters. Easy to extend the model to include new components
- Tailored to time series with piecewise trends, multiple seasonality, floating holidays

# 3.1 Trend Model
- Saturating growth model
- Piecewise linear model

Changepoints can be specified or may be automatically selected given a set of candidates. A parameter controls the flexibility of the model altering its rate

The uncertainty in the trend is measured assuming the future will se the same average frequency and magnitude of rate changes that were seen in the history

# 3.2 Seasonality
Fourier series to provide a flexible model of periodic effects

# 3.3 Holidays and Events
Analyst provide a custom list of past and future events, identified by the event or holiday's unique name

Include additional parameters for the days surrounding the holiday, essentially treating each of the days in the window around the holiday as a holiday itself

# 3.4 Model fitting
Benefit of a decomposable model: allow us to look at each component of the forecast separately

Default values are appropriate to most forecast problems

# 3.5 Analyist-in-the-Loop Modeling
- Capacities
- Changepoints
- Holidays and seasonality
- Smoothing parameters

Parameters to increase/decrease trend flexibility and strength of the seasonality component

> Analyist-in-the-Loop Modeling: blends the advantages of statistical and judgemental forecasts. Lets analysts apply judgement to forecasts through a small set of intuitive model parameters and options, while retaining the ability to fall back on fully automated statistical forecasting when necessary


# 4. Automating Evaluation of Forecasts

# 5. Conclusion