# Vaulta Pay Model — Next Session Prompt
**Copy and paste this entire prompt to start the next session.**

---

## Project Summary
A standalone interactive HTML financial model + investor pitch deck for **VaultaPay** — a closed-loop digital wallet using vUSD (1 vUSD = $1 USD) on Solana devnet. Consumers pay merchants via QR code, earn Vaulta Rewards every 90 days. No bank account required.

## Repository
- **GitHub:** https://github.com/moazzamkhoja/Vaulta-Pay-Model (public)
- **GitHub Pages (if enabled):** https://moazzamkhoja.github.io/Vaulta-Pay-Model/
- **Local path:** `C:\Projects\Vaulta-Pay-Model\`
- **Files:** `index.html` (model + benchmarks + pitch tabs), `pitch-embed.html` (8-slide pitch deck)

> ⚠️ There is a **separate** app repo at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`). Do NOT make model changes there. The stale `model/` subfolder inside that repo has been deleted.

## Current State (Session 19)
The model is a single-file HTML app with three tabs:

### Tab 1 — 📊 Financial Model
Interactive 10-year DCF model. Sidebar has sliders; all KPIs and charts update instantly.

**Sliders (with default values):**
| ID | Label | Default |
|---|---|---|
| `i_wallet` | Avg Wallet Balance | $2,800 |
| `i_txnrate` | Monthly Transaction Rate | 20% |
| `i_mfee` | Merchant Fee Rate | 0.80% |
| `i_cac` | Base CAC (Seed) | $60 |
| `i_sleeve` | Consumer Sleeve (Vaulta keeps) | 20% |
| `i_tbrate` | T-Bill Annual Rate | 4.8% |
| `i_msleeve` | Merchant Sleeve % | 25% |
| `i_ssgrowth` | Steady-State Growth (Yr7+) | 25% |
| `i_serBraise` | Series B Raise | $15M |
| `i_seedbuf` | Seed Contingency Buffer | 20% |
| `i_wacc` | WACC | 20% |
| `i_exitm` | Exit EBITDA Multiple | 10x |
| `i_survival` | Survival Probability | 35% |
| `i_sal_eng` | Engineering salary | $150,000 |
| `i_sal_bd` | Business Dev salary | $120,000 |
| *(+ more salary inputs)* | CS, Legal, Lead, Cyber | various |

**Consumer targets (number inputs):**
- Seed: 1,000 | Series A: 25,000 | Series B: 500,000

**Revenue model:**
- T-bill gross = `cons × wallet × tbDeploy × tbRate` (tbDeploy hardcoded = 1.0 per GENIUS Act)
- Merchant fee = `cons × wallet × txnRate × mFeeRate × 12`
- Merchant T-bill sleeve = `merchants × mSettle × tbDeploy × tbRate × mSleeve`
- COGS = T-bill consumer payout `(1 - cSleeve)` + infra var + merchant T-bill payout
- Opex = payroll + mktg + referrals + infra fixed + G&A + legal retainer + KYC + FCC (Yr2 only)
- CAC: paid acquisition only — `baseCAC × cacTap(yr)` where cacTap declines 1.0→0.4 over phases
- Referrals: tracked separately in opex as `cons × 1.5% × $5 × 12`

**Key computed outputs (returned from `model()`):**
`cons[], phases[], merch, totalRev, grossProfit, ebitda, opex, monthlyTbill, vaultSlv, consRwd, mFeeMo, netContrib, netAnnual, ltv3, ltvCac, cacPayback, effYield, seedRaise, serARaise, serBRaise, totalRaised, EV, raEV, beYear, baseCAC, varInfra`

### Tab 2 — 📐 Benchmarks
All VaultaPay cells are **live-linked to model sliders**. Three sections:

**Unit Economics** (vs Chime, Revolut, Cash App, MoneyLion):
- LTV:CAC (`bm_ltvcac`), CAC (`bm_cac`), Annual Net ARPU (`bm_arpu`), CAC Payback (`bm_payback`)

**Revenue Model** (vs PayPal, Square/Block, Stripe, Interchange Avg):
- Merchant Fee Rate (`bm_mfee`), Gross Margin (`bm_gm`), EBITDA Margin (`bm_ebitda_margin`)

**EBITDA Margin 10-Year Trend (2016–2025):**
- VaultaPay Yr1–5 targets (`bm_eb_yr1` through `bm_eb_yr5`) — live from model
- PayPal: 19–22% (stable, 10 years of data from 10-K)
- Block/Square: -7.8% (2016) → +3.9% (2025); margins suppressed by Bitcoin gross revenue
- Stripe: private; negative through 2022, ~breakeven 2023, ~2% in 2024, ~17% in 2025
- Visa: 63–69% (network economics — shown as ceiling, not a direct comp)

**Growth & Scale** (vs Chime, Revolut, Cash App, Robinhood):
- EBITDA Positive year (`bm_breakeven`), 3-Year LTV (`bm_ltv`)

### Tab 3 — 🎯 Investor Pitch
Full-screen iframe loading `pitch-embed.html`. 8-slide seed deck:
1. Cover — VaultaPay / $2M Seed
2. Problem — unbanked/underbanked, high payment fees
3. Solution — closed-loop vUSD wallet
4. How It Works — CSS phone mockups, QR flow
5. Market — TAM/SAM/SOM
6. Business Model — T-bill sleeve + merchant fees
7. Traction — metrics
8. The Ask — $2M at $8M pre-money, 20% equity, $10M post-money

Navigation: ← → keyboard arrows + dot clicks.

## Architecture Notes
- **Single file** `index.html` — no build step, no npm, no bundler
- **Tab switching:** `switchTab(name)` — toggles `.tab-panel.active`, matches button text
- **Pitch tab:** `#tab-pitch` is `position:fixed; inset:90px 0 0 0` (sits above header height)
- **Chart.js 4.4.0** loaded from CDN for P&L bar chart and consumer growth chart
- **Color palette:** `--navy:#1F4E79`, `--blue:#2E75B6`, `--ltblue:#BDD7EE`, `--green:#70AD47`, `--orange:#ED7D31`
- **Strict rule:** NEVER use "yield", "interest", "APY" — always "Vaulta Rewards", "cycle reward rate", "estimated reward"

## How to Edit & Deploy
```
# Edit locally
C:\Projects\Vaulta-Pay-Model\index.html   ← main file
C:\Projects\Vaulta-Pay-Model\pitch-embed.html  ← pitch deck

# Commit and push
cd C:\Projects\Vaulta-Pay-Model
git add index.html pitch-embed.html
git commit -m "your message"
git push origin main
```
GitHub Pages auto-deploys from `main` branch root (if Pages is enabled).

## GitHub Pages Setup (if not yet enabled)
1. Go to: https://github.com/moazzamkhoja/Vaulta-Pay-Model/settings/pages
2. Source → Deploy from a branch → `main` / `/ (root)` → Save
3. Live URL: https://moazzamkhoja.github.io/Vaulta-Pay-Model/

## Pending / Possible Next Steps
- Confirm GitHub Pages is live and test all three tabs on the hosted URL
- Add Vaulta Rewards rate to Benchmarks tab (consumer reward % vs competitor loyalty programs)
- Add a "Funding Schedule" view showing seed / Series A / Series B raise amounts from the model
- Possibly add a sensitivity table (2D: wallet size × merchant fee rate → EBITDA margin)
- Consumer ACH withdrawal screen (in the mobile app — separate repo)

## Commit History Summary
| Commit | What changed |
|---|---|
| `42e935a` | EBITDA margin row + 10-year trend table in Benchmarks |
| `e2230b7` | Investor Pitch tab (pitch-embed.html, 8 slides) |
| `da9699b` | Split Series A into Operations + Regulatory Capital in Funding Schedule |
| `48edac2` | Benchmarks tab — live VaultaPay column vs Chime/Revolut/CashApp/MoneyLion/Stripe |
| `0807b86` | Fix duplicate benefits constant bug |
| `863d116` | Live Headcount & Salaries section |
| `c264f6f` | T-bill allocation hardcoded to 100% (GENIUS Act) |
| `15d6079` | Seed contingency buffer slider |
| `e416d73` | Transaction rate moved to primary levers; consumer sleeve max 80% |
| `d26e5a5` | Fix merchant T-bill double-counting bug |

## Related Repo
The **mobile app** lives at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`, private). See `C:\Projects\Vaulta\NEXT_SESSION_PROMPT.md` for app session state. The two repos are independent — do not mix them.
