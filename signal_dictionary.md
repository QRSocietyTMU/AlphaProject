| **Signal Name** | **Input** | **What it measured** | **Why it was calculated** |
|---|---|---|---|
| **1-Day Return** | `df['1d_return'] = df['close'].pct_change()` | The percentage change in SPY’s price over the previous trading day. | To test whether very recent price movement contains information about SPY’s next 5-day direction. |
| **5-Day Return** | `df['5d_return'] = df['close'].pct_change(5)` | The percentage change in SPY’s price over the previous 5 trading days. | To capture short-term momentum and determine whether the past week’s performance helps predict the next 5-day direction. |
| **20-Day Return** | `df['20d_return'] = df['close'].pct_change(20)` | The percentage change in SPY’s price over the previous 20 trading days. | To capture a longer short-term trend and test whether recent monthly performance predicts future direction. |
| **Distance from 10-Day SMA** | `df['10ma'] = df['close'].rolling(window=10).mean()`<br><br>`df['percent_ma_gap'] = (df['close'] - df['10ma']) / df['10ma'] * 100` | The percentage difference between the current price and its 10-day simple moving average (SMA). | To determine whether SPY is trading unusually far above or below its recent short-term average. |
| **10-Day/50-Day SMA Crossover** | `df['50ma'] = df['close'].rolling(window=50).mean()`<br><br>`df['sma_crossover'] = (df['10ma'] > df['50ma']).astype(int)` | 1 if the 10-day SMA is above the 50-day SMA, 0 otherwise. | To capture changes in short- versus medium-term trends that may signal bullish or bearish conditions. |
| **20-Day Drawdown** | `df['20d_drawdown'] = df['close'] / df['close'].rolling(window=20).max() - 1` | The percentage decline from the highest price observed during the previous 20 trading days. | To measure whether SPY has recently experienced a decline that could indicate weakness or a potential recovery. |
| **10-Day Realized Volatility** | `df['10d_volatility'] = df['1d_return'].rolling(window=10).std()` | The standard deviation of daily returns over the previous 10 trading days. | To determine whether recent market uncertainty affects the predictability of SPY’s future direction. |
| **Volatility Ratio** | `df['20d_volatility'] = df['1d_return'].rolling(window=20).std()`<br><br>`df['volatility_ratio'] = df['10d_volatility'] / df['20d_volatility']` | 10-day volatility divided by 20-day volatility. | To compare current short-term volatility with a longer recent volatility baseline. |
| **20-Day Volume Z-Score** | `df['volume_zscore'] = ((df['volume'] - df['volume'].rolling(window=20).mean()) / df['volume'].rolling(window=20).std())` | How many standard deviations the current volume is from its 20-day average volume. | To identify unusually high or low trading activity that may contain information about future price direction. |
| **14-Day RSI** | `delta = df['close'].diff()`<br><br>`gain = delta.clip(lower=0)`<br>`loss = -delta.clip(upper=0)`<br><br>`avg_gain = gain.rolling(window=14).mean()`<br>`avg_loss = loss.rolling(window=14).mean()`<br><br>`rs = avg_gain / avg_loss`<br><br>`df['rsi_14'] = 100 - (100 / (1 + rs))` | A momentum oscillator from 0–100 measuring the magnitude of recent gains relative to recent losses. | To test whether overbought or oversold conditions are associated with the subsequent 5-day direction of SPY. |

## Target

The **future 5-day return** and **target** are the outcomes being predicted, not signals.

- **Future 5-Day Return:** The percentage change in SPY’s price over the **next 5 trading days**.
- **Target:** The direction of the future 5-day return, indicating whether SPY’s price is higher or lower after 5 trading days.

The signals above are the explanatory variables used to test whether interpretable market information can help forecast the target.