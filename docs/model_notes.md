# Baseline Logistic Regression Dataset:

The analysis uses the signals.csv dataset, where the data was sorted chronologically by date before modeling.

The original dataset contains 1,255 observations. The first 49 observations for the 10-day / 50-day SMA crossover were kept as unavailable because the 50-day SMA does not yet exist. The final 5 observations for the future 5-day target were also kept as unavailable because their future 5-day return cannot be calculated.
After removing observations with missing values in any of the 10 signals or the target variable, 1,201 of the 1,255 observations remained.

## Predictors

The baseline logistic regression uses the following 10 market signals:

| **Market Signals** | **Variable** |
|---|---|
| **1-Day Return** | `1d_return` |
| **5-Day Return** | `5d_return` |
| **20-Day Return** | `20d_return` |
| **Distance from 10-Day SMA** | `percent_ma_gap` |
| **10-Day / 50-Day SMA Crossover** | `sma_crossover` |
| **20-Day Drawdown** | `20d_drawdown` |
| **10-Day Realized Volatility** | `10d_volatility` |
| **Volatility Ratio** | `volatility_ratio` |
| **20-Day Volume Z-Score** | `volume_zscore` |
| **14-Day RSI** | `rsi_14` |

## Target
The outcome variable is target.
The target represents the direction of the future 5-day return, with the model estimating the probability that the target equals 1.

## Data Preparation
The master dataset was kept unchanged. Within the baseline regression notebook, the data was sorted chronologically and a working dataset was created containing the date, the 10 signal variables, and the target.

The first 49 SMA crossover values were kept as unavailable because the 50-day SMA does not yet exist. The final 5 target values were kept as unavailable because a future 5-day outcome is not available for those observations.

Rows with missing values in any predictor or the target were then removed before fitting the model.

## Development and Test Split
The 1,201 usable observations were divided chronologically into an older development/training period and a newer final test period.

The development period contains 960 observations from October 6, 2021 through August 4, 2025.

The final test/holdout period contains 241 observations from August 5, 2025 through July 21, 2026.

The final test period was kept separate from model fitting and tuning.

## Model
A baseline logistic regression was fitted using statsmodels.
The model uses the 10 market signals as predictors and target as the binary outcome.
The regression coefficients, standard errors, z-statistics, p-values, and confidence intervals are saved in:

regression_coefficients.csv

Predicted probabilities are saved in:

model_predictions.csv

## Validation
The baseline model does not perform expanding-window walk-forward validation.
The full expanding-window walk-forward evaluation will be performed during the subsequent validation stage.
The final holdout period is therefore not used to fit or tune the baseline regression.

## Model Output

The baseline logistic regression produced the following output:

```text
Optimization terminated successfully.
    Current function value: 0.671632
    Iterations 4
                            Logit Regression Results
==============================================================================
Dep. Variable:                 target   No. Observations:                  960
Model:                          Logit   Df Residuals:                      949
Method:                           MLE   Df Model:                           10
Date:                Sun, 16 Aug 2026   Pseudo R-squ.:                0.008492
Time:                        02:45:45   Log-Likelihood:                -644.77
converged:                       True   LL-Null:                       -650.29
Covariance Type:            nonrobust   LLR p-value:                    0.3540
==============================================================================
                 coef        std err       z        P>|z|      [0.025      0.975]
----------------------------------------------------------------------------------
const             1.4950      0.678      2.206      0.027       0.167       2.823
1d_return        -6.9914      6.979     -1.002      0.316     -20.670       6.687
5d_return        -1.5599      6.957     -0.224      0.823     -15.196      12.076
20d_return        3.1819      3.173      1.003      0.316      -3.038       9.402
percent_ma_gap   -0.0331      0.127     -0.261      0.794      -0.281       0.215
sma_crossover    -0.2899      0.217     -1.335      0.182      -0.715       0.136
20d_drawdown      4.1418      6.510      0.636      0.525      -8.618      16.902
10d_volatility   -7.1796     18.419     -0.390      0.697     -43.281      28.922
volatility_ratio -0.2225      0.434     -0.513      0.608      -1.072       0.627
volume_zscore    -0.1476      0.072     -2.059      0.039      -0.288      -0.007
rsi_14           -0.0103      0.007     -1.389      0.165      -0.025       0.004
==================================================================================


