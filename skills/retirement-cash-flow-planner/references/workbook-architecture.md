# Retirement Workbook Architecture

A full retirement plan of this kind can run to 13 tabs. The starter template
(`assets/retirement-plan-template.xlsx`) builds the first six; this doc describes all
13 so the skill can extend the template when a person's situation calls for it.

Formulas flow one direction: **Assumptions → everything else.** Every other tab pulls
its inputs from named cells on Assumptions, so changing one input cascades everywhere.
Keep it that way — never hardcode a number on a downstream tab that could instead be a
cell reference back to Assumptions.

## 1. Cover
One page of key facts: names/dates (as placeholders until filled in), retirement date,
total net worth, key account balances, and a milestone-date summary (59½, Medicare, SS
claim ages, RMD start years). Also a workbook guide — one line per tab.

## 2. Assumptions
Every input the model needs, in one place, organized in labeled blocks: Personal,
Compensation, Expenses, Investments & Retirement, Federal tax brackets, State tax
brackets, Rental/other income, Mortgage payoff dates (if relevant). Yellow fill marks
cells meant to be updated annually; everything downstream references these cells by
address, never by re-typing the number.

## 3. [Pre-retirement year] Tax Analysis
A full breakdown of the last working year's taxes — useful for deciding exact
retirement timing (e.g., does retiring Dec 31 vs. mid-year change the tax picture
meaningfully?). Optional; only build if the person cares about optimizing their exact
retirement date.

## 4. Retirement Date Analysis
Side-by-side comparison of a few candidate retirement dates, showing the after-tax
income captured, healthcare cost difference, and Roth conversion room gained/lost for
each. Optional — build only if the person is actively deciding between dates.

## 5. Phase Plan
The core annual cash-flow tab: gross income sources (deferred comp, rental, Social
Security, pension, etc.) minus expenses (living costs, healthcare, remaining mortgage
payments) equals a gap, funded by 401(k) withdrawals or savings draws. Runs one column
per year, from retirement through the end of the planning horizon. Include a PHASE row
labeling which of the six phases (see SKILL.md) each year falls into.

## 6. Tax Calculator
Full federal + state tiered-bracket tax calculation for a sample of years across the
plan (doesn't need every single year — a handful of representative years is enough to
see the trend). Feeds the effective tax rate used elsewhere in the model.

## 7. Roth Conversion
Year-by-year conversion tracker: starting traditional balance, amount converted,
tax cost of the conversion, resulting Roth balance, and remaining room in the target
tax bracket. Strategy note column per year. Prioritize converting the larger balance
(or the one with the least favorable RMD treatment) first.

## 8. Properties
Only if the person owns rental or investment real estate: one row per property with
purchase price, current value, mortgage balance, net equity, monthly net rent, and
annual cash flow. Include a note on cost-basis/appreciation strategy (e.g., hold for
stepped-up basis vs. sell) if relevant to the person's stated goals — don't assume a
strategy they haven't stated.

## 9. Net Worth
Wealth trajectory by asset class (retirement accounts, Roth, HSA, cash, real estate
equity, and an "Other Assets" line for anything else the person mentioned — gold or
other precious metals, a pension, a business interest, cryptocurrency, collectibles)
across the same year range as Phase Plan. Should sum to the Cover page's total net
worth figure in year 1. Always ask about other assets before finalizing this tab (see
SKILL.md Step 1) — a single catch-all row is usually enough unless the person wants
one of these tracked with its own growth/income assumptions, in which case give it its
own row or, for something recurring like a pension, its own line on Phase Plan too.

## 10. Mortgage Schedule
If there are multiple mortgages, one row per loan with balance, payment, payoff date,
and the monthly cash flow it frees up once paid off — useful for seeing exactly when
expenses drop.

## 11. HSA & Healthcare
HSA balance growth year over year (contributions + growth − withdrawals), plus a
healthcare cost table broken into phases (employer plan → retiree/marketplace plan →
Medicare), since this is usually the most volatile expense line in early retirement.

## 12. Action Checklist
A prioritized to-do list tied to the plan's key dates (open enrollment, mortgage
payoffs, first Roth conversion, Social Security claim dates, etc.). **Build this fresh
for each person from their own stated action items — never copy in specifics like
attorney names, case numbers, account numbers, or insurance contacts from a prior
conversation or example.** Generic category placeholders ("confirm retiree health plan
enrollment," "review estate planning documents with your attorney") are fine as a
starting checklist; specifics are the person's to fill in.

## 13. Insights Dashboard
A summary tab that pulls headline numbers from the other tabs (net worth growth,
income source mix over time, cash flow unlocked by mortgage payoffs, key milestone
dates) into one glanceable view — mostly formulas referencing cells on other tabs, plus
a few short text takeaways. Build last, once the other tabs are stable.
