# Choosing an electricity contract from a year of smart-meter data

> Course assignment from 2023, kept as it was written. The notes under "Reading the result" were added in November 2026.

A data-cleaning case: one year of hourly meter readings arrives as 8,760 free-text lines such as
`_1AM  Friday 19th-Dec-2014___0.209  kwh`. The notebook parses them, rebuilds the time series and
prices the year under three contracts.

## Method

1. One regular expression extracts hour, AM/PM, day, month, year and kWh from every line.
2. Build timestamps, sort, and drop 6 duplicate rows (8,754 hours remain).
3. Answer the six questions of the case with pandas.

## Result

| Contract | Cost of the year |
|---|---|
| No Flex (flat price) | $1,436.87 |
| Monthly Flex | $1,420.06 |
| **Hourly Flex** | **$1,367.85** |

Hourly Flex is cheapest, by $69 (4.8%) against the flat price.

| Question | Answer |
|---|---|
| Average hourly usage | 0.782 kWh |
| Average hourly usage in February | 0.834 kWh |
| Day of the week with the highest usage | Sunday (0.899 kWh per hour) |
| Highest usage in 4 consecutive hours | 17.237 kWh |

## Reading the result

The comparison assumes next year's usage repeats last year's hour by hour. The Hourly Flex
advantage depends on usage staying out of the expensive hours.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook "Electricity Contract Selection.ipynb"
```

## Files

| File | Content |
|---|---|
| `Electricity Contract Selection.ipynb` | Analysis |
| `Electricity Contract Selection.html` | Rendered copy |
| `data_cleaning.xlsx` | Raw usage lines and contract prices |
| `output.xlsx` | The cleaned hourly series |
| `About.txt` | Original case text |
