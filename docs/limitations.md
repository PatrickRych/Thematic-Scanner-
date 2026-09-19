# Limitations and outstanding validation

**Status:** Findings below come from a technical handoff describing the earlier 100-block `SCANNER.xlsx`. They have **not yet been independently checked** against the expanded 150-block workbook. Reported problems may have been addressed in that newer version.

## Reported engineering issues

| Issue in earlier version | Why it matters | Acceptance check for updated version |
|---|---|---|
| 100-ticker processing cap | A selected board with more entries could silently omit names. | Test 110 and 150 eligible tickers end to end; report overflow of 151. |
| Asynchronous ticker data dates | Cross-sectional indicators might mix nonmatching observation dates. | Show a common as-of policy and individual source dates; flag stale data. |
| `IFERROR(...,"")` masking | Missing data, invalid symbols, calculation errors and filtered names can look identical. | Surface counts and diagnostic reasons; reconcile selected/processed/excluded names. |
| Incomplete board-count ranges and hardcoded map counts | Reported universe sizes may be incorrect. | Count nonblank tickers over the whole universe; compare source and displayed counts. |
| Misleading indicator names | Reported `RVOL21` and `RVOL_Pctl252` were expanding statistics, not rolling. | Correct definitions or names and explain which fields are active. |
| Numeric controls accept text | User entry can cause spill calculation errors. | Validate numeric limits and display actionable error guidance. |
| Fixed summary/lookback references | Adding history blocks without updating dependent ranges can leave names unprocessed. | Audit all 150 inputs, histories, summaries, joins and output formulas. |
| No historical snapshots | The previous universe and market state cannot be reconstructed solely from today's screen. | Do not claim point-in-time backtesting without a snapshot process. |

The handoff also mentioned old staging worksheets, vendor-data columns and references in a development log to features absent from the inspected file; these remain version-specific questions.

## Research limitations

The screener is **descriptive**. The handoff did not identify backtests, forward tests, benchmark comparisons or proof of predictive ability. A manually curated universe can introduce selection bias, and reconstructing past screens from today's surviving securities would risk look-ahead and survivorship bias. Changing threshold values after observing outcomes can create data-snooping risk. The `Tilt Matrix` is discretionary context, not a quantitatively inferred macro regime.

## Public workbook safeguards

Do not publish the private original. Inspect hidden sheets, defined names, author properties, notes, external workbook links, formula caches and any embedded data connections. Live Excel `STOCKHISTORY` data and Options Samurai-supplied fields may be covered by source-specific terms; a shareable demonstration should use **clearly synthetic OHLCV and synthetic placeholders** only after checking any remaining dependencies. Do not assume removing visible account data sanitizes workbook internals.

## Compatibility

The reported design uses Microsoft 365 functions including `LET`, `MAP`, `LAMBDA`, `FILTER`, `SORTBY` and dynamic spill behavior. Other spreadsheet programs cannot be promised equivalent results. The demo should disclose its calculation requirements and be opened and recalculated in the intended Excel environment.

**Publication gate:** No downloadable workbook or screenshots should be described as verified until the actual updated file has passed functional, data-quality and privacy checks.