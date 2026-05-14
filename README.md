# HEX Stake Analyzer

A fully client-side, single-file HTML tool that reads your native HEX stakes from both **PulseChain** and **Ethereum** and renders an interactive dashboard — all in your browser.

**Zero backend. Zero storage. Zero cookies. Pure read-only blockchain data.**

---

## Features

### Dual-Chain Support
- **PulseChain (pHEX) + Ethereum (eHEX)** — toggle between chains or view both together
- Each stake valued at its own chain's live price — pHEX and eHEX trade independently since the May 2023 fork
- Progressive loading: PulseChain loads first, Ethereum scans in background with status/ETA messaging
- Ethereum ended stakes discovered via batched `eth_getLogs` scanning (~7–10 seconds for full history)

### Live Price Ticker
- DexScreener API per chain (PulseX DEX for pHEX, Uniswap for eHEX)
- CoinGecko fallback per chain
- 24h change, 24h high/low
- 30-day sparkline chart
- HEX Day counter with live per-second countdown to next day

### Stake Analysis
- **Active, pending, ended, and overdue stakes** with sortable table view
- **Multi-wallet support** — add up to 10 wallets, view aggregated or filtered
- **Sea creature league rankings** — 🐋 Whale, 🦈 Shark, 🐬 Dolphin, 🐙 Octopus, 🦀 Crab, 🦐 Shrimp — based on total active T-Shares
- **Big Pay Day (BPD) column** — historically validated with correction factor
- **Totals row** on both Active and Ended stake tables — summed Principal, T-Shares, Yield, Cost, Value, and P&L

### Financial Metrics
- **Cost basis tracking** — historical HEX prices from Day 1 via HEXDailyStats (on-chain DEX data), CoinGecko gap-fill
- **Dual-chain cost basis** — pre-fork stakes use eHEX pricing, native PulseChain stakes use pHEX pricing, fork copies get $0 basis
- **Unrealized & Realized P&L** — active stakes at live price, ended stakes at exit-day price
- **Yield metrics** — total yield, effective APY, daily yield rate, monthly projections

### T-Share Analytics
- **T-Share price** derived on-chain from `globalInfo()` shareRate per chain
- **Average T-Share price paid** — weighted average USD cost per T-Share across all stakes
- **Highest / Lowest T-Share price paid** — red/green indicators
- Holdings value and network share percentage

### Charts
- **Locked vs Liquid HEX** — stacked donut chart with percentage breakdown
- **Yield Accumulation** — green area chart showing cumulative HEX yield earned over time
- **Stake Maturity Calendar** — bar chart grouped by end month with urgency coloring (red = overdue/this month, amber = within 3 months, blue = within a year, purple = 1+ year)

### Comparison Strip
- Side-by-side pHEX vs eHEX metrics: 24h Performance, Price Premium & Parity, T-Share Price, Payout Per T-Share, Available HEX (DEX pool liquidity)

### Available HEX (DEX Pool Liquidity)
- Real-time `balanceOf` queries against known DEX pool contracts per chain
- Staked percentage from `globalInfo()` on-chain data

### Restake Behavior Analyzer
- Analyzes ended stakes to determine restake probability
- 🟢 Restaked (new stake within 14 days), 🟡 Held (too recent to classify), 🔴 Not Restaked
- Percentage breakdown with HEX volume per category

### Moon Math
- Hypothetical price modeling tool — enter any future price per chain
- Quick multiplier buttons: 2×, 10×, 100×, 1,000×, 10,000×
- Per-chain price overrides with unified gold frame visual treatment

### Additional Features
- **Wallet balance** — liquid (unstaked) HEX with USD value per chain
- **Next Stake Ending alert** — prominent banner with urgency coloring
- **Shareable snapshots** — generate downloadable PNG of your dashboard (via html2canvas)
- **Info tooltips** — hover any card, chart, or metric for a plain-English explanation
- **Collapsible Ended Stakes section** — keeps the dashboard clean for large portfolios

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
| **Ethereum RPCs** | Stake data, wallet balance, T-Share price, ended stake log scanning (publicnode + llamarpc) |
| **DexScreener API** | Live pHEX price (PulseX DEX) and eHEX price (Uniswap) |
| **CoinGecko API** | Price fallback per chain + 30-day sparkline |
| **HEXDailyStats** | Historical on-chain DEX prices — eHEX from Day 1, pHEX from Day 1261 (hardcoded tables) |

---

## Security & Privacy

This tool is **strictly read-only**:

- No localStorage, sessionStorage, or cookies
- No backend, no analytics, no tracking
- No wallet connection or private keys required
- All data lives in browser memory and is gone when you close the tab
- The only network calls are blockchain RPC reads and public price API fetches
- No API keys — all endpoints are free public tier

---

## Technical Details

- Single HTML file (~3,200 lines)
- Pure JavaScript — no frameworks
- External dependencies: [Chart.js](https://www.chartjs.org/) (charts) and [html2canvas](https://html2canvas.hertzen.com/) (snapshots), both loaded from CDN
- Custom Keccak-256 implementation for contract selector computation
- Ethereum ended stake discovery via batched `eth_getLogs` with 49,999-block chunks and 20-parallel concurrency
- Complete daily price tables hardcoded from HEXDailyStats with CoinGecko runtime gap-fill

---

## License

GPL-3.0

---

*Safe. Free. Fast. Forever.*
*Built for HEX stakers, by a HEX staker.*
