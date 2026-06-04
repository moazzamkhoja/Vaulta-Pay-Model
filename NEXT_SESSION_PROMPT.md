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

## Current State (Session 21)

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

### Tab 2 — 📐 Benchmarks
All VaultaPay cells are live-linked to model sliders.

### Tab 3 — 🎯 Investor Pitch
Full-screen iframe loading `pitch-embed.html`. **14-slide** seed deck.

| # | Slide | Notes |
|---|---|---|
| 1 | Cover | $2M / $8M pre / $10M post |
| 2 | Problem | 3 cards: checking earns nothing, merchant fees, unbanked |
| 3 | Solution | Two-column: banking layers vs Solana; GENIUS Act explainer |
| 4 | Why Now | 2×2 grid: GENIUS Act, CLARITY Act, Solana, Consumer demand |
| 5 | Consumer Flow | KYC → Load → QR Pay → Rewards; vUSD explainer strip |
| 6 | Merchant Flow + T-Bill | KYB → accept → settle → rewards; T-bill 80/20 split |
| 7 | Market | Bottom-up bar sizing, TAM/SAM/SOM + Why VaultaPay Wins |
| 8 | Benchmarks | Live-linked to model via postMessage |
| 9 | Business Model | 2-col cards (Consumer/Merchant Value) + 3-tile Revenue Streams |
| 10 | Competition | 7-feature table vs Venmo/Cash App/Zelle/Chime/Apple Pay |
| 11 | GTM | Placeholder |
| 12 | Team | Placeholder |
| 13 | Traction + Seed Plan | Current state + 3 seed goals |
| 14 | The Ask | $2M, dilution path, return scenarios $50M–$500M exit |

**Dynamic link (postMessage):**
- iframe signals parent with `{ type: 'pitchReady' }` when loaded
- parent calls `sendPitchData()` immediately on receiving pitchReady
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

**Slides with vertically-centered body content:**
- Slides 5, 6, 9: `.slide-body` has `justify-content: center` inline

**Slide 9 (Business Model):** Dark navy Unit Economics panel was removed. Now shows:
- Top row: 2-col grid (Consumer Value card | Merchant Value card), `align-items: start`
- Bottom: Revenue Streams card with 3 metric tiles (0.8% / 20% sleeve / Roadmap)
- Hidden dynamic ID spans at bottom for postMessage

## Preview Workflow (IMPORTANT — read PREVIEW_WORKFLOW.md for full details)

1. Start server: `python -m http.server 4321 --directory "C:\Projects\Vaulta-Pay-Model"` (background)
2. Navigate preview browser: `window.location.assign('http://localhost:4321/pitch-embed.html')`
3. Verify: `document.title` should be `"VaultaPay — Seed Pitch Deck"`
4. Navigate slides: `goTo(0)` through `goTo(13)` (0-indexed)
5. **`preview_screenshot` DOES NOT WORK** — always times out. Use `preview_eval` measurements instead.
6. Measure content vs nav bar:
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

**Measured content bottoms (viewport height = 720px, navTop = 658):**
| Slide | Content bottom | Space below nav |
|---|---|---|
| 2 | 381 | 277px free |
| 4 | 435 | 223px free |
| 5 | ~436 | centered |
| 6 | 574 | 84px free |
| 9 | 501 | centered |
| 13 | 438 | 220px free |
| 14 | 652 | 6px clearance (tight) |

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
- **Content review** (priority) — Moazzam reviewing all 14 slides for copy/content changes
- **Adaptive font sizing** — slides 2 and 4 have 200+ px free; increase fonts proportionally using JS measurement + CSS scaling. Use preview measurements to verify before committing.
- Confirm GitHub Pages is live and test all 14 slides on hosted URL
- Add Vaulta Rewards rate to Benchmarks tab (consumer reward % vs competitor loyalty)
- Add a "Funding Schedule" view showing seed / Series A / Series B raise amounts
- Sensitivity table (2D: wallet size × merchant fee rate → EBITDA margin)
- Consumer ACH withdrawal screen (separate app repo `C:\Projects\Vaulta`)

## Related Repo
The **mobile app** lives at `C:\Projects\Vaulta` (`moazzamkhoja/Vaulta`, private). See `C:\Projects\Vaulta\NEXT_SESSION_PROMPT.md` for app session state. The two repos are independent — do not mix them.
