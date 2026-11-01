# Export Packing Cost Analysis - In-house vs Outsourced (Excel case study)

![Dashboard](dashboard.png)

An Excel model that costs export packing for FRP pressure vessels from SAP-style stores data, proposes standard packing BOMs for the sizes that had none, and checks whether outsourcing packing would be cheaper than doing it in-house.

> **Data note:** this is a fictional case study. All data - orders, stores issues, labour log, BOM and vendor quotes - is simulated to look like SAP exports and shop records. No company, customer or supplier data is included. Material rates, wages and USD-INR are based on public market data (links inside the workbook).

**In short:**
- **In-house packing is the cheapest option for every vessel size.** The turnkey packer quotes 1.16-1.22x our own cost.
- **Flat-rack sizes (2.4 m and above) cost about twice as much to pack:** ₹26,755 vs ₹13,208 per vessel.
- **The 2.0 m jobs used 5.9% more timber than their BOM**, and the other six sizes had no BOM at all.
- **Recommendation:** release the proposed BOMs, keep packing in-house, and buy ready-made skids only if the packing bay becomes a bottleneck.

**Skills used:** Excel (SUMIFS, lookups, data validation, charts), data cleaning, job costing, make-or-buy and breakeven analysis.

## Why I picked this

In export planning, packing sits between production and dispatch, and it can decide whether a shipment leaves on time. It is also easy to under-cost, because it is usually done by eye and nobody adds up the timber, labour and bay time per vessel.

## The problem

The brief in this case has two goals: **close the gap between actual and design BOMs**, and **decide which outsourced activities should be done in-house**. For export packing (timber skids, foam, bubble wrap, stretch film, lashing), only one vessel size (2.0 m) had a written packing BOM. Every other size was packed as the supervisor decided, so nobody knew what packing actually cost per vessel.

Three questions:
1. What does packing cost per vessel, by size?
2. What standard BOM should each size have?
3. Is any outsourcing option cheaper than packing in-house?

## My role

Engineering inputs (packing method, vessel dimensions, what a BOM should contain) came from the project engineer. **I did the data work:** collecting the SAP exports, labour log and vendor rates, cleaning them, building the costing model, the analysis and the dashboard.

## How I worked through it (DMAIC)

1. **Define** - no standard BOM for most sizes, so packing cost per vessel was unknown. The three questions above.
2. **Measure** - collected SAP goods-issue exports, a packing labour log, vendor rates and three packer quotes (`Data -` tabs, pasted as values). Cleaned them with helper columns next to the raw data: corrected job numbers, fixed text dates, filled one missing labour day, converted units, removed GST, and mapped **27 vendor item names to 13 items**.
3. **Analyse** - costed every job: material from stores issues, labour from the log (average hours per vessel for jobs before the log existed), overtime at double rate, fumigation and supervision. Compared actual use with the one written BOM, and compared four options per size: in-house, contractor labour only, buying ready-made skids, and a turnkey packer.
4. **Improve** - average use per vessel by size became the draft standard BOM (**35 timber lines for 6 sizes**), checked against the one written BOM.
5. **Control** - once the BOMs are released, stores issues can be checked against them on every job. The dashboard (vessel size and vessels per shipment) makes that check quick.

## Findings (simulated data)

- **Actual vs design:** the 2.0 m jobs used **5.9% more timber** than their BOM (7.56 vs 7.14 cft per vessel). The earlier jobs were packed before the BOM existed.
- **Flat-rack sizes cost about 2x to pack.** Vessels 2.4 m and above don't fit through a 40-ft container door, so they ship on flat racks and need heavier saddles and weather cover: **₹26,755 vs ₹13,208 per vessel**.
- **In-house is cheapest for every size** on cash cost. The turnkey packer quotes **1.16-1.22x** our own cost.
- **Buying ready-made skids** only pays when packing-bay time is scarce: above **₹2,400-13,300 per bay-day**, depending on size.
- The rupee is **9.4% weaker** than when the USD packaging price was set, which raises the rupee margin with no price change.

**The economics behind it.** On cash cost alone, in-house wins every time. The only case for buying skids is the opportunity cost of the packing bay: if a free bay-day is worth more than the breakeven above (because it lets another shipment go out), buying skids makes sense. The workbook lets you set that value and see where the answer flips.

**Recommendation:** release the proposed BOMs, keep packing in-house, and revisit buying skids if the packing bay becomes a bottleneck.

![Proposed standard](proposed_standard.png)

## Workbook tour

| Tab | What it does |
|---|---|
| Dashboard | Findings, key figures, 4 charts, 2 controls |
| Notes | Goal, roles, data basis, steps, assumptions, limitations, terms |
| Inputs | All assumptions in one place: current rates, wages, quotes, vessel dimensions, FX |
| Job Costing | Cost of each of the 19 jobs, 60 vessels |
| Proposed Std | Average use per vessel by size, standard cost, actual vs design BOM, draft BOM |
| Size Model | In-house vs 3 outsourcing options per size; cheapest option; breakeven |
| Outsourcing | Cost per vessel by shipment size for the selected size |
| Data - ... | SAP issues, labour log, vendor rates, item master, the 2.0 m BOM, with my check columns in green |

## Excel techniques used

SUMIFS, AVERAGEIFS, COUNTIF · VLOOKUP / HLOOKUP (exact and approximate match for date-based rates) · IF logic · data validation dropdowns · helper-column data cleaning · stacked, clustered and line charts. Works in Excel 2010 and later.

## Assumptions and limitations

- Design pressure 7.5-10 bar; wall thickness at the upper end (a few mm, no effect on packing cost).
- Jobs before the labour log started use average hours per vessel of logged jobs of the same size.
- Small sample: 19 jobs, 1 to 4 per size. Proposed standards are averages and need production sign-off.
- Flat-rack lashing is not checked against sea-transport forces. Vendor quotes are estimates built from market rates.

## How to use

Open `Export_Packing_Cost_Case_Study.xlsx` in Excel and change the two blue cells on the Dashboard: vessel size and vessels per shipment. To test the effect of a busy packing bay, set **Value of a free packing-bay day** on the Inputs tab.

## Files

- `Export_Packing_Cost_Case_Study.xlsx`: the model
- `dashboard.png`, `dashboard.pdf`: dashboard snapshot
- `proposed_standard.png`: the proposed-standard sheet

*Next step: a Power BI version of the dashboard from the same data.*
