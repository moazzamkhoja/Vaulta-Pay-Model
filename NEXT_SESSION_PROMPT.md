# VaultaPay Financial Model — Session State (v7, Bill-Pay Segmented)
**Copy/paste this to start the next session.**

---

## What VaultaPay is
A standalone interactive HTML financial model for **VaultaPay** — a **blockchain bill-pay portal** (vUSD on Solana, 1 vUSD = $1). Consumers pay **rent + utilities** (and P2P) through the app; **merchants are apartment operators and utilities**. Free to the consumer; the **merchant pays a flat fee**. Revenue = transaction fees + float (T-bill income on balances, net of Vaulta Rewards). P2P is free.

> Strict wording rule: never "yield/interest/APY" → always "Vaulta Rewards", "T-bill float", "estimated reward".

## Repo / deploy
- Local: `C:\Projects\Vaulta-Pay-Model\`
- GitHub Pages: https://moazzamkhoja.github.io/Vaulta-Pay-Model/ (deploys from `main` root)
- Files: `index.html` (model — 4 tabs), `pitch-embed.html` (pitch deck — STILL OLD narrative)
- Old debit-card model archived: `index-debit-v5.html`, `pitch-embed-debit-v5.html`, git tag `v5-debit-model`
- Separate app repo (do NOT touch from here): `C:\Projects\Vaulta`

## index.html tabs
1. **📊 Model** — sidebar levers (reordered by importance) + KPIs + charts + funding schedule + P&L-by-year + per-consumer detail.
2. **📒 Financials** — line-item P&L (net-revenue), Headcount by Function, Seed Use of Funds.
3. **📐 Benchmarks** — STILL OLD competitors (Chime/Revolut/PayPal). Needs rework to bill-pay comps.
4. **🎯 Investor Pitch** — iframe to `pitch-embed.html`. STILL OLD narrative. Needs rework.

## The engine (`model()` in index.html)
- **Growth = deal targets per round, per segment** (NOT a growth rate). BD headcount is *derived* = new deals ÷ deals-per-BD. Customers = cumulative merchants × customers/merchant × **adoption**.
  - Round lengths: Seed 1yr (yr1), Ser A 2yr (yr2-3), Ser B 3yr (yr4-6), Steady 4yr (yr7-10). Deals spread evenly within a round.
- **Revenue (NET presentation, bank/fintech style):** transaction fees + net float (the sleeve Vaulta keeps). Gross T-bill income & Vaulta Rewards shown as memo only.
- **COGS:** variable infra only ($0.50/customer/mo). Gross margin ~93%.
- **Opex:** payroll (engineering, CS, other=legal/leadership/cyber) + sales/BD + **customer activation** + **brand marketing** + referrals + fixed infra + **G&A (% of rev, incl. compliance)** + legal retainer + KYC.
- **CAC = (sales/BD + activation) ÷ new customers.** Brand marketing is OPEX, NOT in CAC (it serves the whole base). Adding enterprise deals now *lowers* CAC; higher adoption *lowers* CAC.
- **LTV = 3-yr, churn-adjusted, NPV at WACC** (end-of-year): Σ netAnnual·(1−churn)^(t−1)/(1+WACC)^t.
- **Round sizing = phase net burn × (1+buffer).** Profitable phase → $0 (Series B currently $0). Regulatory capital ($6M GENIUS Act reserve) is a **balance-sheet** raise at Series A — excluded from P&L.
- **Headcount:** Engineering fixed phase ramp 4/8/15/25 (AI-leveraged). CS = customers/30,000. Compliance/AML headcount shown but cost carried in G&A. `custPerEmp` sanity metric (benchmark Chime ~8,200 / Revolut ~3,500).

## Sidebar lever order (by importance) + default values
1. **Fees** — Merchant Fee/payment **$2.00**, Consumer Fee **$0.00** (both flat, min 0)
2. **Deal Targets (per round)** — Local **5/15/45/120**, Enterprise **0/2/8/20**
3. **Balances/Float/Retention** — Merchant retention **25%**, Consumer retained balance **$1,500**, Float sleeve **20%**, Adoption **50%**
4. **Marketing & G&A** — Brand marketing **8% of rev**, Customer activation **$25/new cust**, G&A **10% of rev ($400k floor)**
5. **Consumer Inflow** — Monthly inflow **$4,500**, Bill-payment **33% of inflow**
6. **Segment Economics** — Local 200 cust/merch, 8 deals/BD, $80k; Enterprise 50,000 cust/merch, 2 deals/BD, $200k
7. **Churn/Rates/Funding** — Consumer churn **20%**, Merchant churn **8%**, T-bill **3.7%**, Buffer **20%**
8. **Valuation** — WACC **20%**, Exit **10×**, Survival **35%**
9. **Headcount & Salaries** — eng $150k, CS $57k, lead $112k, legal $135k, cyber $190k, benefits 25%

## Current default outputs (sanity check)
EV **$53.4M** · risk-adj EV **$12.2M** · LTV **$140** · **LTV:CAC 3.78×** · CAC **$37** · payback 5.6mo · **break-even Year 4** · Rev Yr10 **$53M** · EBITDA Yr10 **$28M (93% GM)** · 617k customers · 171 merchants · 64 employees (9,636 cust/emp). Funding: Seed **$2.06M**, Series A **$2.69M ops + $6M reg capital**, Series B **$0** (profitable by then).
Seed use-of-funds: ~$0.75M engineering (4 FTE) + $0.4M G&A/compliance + ~$0.5M other people + ~$0.1M sales + infra/legal/activation, net of Yr-1 revenue, + 20% buffer.

## Research captured (for the pitch)
- **Competitor fees:** rent convenience fee $2–$3.95 flat ACH / 2.95–3.5% card (tenant pays); Bilt free-to-renter, landlord pays 0.6–0.9%; Doxo $3–4 or $5.99/mo; Plastiq 2.9–2.99%; utilities $1.95–$2.95; true ACH cost $0.26–0.50. Property pays ~$0/txn + SaaS $1.40–5/unit/mo.
- **Adoption benchmarks:** ~30% baseline no-app → 60–80% with app+activation (Zego 60%+, Lincoln 72%) → 96% best-in-class; 97% of renters prefer online (NMHC).
- **TAM:** ~52k community water systems + ~3k electric + ~1.4k gas utilities; apartment ops Greystar ~800k units, NMHC Top 50 = ~20% of US units.
- **CAC/efficiency:** Chime ~8,230 cust/employee; one enterprise deal (50k units, 50% adoption) ≈ $3.5M gross rev / $2M gross profit per year.
- **G&A** McKinsey top performers 3–5% of rev; **marketing** Chime ~31% of rev (pure-D2C; we're leaner B2B2C).

## Restore points / git
- Pre-pivot debit model: tag `v5-debit-model` (commit 14c9196), live at `index-debit-v5.html`.
- Bill-pay v6 engine: commit `bf2af23`.
- This session (v7: segmentation, deal-targets, adoption, Financials tab, G&A%, marketing/CAC split, net-revenue, sidebar reorder, Seed use-of-funds) — see latest commit.

## Pending / next steps
- **Rework Benchmarks tab** to bill-pay comps (Bilt, Doxo, Zego, Paymentus, RentPayment) — drop Chime/PayPal framing.
- **Rework pitch deck** (`pitch-embed.html`) to the bill-pay narrative; postMessage payload still carries old keys.
- Consider: marketing→adoption uplift curve (discussed, not built); enterprise CPM (50k is conservative — EQR 83k, Greystar 800k).
- Prototype changes live in separate `C:\Projects\Vaulta` repo.

## Preview workflow
Static server: `python -m http.server 4399 --directory "C:\Projects\Vaulta-Pay-Model"`; open `http://localhost:4399/index.html`. `preview_screenshot` times out — use `preview_eval` to read DOM/run `model()`.
