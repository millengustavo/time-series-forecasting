# Forecasting at Scale
Authors: Sean J. Taylor and Benjamin Letham

[Source](https://peerj.com/preprints/3190.pdf)

## Table of Contents
- [Forecasting at Scale](#forecasting-at-scale)
  - [Table of Contents](#table-of-contents)
- [1. Introduction](#1-introduction)
- [2. Features of Business Time Series](#2-features-of-business-time-series)
- [3. The Prophet Forecasting Model](#3-the-prophet-forecasting-model)
- [3.1 Trend Model](#31-trend-model)
- [3.2 Seasonality](#32-seasonality)
- [3.3 Holidays and Events](#33-holidays-and-events)
- [3.4 Model fitting](#34-model-fitting)
- [3.5 Analyist-in-the-Loop Modeling](#35-analyist-in-the-loop-modeling)
- [4. Automating Evaluation of Forecasts](#4-automating-evaluation-of-forecasts)
  - [Simulated Historical Forecasts](#simulated-historical-forecasts)
  - [Identifying Large Forecast Errors](#identifying-large-forecast-errors)
- [5. Conclusion](#5-conclusion)

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
- Use of baseline forecasts
- Modeling forecast accuracy: mean absolute percentage error (MAPE) -> for interpretability

## Simulated Historical Forecasts
- Produce `K` forecasts at various cutoff points in the history
- Simulate the errors we would have made hade we used this forecasting method at those points in the past
- Simple, easy to explain and relatively uncontroversial for generating insight into forecast errors

Issues to be aware:
- The more simulated forecasts we make, the more correlated their estimates of error are
- Forecasting methods can perform better or worse with more data

## Identifying Large Forecast Errors
- When the forecast has large errors relative to the baselines, the model may be misspecified. Analysts can adjust the trend model or the seasonality, as needed
- Large errors for all methods on a particular date are suggestive of outliers. Analysts can identify outliers and remove them.
- When the SHF error for a method increases sharply from one cutoff to the next, it could indicate that the data generating process has changed. Adding changepoints or modeling different phases separately may address the issue.

# 5. Conclusion
Prophet in summary:
- Simple, modular regression model that often works well with default parameters, and that allows analysts to select the components that are relevant to their forecasting problem and easily make adjustmens as needed
- Has a system for measuring and tracking forecast accuracy, and flagging forecasted that should be checked manually to help analysts make incremental improvements