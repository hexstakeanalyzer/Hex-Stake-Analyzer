# HEX / PulseChain Stake Analyzer

A fully client-side, single-file HTML tool that reads your native HEX stakes from the PulseChain blockchain and renders an interactive dashboard — all in your browser.

**Zero backend. Zero storage. Zero cookies. Pure read-only blockchain data.**

---

## Features

- **Multi-wallet support** — Add up to 10 wallets, view aggregated totals or filter by wallet
- **Live price ticker** — DexScreener (PulseX DEX) with CoinGecko fallback, 24h change, high/low, 30-day sparkline
- **Complete stake analysis** — Active, pending, ended, and overdue stakes with sortable table view
- **Cost basis tracking** — Historical HEX prices from Day 1 to present via HEXDailyStats (on-chain DEX data)
- **Unrealized & Realized P&L** — Active stakes valued at current price vs ended stakes valued at exit price
- **Yield metrics** — Total yield, effective APY, daily yield rate, monthly projections
- **T-Share analytics** — T-Share price (on-chain), holdings value, network share percentage
- **Wallet balance** — Liquid (unstaked) HEX with USD value
- **Locked vs Liquid chart** — Pie chart showing staked vs available HEX
- **Stake allocation chart** — Portfolio concentration across stakes
- **Next Stake Ending alert** — Prominent banner with urgency coloring
- **Shareable snapshots** — Generate downloadable PNG of your dashboard
- **Info tooltips** — Hover any card or chart for a plain-English explanation

## How to Use

1. Download `index.html`
2. Open it in any modern browser
3. Paste a PulseChain wallet address (0x…) and click **+ Add**
4. Add more wallets if desired (up to 10)
5. Click **Analyze**

That's it. No install, no wallet connection, no private keys.

## Data Sources

| Source | What It Provides |
|--------|-----------------|
| **PulseChain RPCs** | Stake data, wallet balance, T-Share price (4-node failover) |
| **DexScreener API** | Live pHEX price from PulseX DEX |
| **CoinGecko API** | Price fallback + 30-day sparkline |
| **HEXDailyStats** | Historical on-chain DEX prices, Day 1 to present (hardcoded) |

## Security & Privacy

This tool is **strictly read-only**:

- No localStorage, sessionStorage, or cookies
- No backend, no analytics, no tracking
- No wallet connection or private keys
- All data lives in browser memory and is gone when you close the tab
- The only network calls are blockchain RPC reads and public price API fetches

## Technical Details

- Single HTML file (~1,300 lines)
- Pure JavaScript — no frameworks
- External dependencies: [Chart.js](https://www.chartjs.org/) (charts) and [html2canvas](https://html2canvas.hertzen.com/) (snapshots), both loaded from CDN
- Custom Keccak-256 implementation for contract selector computation
- Complete daily price tables: 2,331 eHEX entries + 1,070 pHEX entries hardcoded from HEXDailyStats

## Support

This tool is free and open-source. If you find it useful, consider sending a donation to:

`0xcE814f3042bD70aCE79f7d40cAdb719B3824067d`

PulseChain & Ethereum compatible — HEX, PLS, PLSX, ETH, USDC, or your favorite meme coins. Every contribution helps keep the tool maintained.

## License

GPL-3.0 — See [LICENSE](LICENSE) for details.

© 2026 HexStakeAnalyzer. All rights reserved.

---

*Built for HEX stakers, by a HEX staker.*
