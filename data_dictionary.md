# Data Dictionary

This file explains the columns in `data/clean_data.csv`.

| Column | Data type | Description |
|---|---|---|
| `date` | Date (`YYYY-MM-DD`) | The SPY trading date. Each date appears once and the file is ordered from oldest to newest. |
| `open` | Decimal number | SPY's opening market price for the trading day. |
| `high` | Decimal number | The highest SPY market price recorded during the trading day. |
| `low` | Decimal number | The lowest SPY market price recorded during the trading day. |
| `close` | Decimal number | SPY's closing or last market price for the trading day. The raw file called this field `Close/Last`; it is not labelled as adjusted close. |
| `volume` | Whole number | The number of SPY shares traded during the trading day. |

## Notes

- Prices are stored as plain numerical values without dollar signs or commas.
- Volume is stored as a whole number without commas.
- No returns, volatility, trends, targets, or other engineered signals are included.
