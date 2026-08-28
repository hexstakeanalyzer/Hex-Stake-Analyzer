# HEX Stake Analyzer

A single-file, client-side dashboard for HEX stakes across **PulseChain** and **Ethereum**. Paste a public address, see every stake, HSI, HTT, and their USD values — all in your browser.

**Zero backend. Zero analytics. Only your recent addresses are saved locally, and only on this device.**

Live: <https://hexstakeanalyzer.github.io/Hex-Stake-Analyzer/>

---

## Features

**Multi-chain, multi-wallet**
- Toggle between PulseChain (pHEX), Ethereum (eHEX), or both
- Analyze up to 10 wallets at once; filter or aggregate freely
- Each stake valued at its own chain's live price — pHEX and eHEX trade independently since the May 2023 fork

**Every stake type**
- Native HEX stakes
- HSI — tokenized (ERC-721) and untokenized Hedron Stake Instances
- HTT — Actuator-delegated stakes on PulseChain
- Bridged eHEX detection on PulseChain

**HTT deep-dive**
- Live per-HTT USD prices via the PulseX v2 subgraph
- USD value on every extracted / extractable / in-wallet total
- Automatic discovery of any HTT series that exists on-chain (Actuator-listed or otherwise), with spoof-token filtering
- Per-series breakdown showing borrowed vs native extraction

**Portfolio numbers**
- Unrealized + Realized P&L with lifetime yield and average holding period
- Effective APY (active / ended / combined), daily yield rate, monthly projections
- T-Share holdings + network share; T-Share price on-chain per chain
- Wallet balance broken down by chain + bridged eHEX + HTT

**Recent-address history**
- The last 20 addresses you analyze are saved to localStorage on this device
- Dropdown opens when you click the address input; click one to load it, × to remove it individually
- One-click **Clear addresses** wipes the whole list. Never sent anywhere.

## How to Use

1. Open `HSA v54.1.html` in any modern browser (or visit [hexstakeanalyzer.github.io/Hex-Stake-Analyzer](https://hexstakeanalyzer.github.io/Hex-Stake-Analyzer/))
2. Paste one or more wallet addresses; click **+ Add** to stack them, then **Analyze**
3. Choose PulseChain, Ethereum, or Both at the top of the dashboard

No install. No wallet connection. No signatures.

## Data Sources

| Source | Provides |
|---|---|
| **PulseChain RPCs** (4-node failover) | Stake data, wallet balances, share rate |
| **Ethereum RPCs** (publicnode + runtime failover) | Same on Ethereum |
| **Blockscout / PulseScan** | Ended-stake event log scans |
| **Actuator contract** (PulseChain only) | HTT discovery + per-stake extraction detail |
| **PulseX v2 subgraph** | Live HTT USD prices + HTT safety-net discovery |
| **DexScreener** | Live HEX price per chain (PulseX + Uniswap), with CoinPaprika / CoinGecko fallback. Also enumerates every HEX / eHEX / pHEX liquidity pool per chain — the Available HEX card auto-discovers pools on every refresh instead of relying on a hardcoded list |
| **HEXDailyStats** | Baked daily payout + historical price tables (Day 1 forward), with CoinGecko range fallback |

All read-only. All public. No API keys.

## Security & Privacy

- **Read-only.** No signatures, no wallet connection, no private keys — just paste a public address.
- **Nothing sent anywhere.** All calculation happens in your browser.
- **sessionStorage** for a same-tab scan cache (auto-wipes on tab close).
- **localStorage** for one thing only: the recent-address history (key `hsa_recent_addrs`, capped at 20). A visible **Clear addresses** button next to the search bar wipes it any time. Skip this on shared computers.
- No cookies, no analytics, no tracking, no telemetry.
- **Auto-update:** on a fresh visit, the app quickly checks whether a newer version has been published and, if so, reloads once to pick it up (adds a `?updated_from=...` cache-buster to the URL). Tabs you've had open for a while show an "update available" banner instead of reloading, so an in-progress analysis is never interrupted.

## Technical Notes

- Single HTML file, no build step, no framework.
- Charts via [Chart.js](https://www.chartjs.org/) loaded from CDN.
- Custom Keccak-256 for function-selector computation.
- HTT scan parallelizes ~20 batched RPC probes and one GraphQL query — completes in roughly one round-trip time even for large wallets.
- Sticky column headers on every stake table so the row identity stays visible as you scroll.

## Refreshing Baked Tables

Baked `DAILY_DATA_*` and `PRICE_TABLE_*` arrays cover on-chain history back to Day 1 (eHEX) and Day 1261 (pHEX). Before a release:

1. Open `fetch_daily_data.html` in any browser
2. Click **Fetch All Data**
3. Wholesale-replace the four array literals in the current HSA HTML file

Runtime tail-fetch fills any gap between the baked cutoff and today automatically, so a stale baked table degrades gracefully rather than silently undercounting yield.

## Support

Donation address is in the topbar `♥ Thanks` button — same address works on PulseChain and Ethereum.

## License

GPL-3.0

---

*Built for HEX stakers, by a HEX staker.*
