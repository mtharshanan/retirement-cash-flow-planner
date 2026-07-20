---
name: retirement-cash-flow-planner
description: Build a personalized multi-decade retirement financial plan — phased after-tax cash flow projections, a Roth conversion strategy, a federal + state tax calculator, and a net worth trajectory — as an Excel workbook tailored to the person's own dates, balances, and goals. Use this whenever someone wants to plan retirement timing, model retirement income/expenses, plan Roth conversions, estimate retirement taxes, or asks for a "retirement plan," "retirement model," or "retirement spreadsheet." Always gather the person's own numbers first — never reuse another person's figures or dates.
---

# Retirement Cash Flow Planner

Builds a full, personalized retirement financial model as an Excel workbook: phased
after-tax cash flow, a Roth conversion ladder, a tax calculator, and a net worth
projection — all driven by formulas off one Assumptions tab, so the whole model
recalculates when any input changes.

**Every workbook this skill produces must be built from that specific person's own
numbers.** `assets/retirement-plan-template.xlsx` is a *structural* starting point with
a fictional example household — it exists to show the tab layout, formula patterns, and
formatting conventions, not to be handed to a user with someone else's numbers still in
it. Never carry over another person's dates, balances, or account details from a prior
conversation or from the template into a new person's workbook.

## Before building anything: read the skill's own template

Open `assets/retirement-plan-template.xlsx` and `references/workbook-architecture.md`
first, even if you think you remember the layout — the exact cell coordinates matter
because every downstream tab references the Assumptions tab by cell address.

## Step 1 — Gather assumptions

**Before building anything, ask ALL four of the following in a single upfront
message — not just filing status, not split across several turns, and not skipped
because the person only gave you a balance and a timeline.** Treat this as a fixed
checklist: every item below must be asked, even if you expect a common answer (e.g.
"just testing" or "single"). Do not infer or default any of these:

1. **Real plan or test/placeholder?** — if it's a real plan, everything below needs
   their actual numbers; if it's a test, fictional numbers are fine but still ask the
   remaining three items so the demo reflects what a real user would be asked.
2. **Marital/filing status** — single or married filing jointly? (Changes tax
   brackets, standard deduction, and whether there's a second Social Security benefit
   and a second set of account balances to model.)
3. **Dependents and real estate** — any dependents (and until when do they affect
   shared expenses/benefits), and any rental or investment properties beyond a
   primary residence? (Real estate triggers a Properties tab — see
   `references/workbook-architecture.md`.)
4. **Other assets** — anything outside retirement/brokerage accounts worth including,
   e.g. gold or other precious metals, a business interest, a pension, cryptocurrency,
   collectibles? These don't all need their own tab, but should at least be captured
   on Net Worth so the total picture isn't understated.

Ask all four together, e.g.: "Quick check before I build this — (1) is this a real
plan or a test run with placeholder numbers, (2) married filing jointly or single,
(3) any dependents or real estate beyond a primary residence, and (4) any other
assets like gold, a pension, or a business interest I should include?" **Getting an
answer to question 1 or 2 is not a reason to stop asking 3 and 4** — a short prompt
that only gives a balance and a timeline is exactly the case most likely to be
missing dependents/real estate/other-assets information, and answering the first
question or two does not waive the rest.

Once household shape and assets are confirmed, interview for (or use numbers already
given for) at least:

- **Personal:** retirement date, both spouses' birth month/year (or single filer),
  dependents and when they age off any shared benefit, life expectancy/planning
  horizon, Social Security claim ages, 59½ / Medicare / RMD dates
- **Income (final working year):** salary, bonus, retirement plan contributions, any
  deferred compensation (balance + payout schedule)
- **Expenses:** current monthly living expenses, expected inflation rate, healthcare
  cost by phase (employer → retiree/marketplace → Medicare)
- **Accounts:** balances and growth-rate assumptions for each 401(k)/403(b)/IRA, HSA,
  cash savings, and (if relevant) rental, other-asset, or recurring income
- **Roth strategy:** target annual conversion amount and which account to convert first
  (usually the larger or the one with worse RMD exposure)
- **Tax:** filing status and state — use current-year federal brackets and the
  relevant state's brackets (these are public data; look them up rather than reusing
  the template's example numbers, which go stale every year)

If the person hasn't given you enough to fill in a section, ask — don't invent
plausible-sounding numbers and don't silently reuse figures from an earlier
conversation about a different person.

## Step 2 — Build the workbook

Copy `assets/retirement-plan-template.xlsx` as your starting point, or build fresh
following `references/workbook-architecture.md` if the person's situation needs a
different tab set (e.g., multiple rental properties, a pension, a business sale).
Either way:

1. Replace every value in **Assumptions** with the person's real inputs. Nothing from
   the template's example household should remain.
2. Extend or shorten the year range in **Phase Plan** / **Tax Calculator** /
   **Roth Conversion** / **Net Worth** to run from the actual retirement year through
   the end of the planning horizon (life expectancy), not just the illustrative 10
   years in the starter file.
3. Add tabs the person's situation calls for that aren't in the starter file —
   see `references/workbook-architecture.md` for the full 13-tab pattern the original
   framework this skill is based on used (Properties, Mortgage Schedule, HSA &
   Healthcare tracker, a Cover-page milestone summary, etc.). Only build what's
   relevant; an empty-nester renter doesn't need a Properties tab.
4. Follow the `xlsx` skill's conventions throughout: formulas not hardcoded results,
   blue text for hardcoded inputs, yellow fill for cells the person should update
   annually, currency/percent number formats, and a legend if you leave any cells for
   the person to fill in themselves.
5. **Never hand-copy an Action Checklist, attorney contacts, account numbers, or any
   other person's real identifying detail into a new workbook** — those sections, if
   built at all, should be generated fresh for the current person from their own
   stated action items.

## Step 3 — Recalculate and verify

Run `recalc.py` (from the `xlsx` skill) until `total_errors: 0`. Then spot-check that
totals in Phase Plan flow into Tax Calculator and Net Worth correctly — an off-by-one
cell reference is the most common failure mode in a multi-tab linked model like this.

## The six-phase framework

The cash-flow logic this skill encodes generalizes to most retirement timelines:

- **Phase 1 — Bridge year(s):** the gap between the last paycheck and any deferred
  comp, pension, or Social Security starting. Usually funded from cash savings or
  early 401(k) withdrawals (if past 59½) — this is typically the single best Roth
  conversion window, since taxable income is at its lowest.
- **Phase 2 — Stabilizing:** deferred income sources ramp down; mortgages or other
  fixed obligations start getting paid off, freeing up cash flow.
- **Phase 3 — Approaching self-funding:** major debt payoff (e.g., the primary
  mortgage) meaningfully reduces the expense side of the model.
- **Phase 4 — Pre-Social-Security:** the years right before claiming SS, if the
  person is delaying to increase the benefit — still a strong Roth conversion window.
- **Phase 5 — Social Security / Medicare begins:** taxable income rises with SS
  benefits (up to 85% federally taxable); Roth conversion room narrows.
- **Phase 6 — RMDs / legacy:** once Required Minimum Distributions begin, conversion
  opportunity mostly closes; the focus shifts to managing RMD tax impact and any
  estate/legacy planning.

Not every plan needs all six phases modeled explicitly — collapse or expand them to
fit the person's actual timeline.

## Reference files

- `references/workbook-architecture.md` — full tab-by-tab layout (13-tab pattern),
  what each tab computes, and the formula relationships between tabs. Read this before
  extending the starter template or building a tab it doesn't include.
- `assets/retirement-plan-template.xlsx` — starter workbook (Cover, Assumptions, Phase
  Plan, Tax Calculator, Roth Conversion, Net Worth) with a fictional example household
  and working formulas throughout.
