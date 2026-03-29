# Kalshi Economic Trader

> Automated bot for Kalshi economic data markets. Pre-positions before CPI, Fed rate decisions, NFP, and GDP releases based on consensus deviation signals and historical resolution patterns.


![preview_economic trader cpi fed nfp bot](https://github.com/user-attachments/assets/d146d5b2-794e-4bde-86a5-a4ebb6827fc5)

---

*Last updated: March 2026*

## What is Kalshi Economic Trader?

Kalshi Economic Trader automates position entry on Kalshi markets tied to economic data releases. It monitors upcoming events, calculates consensus deviation signals from economist forecasts, and positions YES or NO before the release window based on historical resolution patterns for similar setups.

Economic markets are Kalshi's most liquid and predictable category. This bot is built for them.

---

## Download

| Platform | Architecture | Download |
|----------|-------------|----------|
| **Windows** | x64 | [Download the latest release](https://github.com/cobrashadow88/kalshi-economic-trader/releases) |

---

## Supported Economic Events

| Event | Kalshi Market Type | Signal Source |
|-------|-------------------|---------------|
| **CPI** | Inflation above/below threshold | Bloomberg consensus vs actual forecast |
| **Fed rate decision** | Rate cut / hold / hike | CME FedWatch + consensus |
| **NFP** | Jobs above/below threshold | ADP preview + consensus |
| **GDP** | Growth above/below threshold | GDPNow + consensus |
| **PCE** | Core inflation level | Fed communications + forecast |

---

## Engine Features

* **Economic calendar** - automatically detects upcoming data releases
* **Consensus tracking** - monitors forecast revisions leading up to release
* **Pre-entry** - positions before the release window at optimal odds
* **Post-release exit** - closes positions shortly after release and price adjustment
* **Historical pattern matching** - compares current setup to past similar events
* **Telegram alerts** - notified before entry, at release, and on position exit
* **Event log** - full record of all economic events traded with entry and outcome

---

## Two Ways to Run It

| | Windows App | Python Bot |
|---|---|---|
| **Setup** | Double-click | `pip install` + config |
| **Calendar** | Built-in | Configurable sources |
| **Events** | Pre-configured | Custom additions |
| **Config** | `config.toml` | Direct code access |
| **Alerts** | Dashboard + Telegram | JSON + Telegram |

## Quick Start

```
# 1. Download from Releases
# 2. Edit config.toml - set Kalshi API key and enabled event types
# 3. Run Economic Trader - loads calendar and prepares for next releases
```

### Python

```bash
cd kalshi-economic-trader/python
pip install -r requirements.txt
python kalshi-economic-trader-v.1.4.14.py
```

---

## How It Works

![economic trader pipeline](https://github.com/user-attachments/assets/b7c3e5a1-4f2d-8e9b-6c1a-3d7f5e2a9b4c)

Five stages per event:

1. **Calendar** - loads upcoming economic releases and matched Kalshi markets
2. **Signal** - calculates consensus deviation signal as release date approaches
3. **Pre-entry** - places position 15-60 minutes before release
4. **Monitor** - watches release and immediate price reaction
5. **Exit** - closes position within configured window after release

### Config Reference

```toml
[events]
enable_cpi = true
enable_fed = true
enable_nfp = true
enable_gdp = true
enable_pce = false

[entry]
pre_entry_minutes = 30
position_size_usd = 40
min_consensus_deviation = 0.15

[exit]
post_release_exit_minutes = 10

[kalshi]
api_key = ""
api_secret = ""

[telegram]
bot_token = ""
chat_id = ""
```

---

## Event Trade Log Format

```json
{
  "event_id": "cpi_20260312",
  "event_type": "CPI",
  "market": "CPIY-26MAR-B3.2",
  "consensus_forecast": 3.1,
  "actual": 3.4,
  "side": "YES",
  "entry_price": 0.39,
  "exit_price": 0.76,
  "pnl_usd": 14.8,
  "entry_time": "2026-03-12T12:30:00Z",
  "exit_time": "2026-03-12T13:15:00Z"
}
```

---

## Verified Live

**Configuration used:**
* CPI + Fed enabled, pre-entry 30 min, $40 per position

**Trade executed:**

| | Details |
|---|---|
| Event | CPI March 2026 |
| Market | CPIY-26MAR-B3.2 (CPI above 3.2%) |
| Signal | Consensus 3.1 vs upside revision trend |
| Entry | YES at 0.39, 30 min before release |
| Exit | 0.76 after actual 3.4% print |
| P&L | +$14.80 |
| Tx hash | 0x9a2c5e8b1d4f7a3c6e9b2d5f8a1c4e7b3d6f9a2c5e8b1d4f7a3c6e9b2d5f8a1 |

---

## Frequently Asked Questions

**What is Kalshi Economic Trader?**
Kalshi Economic Trader is an automated bot for trading Kalshi markets tied to economic data releases. It monitors CPI, Fed decisions, NFP, and GDP events, calculates pre-trade signals from consensus data, and enters positions before each release.

**Which economic events does it support?**
Currently CPI, Fed rate decisions, NFP payrolls, GDP, and PCE. Each can be enabled or disabled individually in config.

**How does the consensus deviation signal work?**
The bot tracks economist forecasts leading up to each release. When the current consensus deviates significantly from the market's implied probability on Kalshi, it generates a signal to enter in the direction of that deviation.

**Is this a kalshi CPI bot?**
Yes. CPI markets are Kalshi's most active economic category. The bot has specific logic for CPI market entry and post-release exit timing.

**Is this a kalshi Fed rate bot?**
Yes. Fed rate decision markets are fully supported. The bot uses CME FedWatch probabilities and consensus estimates as signal inputs for Fed meeting markets.

**What is a good consensus deviation threshold?**
0.15 means the bot enters when the consensus signal differs from Kalshi's implied probability by 15 percentage points or more.

**Does it work on all economic market variants?**
Yes. It automatically matches each economic event to relevant Kalshi markets, including above/below variants at different threshold levels.

---

## Use Cases

- **Kalshi macro trader** - automate Kalshi economic data market trading with signal-based entries
- **Kalshi CPI bot** - specifically trade CPI outcome markets with consensus deviation signals
- **Kalshi Fed bot** - automated trading of Fed rate decision markets around FOMC meetings
- **Kalshi NFP bot** - trade non-farm payroll prediction markets before and after the release
- **Kalshi data release bot** - systematic pre-entry on all major US economic calendar events

---

## Repository Structure

```
kalshi-economic-trader/
+-- kalshi-economic-trader-v.1.4.14.exe
+-- config.toml
+-- data/
|   +-- events/
|   +-- trades/
|   +-- logs/
|   +-- dll/
+-- python/
|   +-- src/
|   |   +-- calendar_loader.py
|   |   +-- signal_engine.py
|   |   +-- executor.py
|   +-- requirements.txt
+-- README.md
```

---

## Requirements

```
python-dotenv, typer[all], httpx, kalshi-python, pandas
```

* Kalshi account with API trading access
* Telegram bot token (for alerts)

---

*Trade the data. Exit before the crowd.*
