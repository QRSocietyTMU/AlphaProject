# Walk-Forward Validation Summary

## Method

The logistic regression model was evaluated using expanding-window
walk-forward validation.

An initial historical training period was used to fit the model.
The next approximately one-month block was then predicted.
After each prediction block, the training window expanded and the model
was refitted using the available historical observations.

A five-trading-day gap was maintained between the end of each training
window and the beginning of the next test block because the target
measures SPY's direction over the following five trading days.

## Results

- Accuracy: 0.5934
- ROC-AUC: 0.4191
- Brier Score: 0.2496
- Majority-Class Accuracy: 0.5934

## Confusion Matrix

- True Negatives: 0
- False Positives: 98
- False Negatives: 0
- True Positives: 143

## Statistical Power — Supplementary

The validation contained 241 out-of-sample predictions.

An approximate power analysis indicated 35.2% power to detect
a five-percentage-point improvement over the majority-class benchmark
at the 5% significance level.

Approximately an 8.9% improvement over the baseline would be
needed to achieve 80% power under this approximation.

This analysis is supplementary and does not change the primary
walk-forward validation conclusion.

## Conclusion

The model did not outperform the simple majority-class baseline during walk-forward validation. Both achieved an accuracy of 59.34%. At the 0.50 classification threshold, the logistic regression predicted the positive class for every validation observation. The ROC-AUC of 0.419 indicates that the predicted probabilities did not effectively distinguish between subsequent upward and downward SPY movements. Overall, the tested signals did not provide evidence of useful out-of-sample directional forecasting performance under this baseline model. 

The results are reported as observed rather than optimizing the model
until it appears successful.
