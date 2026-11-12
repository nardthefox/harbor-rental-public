# Rental Property Snapshot

A short rental-property calculator from **Todd Renard, REALTOR®**, Harbor Realty and Management Group. Enter a price, rents, a simple loan and a few costs — about two minutes — and read six headline KPIs with a plain-English note on what “good” often looks like.

This page is for educational purposes; it is not a loan offer. Todd Renard is a licensed real estate agent, not a lender.

## How to open it

Open `index.html` in a browser. Everything runs on your device; no account or install is required. To serve the folder locally:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080/`.

To embed the calculator in a page (for example at toddrenard.com/rental-calculator), see `EMBED.md`.

## What’s on the page

- **Units:** buttons for 1, 2, 3 or 4 units (a house through a fourplex). **Add more units** grows the rent roll one row at a time, up to 50. Empty extra rows can be removed. FHA house hack is available only for 1–4 units; if you add a fifth unit, the loan type switches to Conventional and FHA is disabled. Conventional and DSCR terms shown for 5 or more units are example 1–4 unit residential terms, not commercial multifamily financing.
- **Loan type:** Conventional, DSCR, FHA house hack, or Cash. Choosing a type fills example down payment, rate and amortization only — clearly labeled as examples, not quotes and not an offer to lend.
- **Example APR:** shown with the example loan terms as a nominal annual percentage rate (twelve times the monthly unit-period rate), estimated from the example interest rate, points, lender fees, and any mortgage insurance, in the spirit of Regulation Z Appendix J. Property tax and homeowners insurance are not included. It is an example only — not a quote, not a closing disclosure, and not an advertised credit term. A cash purchase shows n/a.
- **Balloon after (years):** optional. Leave blank or 0 if there is no balloon. The monthly payment still uses the amortization term (for example, a 25-year amortization with a 5-year balloon). When a balloon year is set, the remaining loan balance is shown in plain English. Refinance terms are not guaranteed, and the estimate is flagged in amber.
- **Costs:** annual tax and insurance, vacancy %, an ongoing monthly maintenance + CapEx *reserve* (% of rent), management % of rent, other monthly costs, and an optional **upfront rehab / CapEx** one-time amount (default 0). The upfront amount is added to cash invested so cash-on-cash reflects it. It is not the same as the ongoing monthly reserve.
- **Six KPI cards**, each with a value, a green / amber / red rule-of-thumb rating, a one-sentence “what this means,” and a “what good looks like” line. Ratings use the same rounded figure the card displays.
- **KPIs of a successful rental** — a short educational list of the same six ideas, plus a reminder that rules of thumb vary.
- **More detail (optional, collapsed):** example closing costs, other income, an appreciation assumption, and a five-year equity snapshot.
- **Download PDF** uses the browser print dialog and a print stylesheet. It produces a 1–2 page KPI summary. Printing still works when the page is embedded in an iframe, as long as the iframe allows dialogs (see `EMBED.md`).

Example figures are pre-filled so you can see how the cards behave. FHA house hack treats unit 1 as the home you’d live in, so that unit’s rent is not counted as income. Conventional loans with less than 20% down include an example PMI rate (0.75%, dropping at 78% LTV). Cash has no mortgage, so DSCR is n/a.

## KPI bands (rules of thumb, not advice)

Green, amber and red are **general rules of thumb**. They vary by market, strategy and lender. They are not a loan decision, not a valuation, and not financial advice.

The **$100 monthly cash-flow cushion**, the **0.75% amber floor on the 1% rule**, and the **65% expense-ratio amber cap** are **teaching aids, not published industry standards**.

| KPI | Green | Amber | Red | How it’s measured here |
|---|---|---|---|---|
| Monthly cash flow | More than $100 | $0 to $100, or a small deficit down to −$100 | Below −$100 | NOI minus the monthly loan payment (P&I, MI if any) after the costs you entered |
| Cash-on-cash return | 8% or higher | 5% to under 8% | Under 5%, or negative | Annual cash flow ÷ cash invested (down payment, closing costs, points, fees, and any upfront rehab / CapEx) |
| Cap rate | 6% or higher | 4% to under 6% | Under 4% | Annual NOI ÷ purchase price |
| DSCR (rent ÷ PITIA) | 1.25× or higher | 1.00× to under 1.25× | Under 1.00× | Gross scheduled rent ÷ PITIA (how many DSCR lenders qualify). Shown to three decimals so the rating matches the displayed figure. n/a on a cash purchase |
| 1% rule | 1.00% or higher | 0.75% to under 1.00% | Under 0.75% | Monthly rent ÷ purchase price (rehab is not in this screen; it is in cash invested) |
| Expense ratio | 50% or under | Over 50% up to 65% | Over 65% | (Vacancy + operating expenses) ÷ gross potential income, in the spirit of the common “50% rule” shortcut |

### Sources

These sources support the *ranges*, not a claim that any one number is “the” correct target. Accessed 11 Nov 2026.

1. **Investopedia, “One Percent Rule”** — the 1% rule as a quick estimate that monthly rent should be about 1% of price (often including repairs); it does not account for taxes, insurance, vacancy or financing. https://www.investopedia.com/terms/o/one-percent-rule.asp
2. **BiggerPockets, “How Much Profit Should You Make on a Rental Property?”** — many commentators aim for roughly 8–12% cash-on-cash; cap rate “success” depends on the neighborhood and risk; the 1% rule is a quick screen. https://www.biggerpockets.com/blog/defining-successful-roi
3. **White Coat Investor, “5 Rules for Evaluating a Rental Property Investment”** — teaches a **55% rule**: plan for about 45% of gross rent to go to vacancy and operating costs, leaving about 55% as net operating income. A cap rate of about 6–8% is described as “pretty good,” with lower and higher figures depending on the deal. https://www.whitecoatinvestor.com/5-rules-for-evaluating-an-investment-property/

The **50% rule** (about half of rent going to vacancy and operating costs) is a separate, commonly used planning shortcut. It is not the White Coat Investor rule.

DSCR bands follow common published lender guides. Programs often start around **1.00×**, and tighter or better-priced programs around **1.20–1.25×**. Some lenders allow 0.75–0.99× at a lower LTV. These are examples of lender guides, not an offer to lend, and minimums vary by program, LTV and loan purpose:

- LoanStream Wholesale Non-QM DSCR Matrix (effective 10/08/2026): 1–4 unit investment properties only; “Select DSCR” uses a 1.25 ratio and “Core DSCR” uses a 1.00 ratio, with a lower “Sub1” band at 0.75 to under 1.00. https://loanstreamwholesale.com/wp-content/uploads/2026/10/LSM-DSCR-Matrix-dtd-10.08.26.pdf
- CW Lending DSCR 1 Program Matrix (Oct 5, 2026): on purchase loans, a 1.20 minimum applies at higher LTVs (for example 1.20 at 80% LTV); 1.00 appears at lower LTVs. Do not read this as a flat 1.00 minimum — purchase loans are often 1.20× or higher. https://www.cwlend.com/contentimages/1457895694/CWL__DSCR_1_Program_Matrix__10.05.2026__v17.pdf

## Privacy and branding

The page makes no network calls and uses no analytics, cookies or form posts. Fonts are system stacks (Georgia for headings, Helvetica / Arial for body) so the file can be embedded without third-party font requests. Optional saving uses `localStorage` on this device only, under the key `harbor-rental-snapshot-v1`. **Clear my data** removes only that key and restores the examples.

Branding is **Todd Renard, REALTOR®** and Harbor Realty and Management Group, with his cell and toddrenard.com in the footer. Visual language follows the cream-and-sienna realtor-side palette: page `#F7F1E8`, sienna `#A0522D` / `#8B3E1A`, ink `#2B2420`.

Disclaimer, shown on the page and on the PDF:

> Estimates only, not a rate quote, loan approval, tax or financial advice. Confirm terms with a lender and tax advisor.

> For educational purposes; not a loan offer. Todd Renard is a licensed real estate agent, not a lender.

Example rates, down payments and fees are not advertised rates or payments.

## Limits

The Example APR is an estimate from the figures on the page, not a Truth-in-Lending disclosure and not a quote. The calculator does not model capital-gains tax, depreciation recapture, prepayment-penalty dollars, or the FHA self-sufficiency test as a formula. The 1% rule on this page is rent ÷ price, which is the common public definition. Cash invested still includes any upfront rehab / CapEx you enter. A balloon balance is an estimate of principal still owed at that year; it does not change the monthly payment, and refinance terms are not guaranteed.
