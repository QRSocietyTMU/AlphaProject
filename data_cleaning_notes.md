# Data Cleaning Notes

## Input preview

The raw file contained these columns:

- `Date`
- `Close/Last`
- `Volume`
- `Open`
- `High`
- `Low`
- One extra empty column caused by a trailing comma on each row

The raw observations were ordered from newest to oldest. Price fields contained dollar signs, volume contained comma separators, and several column names contained spaces or punctuation.

## Changes made

1. Removed leading and trailing spaces from all fields.
2. Removed the extra empty trailing column.
3. Standardized the retained column names to:
   - `date`
   - `open`
   - `high`
   - `low`
   - `close`
   - `volume`
4. Renamed raw `Close/Last` to `close`.
5. Converted dates to `YYYY-MM-DD`.
6. Sorted dates from oldest to newest.
7. Checked for duplicate trading dates and retained only one row per date.
8. Removed dollar signs and comma separators from price fields.
9. Converted `open`, `high`, `low`, and `close` to decimal numbers.
10. Converted `volume` to a whole number.
11. Kept only the six agreed columns.
12. Checked for missing required values.
13. Checked basic OHLC consistency and positive volume.
14. Did not calculate returns, volatility, trends, labels, or other signals.
15. Did not fill or estimate any missing prices.

## Validation summary

- Clean rows saved: **1,255**
- Date range: **2021-07-28 to 2026-07-28**
- Duplicate dates removed: **0**
- Rows excluded for missing required values: **0**
- Rows excluded for invalid formatting: **0**
- Basic OHLC or non-positive-volume issues found: **0**

## Observations retained without alteration

The following unusual-looking records were kept because the cleaning role should not silently change valid-looking source observations:

- `2026-04-20`: open, high, low, and close are all `710.14`.
- `2026-04-17`: volume is exactly `9,999,999`.

These records should be checked against the original data provider if the team wants to verify them. No values were corrected, filled, or deleted based only on appearance.

## Output

The completed standardized dataset is saved as:

`data/clean_data.csv`
