# Indicator and screening methodology

> **Evidence status:** These definitions are reported in Claude's technical handoff for the earlier screener. The updated 150-block workbook has not been independently audited. This document describes indicators, not a validated investment strategy.

## Price-based calculations

| Measure | Reported method | Interpretation / limitation |
|---|---|---|
| True range | `MAX(High-Low, ABS(High-PriorClose), ABS(Low-PriorClose))` | Includes opening gaps. |
| ATR14 | Seed with 14-period mean TR, then `(13*prior ATR + current TR)/14` | Wilder-smoothed range in price units. |
| ATR% | `ATR14/Close` | Range as a percentage of price. |
| SMA50 | Average of most recent 50 closing prices | Price reference for the extension measure. |
| ATR multiple | `(Close/SMA50-1)/(ATR14/Close)` | Percentage deviation from SMA50 divided by ATR%. Not mathematically identical to `(Close-SMA50)/ATR14`. |
| SMA21 / SMA112 | Trailing averages over 21 and 112 close observations | Shorter- and longer-term trend context. |
| Trend score | `(1[Close>SMA21] + 1[Close>SMA112])/2` | Possible values: 0, 0.5, 1; not a forecast or statistical probability. |
| 1d / 10d / 1m returns | `Close_now/Close_n_trading_rows_ago - 1`, with n=1,10,21 | Trading-day offsets; one month is approximated with 21 rows. |
| Volume ratio | `SMA3(Volume)/SMA50(Volume)` | Recent volume relative to history. |
| Volume z-score | `(latest volume ratio - sample mean of historical ratios)/sample standard deviation` | Unusual activity versus available reference window; dependent on sample completeness. |
| RSI14 | Gains versus losses using the final 14 deltas with simple averages | Cutler-style RSI, not Wilder-smoothed RSI. |
| MFI14 | Typical price times volume; 14-period positive vs negative flow | Money Flow Index; zero-division guards required. |

The older model reportedly has expanding-window statistics labeled `RVOL21` and `RVOL_Pctl252`; these labels do **not** establish rolling 21-day volatility or rolling 252-day percentiles. They were reported unused by the active screening output. Their names and formulas require inspection before publication.

## Screening process

The handoff describes **two sequential stages**:

1. **Universe selection:** board match and effective group match select entries from the curated list.
2. **Result eligibility:** nonblank ticker **AND** numeric ATR multiple **AND** trend score at least the user's minimum **AND** ATR multiple between inclusive user minimum and maximum.

The original open thresholds reportedly use `-99` and `+99`. After filtering, securities are sorted by **one** user-selected metric in the selected direction, with blanks placed last. The default sort is curated Master List order. The tool does **not** compute a weighted multi-factor security ranking or automated buy/sell recommendations.

## External and discretionary inputs

The macro-quadrant tilt is a manually entered label from `Tilt Matrix`, **not** a computed macro forecast. `VOL SCORE`, `SKEW`, and `VOL POWER` were described as Options Samurai data fields; their formulas and source definitions are not independently established here. A public copy must omit licensed data or clearly label any synthetic substitutes.

## Using the output

A trend score of 0.5 means that price exceeds exactly one of the two moving averages. An extreme ATR multiple means a price is extended relative to its own range measure; the indicator alone cannot predict continuation or reversal. Candidate selection is a starting point for additional research, not a trading instruction. No predictive validity or performance claims have been established.