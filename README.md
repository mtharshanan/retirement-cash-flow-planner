# Retirement Cash Flow Planner

A Claude plugin that builds a personalized, multi-decade retirement financial plan as
an Excel workbook — phased after-tax cash flow, a Roth conversion strategy, a federal +
state tax calculator, and a net worth projection, all driven by formulas so the model
recalculates when any input changes.

## What it does

Ask Claude to build your retirement plan, and this plugin's skill will:

1. Interview you for your own dates, balances, income, and expenses (never reuses
   anyone else's numbers)
2. Build an Excel workbook from a proven template: Cover, Assumptions, Phase Plan,
   Tax Calculator, Roth Conversion, and Net Worth tabs
3. Extend the model with additional tabs (rental properties, multiple mortgages, an
   HSA/healthcare tracker) when your situation calls for them
4. Verify every formula recalculates cleanly before handing you the file

## The six-phase framework

The cash-flow logic generalizes to most retirement timelines: a bridge year before
other income sources start, a stabilizing period as fixed obligations get paid off,
approaching self-funding once major debt clears, a pre-Social-Security window (often
the best years for Roth conversions), Social Security/Medicare beginning, and finally
the RMD/legacy phase.

## Installation

```
/plugin marketplace add mtharshanan/retirement-cash-flow-planner
/plugin install retirement-cash-flow-planner
```

Or install directly from the Claude directory once listed.

## Usage

Just ask, e.g.:

> "Build me a retirement plan — I'm planning to retire in 2030, here are my account
> balances and expenses..."

Claude will interview you for anything missing and produce a downloadable `.xlsx`.

## License

MIT — see [LICENSE](LICENSE).
