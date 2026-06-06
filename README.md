# HEX Stake Analyzer

A fully client-side, single-file HTML tool that reads your HEX stakes from both **PulseChain** and **Ethereum** — native, HSI, and HTT (Actuator-delegated) — and renders an interactive dashboard, all in your browser.

**Zero backend. No permanent storage. No cookies. Pure read-only blockchain data.**

---

## Features

### Dual-Chain Support
- **PulseChain (pHEX) + Ethereum (eHEX)** — toggle between chains or view both together
- Each stake valued at its own chain's live price — pHEX and eHEX trade independently since the May 2023 fork
- Progressive loading: PulseChain loads first, Ethereum scans in background with status/ETA messaging
- Ethereum ended stakes discovered via batched `eth_getLogs` scanning (~7–10 seconds for full history)

### Live Price Ticker
- Bold dashboard-style ticker with large price display, glowing accent bars, and prominent chain tags
- DexScreener API per chain (PulseX DEX for pHEX, Uniswap for eHEX)
- CoinGecko fallback per chain
- 24h change, 24h high/low range
- Large 30-day sparkline charts with gradient fill and a live endpoint marker
- HEX Day counter with live per-second countdown to the next day

### Stake Analysis
- **Active, pending, ended, and overdue stakes** with sortable table views
- **Multi-wallet support** — add up to 10 wallets, view aggregated or filtered per-wallet/per-chain
- **Sea-creature league ranking** — 🐋 Whale, 🦈 Shark, 🐬 Dolphin, 🐙 Octopus, 🦀 Crab, 🦐 Shrimp — based on total active T-Shares, shown as a badge in the Wallet Balance card (so you can screenshot your stack and rank without exposing wallet addresses)
- **HSI stake detection** — Hedron Stake Instances (tokenized and untokenized) discovered automatically via on-chain queries to the HSIM contract
- **HTT stake detection** — HEX Time Token (Actuator-delegated) stakes discovered on PulseChain, with a full dedicated analysis section (see below)
- **Stake type badges** — each stake labeled Native, HSI, or HTT so you can see how your stakes are held
- **Big Pay Day (BPD) column** — historically validated with correction factor
- **Totals row** on both Active and Ended stake tables — summed Principal, T-Shares, Yield, Cost, Value, and P&L

### Portfolio Cards
The main dashboard distills your position into eight focused cards across two rows:
- **Row 1 (what you have):** Active Stakes · Active T-Shares · **Stake Value** (current USD value + total HEX staked) · Wallet Balance (with HTT holdings + rank badge)
- **Row 2 (performance):** T-Share Price · Daily Yield Rate · **Unrealized P&L** (P&L + cost basis) · Realized P&L
- Native-only wallets see no HTT clutter; HTT-aware sub-lines appear only when delegated stakes are detected

### HTT Position Analysis *(appears when HTT-backed stakes are detected)*
A dedicated, fact-based section for Actuator-delegated HEX stakes and the HTT (HEX Time Token) minted against them. Surfaces what the Actuator app cannot show on one screen:
- **Key stats strip** — HEX Locked · HTT Outstanding (minted, in circulation) · HTT Mintable (still extractable) · HTT In Wallet · HEX Accrued · Earliest Mintable, each color-coded by unit
- **HEX-Locked-by-Series composition bar** — a compact proportional view of where your locked HEX is concentrated across HTT series
- **Per-HTT Breakdown table** — one row per HTT series with an inline extraction-ratio bar (outstanding vs. mintable), stakes count, HEX backing, in-wallet balance, redemption day, and days left; fully sortable by any column
- **Maturity charts** — two side-by-side timelines: **Outstanding by Redemption Day** (HTT already extracted) and **Mintable by Redemption Day** (HTT still extractable), both plotted against the on-chain redemption day
- **Per-stake HTT detail table** — every delegated stake with principal, accrued yield, T-Shares, mintable, outstanding, and projected end-stake bounty; sortable
- **Wallet HTT holdings** — distinguishes HTT extracted from your own stakes vs. HTT acquired externally (no related stake)
- Handles unminted delegated stakes (listed by their natural redemption day) and the `HTT-N redeems on HEX day N` convention

### Financial Metrics
- **Cost basis tracking** — historical HEX prices from Day 1 via HEXDailyStats (on-chain DEX data), CoinGecko gap-fill
- **Dual-chain cost basis** — pre-fork stakes use eHEX pricing, native PulseChain stakes use pHEX pricing, fork copies get $0 basis
- **Unrealized & Realized P&L** — active stakes at live price, ended stakes at exit-day price
- **Yield metrics** — total yield, effective APY (active / ended / combined), daily yield rate, monthly projections

### T-Share Analytics
- **T-Share price** derived on-chain from `globalInfo()` shareRate per chain
- **Average T-Share price paid** — weighted average USD cost per T-Share across all stakes
- **Highest / Lowest T-Share price paid** — red/green indicators
- Network share percentage per chain

### Charts
- **Locked vs Liquid HEX** — donut chart with percentage breakdown
- **Yield Accumulation** — area chart showing cumulative HEX yield earned over time
- **Stake Maturity Calendar** — bar chart of native/HSI stakes grouped by redemption period

### Comparison Strip
- Side-by-side pHEX vs eHEX market metrics: 24h Performance, Price Premium & Parity, T-Share Price, Payout Per T-Share, and Available HEX (DEX pool liquidity)

### Available HEX (DEX Pool Liquidity)
- Real-time `balanceOf` queries against known DEX pool contracts per chain
- Staked percentage from `globalInfo()` on-chain data

### Restake Behavior Analyzer
- Analyzes ended stakes to determine restake behavior
- 🟢 Restaked (new stake within 14 days), 🟡 Held (too recent to classify), 🔴 Not Restaked
- Percentage breakdown with HEX volume per category

### Moon Math
- Hypothetical price modeling tool — enter any future price per chain
- Quick multiplier buttons: 2×, 10×, 100×, 1,000×, 10,000×
- Per-chain price overrides with unified gold frame visual treatment

### Additional Features
- **Wallet balance** — liquid (unstaked) HEX with per-token breakdown: pHEX, eHEX, and bridged eHEX on PulseChain, plus HTT tokens held, each with individual USD/unit valuation
- **Next Stake Ending alert** — prominent banner with urgency coloring
- **Info tooltips** — tap any card, chart, or metric's ⓘ for a plain-English, HTT-aware explanation
- **Collapsible Ended Stakes section** — keeps the dashboard clean for large portfolios
- **Responsive layout** — fluid scaling tuned for laptop and desktop, with graceful narrow-width fallbacks

---

## How to Use

1. Visit [hexstakeanalyzer.github.io/Hex-Stake-Analyzer](https://hexstakeanalyzer.github.io/Hex-Stake-Analyzer/) — or download the HTML file and open it locally
2. Paste any wallet address (0x…) and click **+ Add**
3. Add more wallets if desired (up to 10)
4. Click **Analyze**
5. Toggle between PulseChain, Ethereum, or Both using the chain selector

That's it. No install, no wallet connection, no private keys.

---

## Data Sources

| Source | What It Provides |
|--------|-----------------|
| **PulseChain RPCs** | Stake data, wallet balance, T-Share price, global info (4-node failover) |
| **Ethereum RPC** | Stake data, wallet balance, T-Share price, ended stake log scanning (publicnode) |
| **Hedron (HSIM) Contract** | HSI stake discovery — untokenized and tokenized (ERC-721) |
| **Actuator Contract** | HTT (delegated) stake discovery, outstanding/mintable amounts, per-stake details (PulseChain only) |
| **Bridged eHEX Contract** | Wallet balance detection for eHEX held on PulseChain (bridged via PulseChain Bridge) |
| **DexScreener API** | Live pHEX price (PulseX DEX) and eHEX price (Uniswap) |
| **CoinGecko API** | Price fallback per chain + 30-day sparkline |
| **HEXDailyStats** | Historical on-chain DEX prices — eHEX from Day 1, pHEX from Day 1261 (hardcoded tables) |

---

## Security & Privacy

This tool is **strictly read-only**:

- **No permanent storage** — no localStorage, no cookies, no backend, no analytics, no tracking
- A temporary **sessionStorage** cache speeds up re-scans within the same browser tab and is automatically erased when the tab closes
- No wallet connection or private keys required — you only paste a public address
- All data lives in browser memory and is gone when you close the tab
- The only network calls are blockchain RPC reads and public price API fetches
- No API keys — all endpoints are free public tier

---

## Technical Details

- Single self-contained HTML file
- Pure JavaScript — no frameworks
- One external dependency: [Chart.js](https://www.chartjs.org/) for the native dashboard charts, loaded from CDN (the HTT charts and bars are hand-rendered SVG, no library)
- Custom Keccak-256 implementation for contract selector computation
- Ethereum ended stake discovery via batched `eth_getLogs` with 49,999-block chunks at concurrency 6
- Stake discovery via on-chain scan paths: native stakes, untokenized HSI, tokenized HSI (ERC-721), and Actuator-delegated HTT (PulseChain only)
- HTT mintable amounts derived from `getExtractableAmount(hsi, maturity)` minus outstanding collateral, per delegated stake
- Complete daily price tables and payout data hardcoded from HEXDailyStats and CoinGecko, with runtime gap-fill for days after the last static entry
- Bridged eHEX detection via `balanceOf` on the PulseChain bridge contract (`0x57fd…D225`)

---

## License

GPL-3.0

---

*Safe. Free. Fast. Forever.*
*Built for HEX stakers, by a HEX staker.*
