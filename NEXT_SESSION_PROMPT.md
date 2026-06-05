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
- **Files:** `index.html` (model + benchmarks + pitch tabs), `pitch-embed.html` (13-slide pitch deck)

> ⚠️ There is a **separate** app repo at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`). Do NOT make model changes there.

## Current State (Session 22)

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

**Unit economics strip (Tab 1):**
- Added: **Vaulta Reward per $ Spent** = `consRwd / (wallet × txnRate)` (monthly reward ÷ monthly spend)
- Removed: Annual Net ARPU box

**postMessage payload (index.html → pitch-embed.html):**
```js
{ ltvCac, cac, arpu, payback, mfee, gm, ebitda3 (Yr10), ltv3,
  mfee_mo, tbill_mo, contrib, beYear, effYield, serARaise }
```
- `ebitda3` now calculated from **Year 10** (not Year 3) EBITDA margin
- `serARaise` dynamically calculated from model burn/ramp

### Tab 2 — 📐 Benchmarks
All VaultaPay cells are live-linked to model sliders.

### Tab 3 — 🎯 Investor Pitch
Full-screen iframe loading `pitch-embed.html`. **13 slides** (Business Model slide removed in Session 22).

| # | Slide | Notes |
|---|---|---|
| 1 | Cover | $2M / $8M pre / $10M post |
| 2 | Problem | 3 cards: checking earns nothing, merchant fees, unbanked |
| 3 | Solution | Two-column: banking layers vs Solana; GENIUS Act explainer |
| 4 | Why Now | 2×2 grid: GENIUS Act, CLARITY Act, Solana, Consumer demand |
| 5 | Consumer Flow | 4 phone screenshots: KYC → Load → QR Pay → Rewards (190×380px frames) |
| 6 | Merchant Flow | 4 phone screenshots: KYB → Accept → Settle → Earn Rewards (same layout as slide 5) |
| 7 | Market | **NEW**: Two-market collision story — Traditional Payments ($187B fees) × Stablecoin Economy ($300B+) → VaultaPay bridge |
| 8 | Benchmarks | Unit Economics + Revenue Model + Funding Rounds tables, all live-linked |
| 9 | Competition | 7-feature table vs Venmo/Cash App/Zelle/Chime/Apple Pay |
| 10 | GTM | Placeholder |
| 11 | Team | Placeholder |
| 12 | Traction + Seed Plan | "Where We Are Today" (larger font) + 3 seed goals |
| 13 | The Ask | $2M, dilution path (comp-avg: Series A 20%, Series B 16%), return scenarios |

**Dynamic IDs in pitch deck (postMessage):**
```
bm_ltvcac, bm_cac, bm_arpu, bm_payback, bm_mfee, bm_gm, bm_ebitda3,
ue_cac, ue_ltv, ue_ltvcac, ue_payback, ue_mfee_mo, ue_tbill_mo, ue_contrib,
be_year, s3_mfee, s3_mfee2, s4_eff_yield, s4_eff_yield_stat,
s6_mfee, s7_mfee, s7_mfee2, s7_rev_potential, fund_serA
```

**Navigation:** ← → keyboard arrows + dot clicks (13 dots, auto-generated from `slides.length`).

## Slide 5 & 6 — Phone Screenshots

**CSS (same for both slides):**
```css
.hiw-phone { width: 190px; height: 380px; border-radius: 22px; overflow: hidden; }
.hiw-phone img { width: 100%; height: 100%; object-fit: cover; object-position: top center; }
```

**Key insight:** Original tall images (1179×2556) scale by WIDTH in object-fit:cover → full screen width shown, no horizontal clipping. Cropped/shorter images cause horizontal clipping — do NOT crop these images.

**Image files (all in repo root):**
| File | Slide | Step |
|---|---|---|
| screen-kyc.png | 5 | Sign Up + KYC |
| screen-load.png | 5 | Load Funds |
| screen-pay.png | 5 | Pay via QR Code |
| screen-rewards.png | 5 | Earn Vaulta Rewards |
| screen-m-kyb.png | 6 | Register + KYB |
| screen-m-accept.png | 6 | Accept Payments |
| screen-m-settle.png | 6 | Instant Settlement (Solana Explorer) |
| screen-m-rewards.png | 6 | Earn Rewards Too |

## Slide 7 — Market (redesigned Session 22)

Three-column layout: Traditional Payments | VaultaPay Bridge | Stablecoin Economy

**Data sources used:**
- US merchant card fees: **$187B in 2024** (Nilson Report, record high)
- Stablecoin supply: **$300B+**; volume: **$33T in 2025** (+72% YoY)
- Stablecoin payments (actual commerce): only **$122B** annualized
- Visa stablecoin settlement: **$4.5B/yr** annualized (Q4 FY2025)
- Revenue potential: 1% of $11T US card volume × fee rate (dynamic)

**Dynamic IDs:** `s7_mfee`, `s7_mfee2`, `s7_rev_potential`

## Slide 8 — Benchmarks

Three tables:
1. **Unit Economics** — LTV:CAC, CAC, Annual Net ARPU, CAC Payback vs Chime/Revolut/Cash App/MoneyLion
2. **Revenue Model** — Merchant Fee, Gross Margin (Yr5), EBITDA Margin (**Yr 10**) vs PayPal/Square/Stripe/Interchange
3. **Funding Rounds** — Seed/$2M, Series A (dynamic from model), Series B/TBD vs Stripe/Chime/Revolut/Cash App

## Slide 13 — The Ask

Cap table dilution path uses **competitor averages**:
- Series A: ~20% (Stripe 18%, Revolut 19%, Square 25%)
- Series B: ~16% (Revolut 15%, Square 17%, Chime ~16%)
- Post-full-dilution seed ownership: **13.4%** (was 12.8% with 20%/20%)

Return scenarios at 13.4%: $50M→3.4x, $100M→6.7x, $250M→16.8x, $500M→33.5x

## Architecture Notes
- **Single file** `index.html` — no build step, no npm, no bundler
- **Tab switching:** `switchTab(name)` — toggles `.tab-panel.active`
- **Pitch tab:** `#tab-pitch` is `position:fixed; inset:90px 0 0 0`; iframe has `id="pitch-iframe"`
- **Chart.js 4.4.0** loaded from CDN
- **Color palette (index.html):** `--navy:#1F4E79`, `--blue:#2E75B6`, `--ltblue:#BDD7EE`, `--green:#70AD47`, `--orange:#ED7D31`
- **Color palette (pitch-embed.html):** `--navy:#0A2540`, `--green:#00C896`, `--light:#F5F7FA`
- **Strict rule:** NEVER use "yield", "interest", "APY" — always "Vaulta Rewards", "cycle reward rate", "estimated reward"

## Layout / CSS State (pitch-embed.html)

**Key spacing values:**
- `.slide-inner` padding: `24px 48px 68px` (top/sides/bottom)
- `#s14 .slide-inner` padding: `20px 48px 68px`
- `.slide-body`: `flex:1; display:flex; gap:24px; align-items:stretch; min-height:0; overflow:hidden`
- Nav bar clearance needed: **62px** from bottom (`bottom:22px` + ~40px tall)

**Global card rule (prevents height-stretching):**
```css
.pcard, .wncard, .val-card, .rev-card, .seed-goal, .curr-state,
.cap-panel, .ret-panel, .uof-panel, .be-row { align-self: start; width: 100%; box-sizing: border-box; }
```

## Preview Workflow (IMPORTANT — read PREVIEW_WORKFLOW.md for full details)

1. Start server: `python -m http.server 4321 --directory "C:\Projects\Vaulta-Pay-Model"` (background)
2. Navigate preview browser: `window.location.assign('http://localhost:4321/pitch-embed.html')`
3. Verify: `document.title` should be `"VaultaPay — Seed Pitch Deck"`
4. Navigate slides: `goTo(0)` through `goTo(12)` (0-indexed, 13 slides total)
5. **`preview_screenshot` DOES NOT WORK** — always times out. Use `preview_eval` measurements instead.
6. **Preview browser windowInnerWidth = 1px** — horizontal layout measurements are UNRELIABLE. Use math to verify horizontal fit; only trust vertical measurements.
7. Measure content vs nav bar:
   ```js
   (function() {
     const navTop = window.innerHeight - 62;
     goTo(slideIndex);
     const els = document.getElementById('sN').querySelectorAll('.your-card-class');
     const maxB = Math.max(...[...els].map(e => e.getBoundingClientRect().bottom));
     return { maxBottom: Math.round(maxB), overflow: Math.round(maxB - navTop) };
   })()
   ```
   `overflow > 0` = hidden behind nav (bad). `overflow < 0` = clearance (ok).

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

## Pending / Possible Next Steps
- **Slides 10 & 11 (GTM + Team)** — currently placeholders, need real content
- **Slide content review** — slides 2, 3, 4, 9 (Competition) not reviewed this session
- **Adaptive font sizing** — slides 2 and 4 have free vertical space; could increase fonts
- Add Vaulta Rewards rate to Benchmarks tab (consumer reward % vs competitor loyalty)
- Sensitivity table (2D: wallet size × merchant fee rate → EBITDA margin)
- Consumer ACH withdrawal screen (separate app repo `C:\Projects\Vaulta`)

## Related Repo
The **mobile app** lives at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`, private). See `C:\Projects\Vaulta\NEXT_SESSION_PROMPT.md` for app session state. The two repos are independent — do not mix them.
