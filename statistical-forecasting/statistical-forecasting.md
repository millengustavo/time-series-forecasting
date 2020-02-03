# Statistical forecasting: notes on regression and time series analysis
Authors: Robert Nau

[Available here](https://people.duke.edu/~rnau/411home.htm)
> "This web site contains notes and materials for an advanced elective course on statistical forecasting that is taught at the Fuqua School of Business, Duke University. It covers linear regression and time series forecasting models as well as general principles of thoughtful data analysis."

# Table of Contents
- [Statistical forecasting: notes on regression and time series analysis](#statistical-forecasting-notes-on-regression-and-time-series-analysis)
- [Table of Contents](#table-of-contents)
- [1. Get to know your data](#1-get-to-know-your-data)
  - [Principles and risks of forecasting](#principles-and-risks-of-forecasting)
    - [Signal vs. noise](#signal-vs-noise)
    - [Risks of forecasting](#risks-of-forecasting)
- [2. Introduction to forecasting: the simplest models](#2-introduction-to-forecasting-the-simplest-models)
- [3. Averaging and smoothing models](#3-averaging-and-smoothing-models)
- [4. Linear regression models](#4-linear-regression-models)
- [5. ARIMA models for time series forecasting](#5-arima-models-for-time-series-forecasting)
- [6. Choosing the right forecasting model](#6-choosing-the-right-forecasting-model)

> "I have seen the future and it is very much like the present, only longer." 
> -- Kehlog Albran, *The Profit*

# 1. Get to know your data
## Principles and risks of forecasting
Statistical forecasting: art and science of forecasting from data, with or without knowing in advance what equation you should use

### Signal vs. noise
Variable you want to predict = signal + noise
- Signal: predictable component
- Noise: what is left over

Sensitive statistical tests are needed to get a better idea of whether the pattern you see in the data is really random or whether there is some signal yet to be extracted. If you fail to detect a signal that is really there, or falsely detect a signal that isn’t really there, your forecasts will be at best suboptimal and at worst dangerously misleading

**random walk model**: the variable takes random steps up and down as it goes forward:
- if you transform by taking the period-to-period changes (the "first difference") it becomes a time series that is described by the mean model
- the confidence limits for the forecasts gets wider at longer forecast horizons
- typical of random walk patterns -> they don't look random as they are! -> analyze the statistical properties: momentum, mean-reversion, seasonality

### Risks of forecasting
> "If you live by the crystal ball you end up eating broken glass"

- **Intrinsic risk**: random variation beyond explanation with the data and tools available
- **Parameter risk**: errors in estimating the parameters of the forecasting model, under the assumption that you are fitting the correct model to the data in the first place
> When predicting time series, more sample data is not always better -> might include older data that is not as representative of current conditions. **Blur of history** problem: no pattern really stays the same forever

You can't eliminate instrinsic risk and parameter risk, *you can and should try to quantify* them in relative terms -> so the appropriate risk-return tradeoffs can be made when decisions are based on the forecast

- **Model risk**: risk of choosing the wrong model. *Most serious form of forecast error* -> can be reduced by following good statistical practices: Follow good practices for exploring the data, understand the assumptions that are behind the models and test the assumptions.

If the errors are not pure noise -> there is some pattern in them, and you could make them smaller by adjusting the model to explain that pattern

# 2. Introduction to forecasting: the simplest models

# 3. Averaging and smoothing models

# 4. Linear regression models

# 5. ARIMA models for time series forecasting

# 6. Choosing the right forecasting model
