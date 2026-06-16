# VaultaPay — Seed Pitch Brief
**Everything needed to build the investor pitch (rework `pitch-embed.html`) and the Benchmarks tab. Grounded in this session's research + the live model. Build the deck to tell THIS story; pull live numbers from the model via postMessage where possible.**

> Wording rule (strict): never "yield / interest / APY" → always "Vaulta Rewards", "T-bill float", "estimated reward".

---

## 1. One-liner / positioning
**VaultaPay is a blockchain bill-pay portal** — Americans pay rent + utilities (and P2P) for free, on stablecoin rails (vUSD on Solana). Merchants (apartment operators, utilities) pay **less than they pay today** and both sides earn **Vaulta Rewards** on idle balances. Think **"Bilt, but on-chain, cheaper for the merchant, and free to the renter."**

## 2. The ask
**$2.1M Seed** to reach product-market fit and the first enterprise wins; Series A adds operating capital + **$6M regulatory (GENIUS Act) reserve capital**. Model shows **break-even Year 4** and **Series B not needed for operations** (self-funding by then).

## 3. Narrative arc (target slide order — rework the 13 existing slides)
1. **Cover** — VaultaPay; blockchain bill-pay portal; "free bill pay, rewards on every dollar." The ask ($2.1M seed).
2. **Problem** — Rent + utilities are the two biggest recurring payments from checking; renters pay **$2–$3.95 convenience fees** per payment; checking earns **~0%**; billers/operators pay processing costs and get nothing on the float they hold.
3. **Solution** — Pay rent/utilities on stablecoin rails: **free to the renter**, **cheaper for the merchant** than incumbents, **both earn Vaulta Rewards** on balances (T-bill float). No bank account required.
4. **Why now** — **GENIUS Act** (stablecoin reserves regulation), CLARITY Act, Solana cost/speed, and **Bilt's $10B valuation** proving rent-as-a-platform works. Stablecoins are mainstream.
5. **How it works — Consumer** — load → pay rent + utilities via app → earn Vaulta Rewards (keep phone screenshots: KYC → Load → Pay → Rewards).
6. **How it works — Merchant** — register/KYB → accept payments (lower cost) → instant Solana settlement → earn Vaulta Rewards on parked balances.
7. **Business model** — Free to consumer; **$2 flat merchant fee** (~50% of the $3.95 incumbents charge); plus float sleeve. Net-revenue: fees + net T-bill margin. P2P free.
8. **Market / TAM** — two-sided and huge (see §5). Bottom-up: sign apartment operators & utilities, each brings tens of thousands of payers.
9. **Competition** — vs Bilt, Doxo, Zego/RentPayment, Paymentus, bank bill-pay (see §4 table). Edge: free-to-renter AND cheaper-to-merchant AND on-chain settlement AND rewards both sides.
10. **Unit economics** — LTV:CAC **3.8×**, CAC **$37**, payback **5.6 mo**; one enterprise deal ≈ **$2–4M gross profit/yr**.
11. **Financial projections** — break-even **Year 4**, Rev Yr10 **$53M**, EBITDA **$28M (93% GM)**; the line-item P&L lives in the Financials tab.
12. **Go-to-market** — **merchant-led / B2B2C**: enterprise sales to apartment operators & utilities; the building/utility funnels its residents (Bilt playbook). Low CAC because the merchant is the channel.
13. **Traction + roadmap** — prototype on Solana devnet; seed milestones → first enterprise wins.
14. **Team** — (placeholder — needs real content.)
15. **The Ask** — **$2.1M seed**; use of funds (see §6); milestones to Series A.

## 4. Competitor / fee comparison (for the Competition slide + Benchmarks tab rebuild — REPLACE Chime/PayPal/Venmo)
| Player | Consumer pays | Merchant/biller pays | Rewards? | On-chain? |
|---|---|---|---|---|
| **VaultaPay** | **$0** | **$2 flat/payment** | **Both sides** | **Yes (Solana)** |
| Bilt | $0 (in-network) | landlord **0.6–0.9%** (~$12 on $1,750) + fees | Renter only (points) | No |
| Doxo | $3–4 or $5.99/mo | — | No | No |
| Zego / RentPayment | $2–3.95 ACH / 2.5–3.5% card | ~$0/txn + SaaS $1.40–5/unit/mo | No | No |
| Paymentus (utilities) | $1.95–$2.95 | varies | No | No |
| Plastiq | 2.9–2.99% card | — | Card points | No |
| Bank bill-pay | usually free | — | No | No |
| *True ACH rail cost* | — | *$0.26–$0.50* | — | — |

**Key message:** VaultaPay is the only one that is **free to the renter AND cheaper to the merchant AND rewards both sides** — and beats Bilt's percentage on a typical rent ($2 flat vs ~$12).

## 5. Market / TAM (sourced this session)
- **Utilities:** ~**52,000 community water systems** + ~3,000 electric + ~1,400 gas utilities → tens of thousands of billers (Paymentus alone: 2,200 billers → 34M consumers).
- **Apartments:** Greystar **~800,000 units**, Equity Residential 83k, Asset Living 291k; **NMHC Top 50 manage ~20% of all US units**. Hundreds of operators with 50k+ units.
- **Spend:** avg US rent **~$1,750/mo**, utilities **~$412/mo**; renter take-home **~$4,500/mo**; ~33% of income on rent+utilities. Bilt processes **$45B+/yr** in rent.
- **One enterprise win** (50k units, 50% adoption = 25k active) ≈ **$3.5M gross revenue / $2M gross profit per year.**

## 6. Seed use of funds (~$2.1M — from the Financials tab)
Engineering (4 FTE) ~$0.75M · G&A + compliance ~$0.4M · other payroll (legal/leadership/cyber) ~$0.2M · CS ~$0.14M · sales/BD ~$0.1M · infra/legal/activation ~$0.15M · less Yr-1 revenue · + 20% buffer = **$2.06M**. (Regulatory $6M reserve raised separately at Series A.)

## 7. Headline numbers to feature (current model defaults — verify live before finalizing)
Break-even **Yr 4** · EV **$53M** (risk-adj $12M) · **LTV:CAC 3.8×** · CAC **$37** · LTV **$140** · payback **5.6 mo** · Rev Yr10 **$53M** · EBITDA Yr10 **$28M (93% GM)** · 617k customers · 171 merchants · 64 employees. Merchant fee **$2** vs incumbents' **$3.95** / Bilt **0.6–0.9%**.

## 8. Technical rebuild notes
- **Deck file:** `pitch-embed.html` — 13 slides, currently the OLD debit-card narrative; ← → arrows + dot nav. Colors `--navy:#0A2540, --green:#00C896`.
- **Benchmarks tab** (in `index.html`): currently old comps (Chime/Revolut/PayPal). Rebuild table around the §4 competitor set; the `bm_*` IDs are live-linked in `update()`.
- **Live data bridge:** `index.html` → `pitch-embed.html` via `postMessage` (`sendPitchData()`); the payload keys are stale from the debit model — update both the payload and the deck's dynamic IDs to the bill-pay metrics (LTV:CAC, CAC, merchant fee, break-even year, Rev/EBITDA Yr10, one-enterprise-deal value).
- Phone screenshots (slides 5/6) already exist in repo root (`screen-*.png`) — keep, don't crop.

## 9. Optional model tweaks for an ambitious-but-defensible deck
- Enterprise CPM 50k → **100k** (still conservative; EQR 83k, Greystar 800k) → EV ~$133M.
- Steady-state enterprise deals 20 → 30–40 → EV +80%.
- These are the levers that scale EV super-linearly (operating leverage); use judiciously and keep them defensible.
