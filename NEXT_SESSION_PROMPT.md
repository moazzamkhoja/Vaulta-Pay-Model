# Vaulta Pay Model — Next Session Prompt
**Copy and paste this entire prompt to start the next session.**

---

## Project Summary
A standalone interactive HTML financial model + investor pitch deck for **VaultaPay** — a closed-loop digital wallet using vUSD (1 vUSD = $1 USD) on Solana devnet. Consumers pay merchants via QR code, earn Vaulta Rewards every 90 days. No bank account required.

## Repository
- **GitHub:** https://github.com/moazzamkhoja/Vaulta-Pay-Model (public)
- **GitHub Pages:** https://moazzamkhoja.github.io/Vaulta-Pay-Model/
- **Owner link (Save as Default button visible):** https://moazzamkhoja.github.io/Vaulta-Pay-Model/?owner=1
- **Local path:** `C:\Projects\Vaulta-Pay-Model\`
- **Files:** `index.html` (model + benchmarks + pitch tabs), `pitch-embed.html` (14-slide pitch deck)

> ⚠️ There is a **separate** app repo at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`). Do NOT make model changes there.

## Current State (Session 20)

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
| `i_sal_cs` | CS salary | $57,000 |
| `i_sal_lead` | Lead salary | $112,000 |
| `i_sal_legal` | Legal salary | $135,000 |
| `i_sal_cyber` | Cyber salary | $190,000 |
| `i_benefits` | Benefits % | 25% |

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

**Save as Default feature:**
- Button hidden unless `?owner=1` in URL — only Moazzam sees it
- On click: saves all 23 slider/input values to `localStorage` under key `vaultapay_defaults`
- On load with `?owner=1`: reads localStorage and pre-fills inputs
- Investors use the plain URL — always see hardcoded defaults, no save button

### Tab 2 — 📐 Benchmarks
All VaultaPay cells are **live-linked to model sliders**. Three sections:

**Unit Economics** (vs Chime, Revolut, Cash App, MoneyLion):
- LTV:CAC (`bm_ltvcac`), CAC (`bm_cac`), Annual Net ARPU (`bm_arpu`), CAC Payback (`bm_payback`)

**Revenue Model** (vs PayPal, Square/Block, Stripe, Interchange Avg):
- Merchant Fee Rate (`bm_mfee`), Gross Margin (`bm_gm`), EBITDA Margin (`bm_ebitda_margin`)

**EBITDA Margin 10-Year Trend (2016–2025):**
- VaultaPay Yr1–5 targets (`bm_eb_yr1` through `bm_eb_yr5`) — live from model

### Tab 3 — 🎯 Investor Pitch
Full-screen iframe loading `pitch-embed.html`. **14-slide** seed deck (rebuilt Session 20):

| # | Slide | Notes |
|---|---|---|
| 1 | Cover | $2M / $8M pre / $10M post |
| 2 | Problem | 3 cards: checking earns nothing, merchant fees, unbanked |
| 3 | Solution | Side-by-side: 4-layer banking vs Solana; GENIUS Act + Solana explainers |
| 4 | Why Now | GENIUS Act, CLARITY Act, Solana speed, consumer demand |
| 5 | Consumer Flow | KYC → Load (ACH/cash) → QR Pay → Rewards after 3 txns |
| 6 | Merchant Flow + T-Bill | KYB → accept → settle → rewards after 30 txns; T-bill 80/20 split diagram |
| 7 | Market | Bottom-up bar sizing, TAM/SAM/SOM |
| 8 | Benchmarks | **Live-linked** to model via postMessage |
| 9 | Business Model | Consumer + merchant value, revenue streams, live unit economics |
| 10 | Competition | 7-feature table vs Venmo/Cash App/Zelle/Chime/Apple Pay |
| 11 | GTM | Placeholder |
| 12 | Team | Placeholder |
| 13 | Traction + Seed Plan | Current state + 3 seed goals (prod app, 500-store LOI, 1K consumers) |
| 14 | The Ask | $2M, dilution path Seed→A→B, return scenarios $50M–$500M exit |

**Dynamic link (postMessage):**
- iframe signals parent with `{ type: 'pitchReady' }` when loaded
- parent calls `sendPitchData()` immediately on receiving pitchReady (no timeout)
- `sendPitchData()` also called from `update()` if pitch tab is active
- Fields sent: `ltvCac, cac, arpu, payback, mfee, gm, ebitda3, ltv3, mfee_mo, tbill_mo, contrib, beYear`
- Dynamic IDs in pitch deck: `bm_ltvcac, bm_cac, bm_arpu, bm_payback, bm_mfee, bm_gm, bm_ebitda3, ue_cac, ue_ltv, ue_ltvcac, ue_payback, ue_mfee_mo, ue_tbill_mo, ue_contrib, be_year, s3_mfee, s6_mfee`

**Navigation:** ← → keyboard arrows + dot clicks (14 dots).

## Architecture Notes
- **Single file** `index.html` — no build step, no npm, no bundler
- **Tab switching:** `switchTab(name)` — toggles `.tab-panel.active`
- **Pitch tab:** `#tab-pitch` is `position:fixed; inset:90px 0 0 0`; iframe has `id="pitch-iframe"`
- **Chart.js 4.4.0** loaded from CDN
- **Color palette (index.html):** `--navy:#1F4E79`, `--blue:#2E75B6`, `--ltblue:#BDD7EE`, `--green:#70AD47`, `--orange:#ED7D31`
- **Color palette (pitch-embed.html):** `--navy:#0A2540`, `--green:#00C896`, `--light:#F5F7FA`
- **Strict rule:** NEVER use "yield", "interest", "APY" — always "Vaulta Rewards", "cycle reward rate", "estimated reward"

## ⚠️ Known Issue to Fix Next Session
**Slide 3 (Solution) overflow** — the two-column comparison layout is too tall for the viewport on typical screens. The nav bar dots overlap content at the bottom. Need to redesign slide 3 layout to be more compact — options:
- Horizontal comparison table instead of two vertical flow-chain columns
- Reduce the number of metric rows shown
- Make the flow chains horizontal rather than vertical

Previous attempt to fix by reducing padding/font-sizes made the visual quality worse. Approach should be a **layout change**, not just size reduction.

**To verify fixes visually:** A `.claude/launch.json` exists at `C:\Projects\Vaulta-Pay-Model\.claude\launch.json` — use `preview_start("vaultapay")` then navigate to `http://localhost:5174/pitch-embed.html`, call `goTo(2)` in eval to jump to slide 3, then `preview_screenshot()` to verify before committing.

## How to Edit & Deploy
```
# Edit locally
C:\Projects\Vaulta-Pay-Model\index.html        ← main file
C:\Projects\Vaulta-Pay-Model\pitch-embed.html  ← pitch deck

# Commit and push
cd C:\Projects\Vaulta-Pay-Model
git add index.html pitch-embed.html
git commit -m "your message"
git push origin main
```
GitHub Pages auto-deploys from `main` branch root.

## Commit History Summary (recent)
| Commit | What changed |
|---|---|
| `2c1bd0f` | Fix slide overflow attempt + pitchReady handshake for dynamic updates |
| `70357a8` | Save defaults to localStorage, keep URL clean as just ?owner=1 |
| `14daaac` | Restore owner-only save button (hidden without ?owner=1) |
| `439d93e` | Rebuild pitch deck: 14 slides, blockchain narrative, dynamic benchmarks |
| `42e935a` | EBITDA margin row + 10-year trend table in Benchmarks |
| `e2230b7` | Investor Pitch tab (pitch-embed.html, 8 slides) |
| `d26e5a5` | Fix merchant T-bill double-counting bug |

## Pending / Possible Next Steps
- **Fix slide 3 overflow (priority)** — layout redesign, not font reduction
- Confirm GitHub Pages is live and test all 14 slides on hosted URL
- Add Vaulta Rewards rate to Benchmarks tab (consumer reward % vs competitor loyalty)
- Add a "Funding Schedule" view showing seed / Series A / Series B raise amounts
- Sensitivity table (2D: wallet size × merchant fee rate → EBITDA margin)
- Consumer ACH withdrawal screen (separate app repo `C:\Projects\Vaulta`)

## Related Repo
The **mobile app** lives at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`, private). See `C:\Projects\Vaulta\NEXT_SESSION_PROMPT.md` for app session state. The two repos are independent — do not mix them.
