# Public demo: build and acceptance plan

This is a **plan**, not a claim that the downloadable demonstration exists.

## Inputs required

- Claude's updated workbook with the proposed 150 processing blocks.
- A brief change log of formulas and ranges altered in the 100-to-150 expansion.
- Confirmation of which research themes, board names and personal notes may be disclosed, if any.

## Build procedure

1. Work on a separate copy; preserve the original workbook unchanged.
2. Inventory worksheets (including hidden ones), defined names, formulas, external connections and properties; compare with the technical handoff.
3. Verify complete processing for blocks 1, 100, 101 and 150, including price history, formulas, summaries and `data_sort` joins.
4. Construct a synthetic universe and reproducible synthetic daily OHLCV inputs. Remove external live-feed requirements, licensed cached values and private annotations.
5. Preserve the genuine indicator calculations and interactive board/group, trend/ATR filter and sort controls.
6. Add explicit as-of/date-staleness and matched, processed, filtered, missing-data and capacity-excluded counts when feasible; document any remaining limitation rather than hiding it.
7. Verify reported board counts and the misleading original indicator labels; disclose any corrections made.
8. Inspect workbook internals for personal metadata, names, links, cached source data and external queries.
9. Recalculate using Microsoft 365 Excel and visually inspect the workbook before taking screenshots.
10. Publish the file, screenshots and operating guide only after the required checks pass.

## Acceptance scenarios

| Test | Expected result |
|---|---|
| 110 eligible names | All 110 appear when filters are open. |
| 150 eligible names | All 150 appear and are mapped to their own indicators. |
| 151 eligible names | An explicit capacity warning or a documented alternate handling strategy; no silent loss. |
| Name without data | Counted with an explanatory data-quality status; not mistaken for a filtering failure. |
| Switch thematic boards | Tickers, notes and metric joins update together. |
| Different last-trade dates | Shown and handled consistently under an explicit as-of policy. |
| Filter threshold boundary | Equality is accepted as documented (`>=` and `<=`). |
| Sorting | Both directions correct; blank/non-numeric values handled transparently. |
| Formula review | No visible `#REF!`, `#VALUE!`, `#SPILL!`, `#NAME?` or silent unresolved errors. |
| Privacy and licensing | No real private notes, credential paths or redistributed vendor data remain. |

**Gate:** Do not label the demo as functional or publish download links before the real workbook passes these tests.