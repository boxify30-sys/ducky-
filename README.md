# The Dice Room 🎲

A Telegram casino bot with crypto deposits/withdrawals (via OxaPay) and a suite
of betting games.

## Games

- 🎲 Dice, 🎳 Bowling, ⚽ Soccer, 🎯 Darts, 🏀 Basketball
- 🃏 Blackjack
- 💣 Mines
- 🪜 Tower
- 🪙 Coinflip
- 🚀 Limbo
- 🎰 Dice Roulette

Players bet, then alternate emoji turns over rounds. Highest score each round
earns a point — first to 3 points wins the pot.

## Features

- Real crypto deposits, withdrawals & house balance via **OxaPay**
- 💰 Balance, 📊 Stats (total wagered + net profit/loss), 🏦 House balance
- Weekly & monthly wager bonuses with a **live countdown** to the exact unlock time
- Leaderboard + weekly leaderboard payouts
- Tipping & rain

## Environment Variables

Set these before running (e.g. in your host's config vars or a local `.env`):

| Variable | Required | Description |
|---|---|---|
| `TELEGRAM_TOKEN` | ✅ | Bot token from @BotFather |
| `OXAPAY_MERCHANT_API_KEY` | ✅ | OxaPay merchant (deposits) key |
| `OXAPAY_PAYOUT_API_KEY` | ✅ | OxaPay payout (withdrawals) key |
| `OXAPAY_GENERAL_API_KEY` | ✅ | OxaPay general/balance key |
| `BALANCES_FILE` | ❌ | Path to persistent balances JSON (default: `/data/balances.json` if `/data` exists, else `balances.json`) |

## Local Setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

export TELEGRAM_TOKEN="..."
export OXAPAY_MERCHANT_API_KEY="..."
export OXAPAY_PAYOUT_API_KEY="..."
export OXAPAY_GENERAL_API_KEY="..."

python ducky.py
```

## Deployment

The included `Procfile` runs the bot as a **worker** process (long-polling, no web
server needed):

```
worker: python ducky.py
```

- `runtime.txt` pins the Python version.
- `requirements.txt` lists dependencies (`python-telegram-bot[job-queue]` is
  required for the scheduled bonus/leaderboard jobs and live countdowns).

> ⚠️ **Persistence:** balances are stored in a JSON file. On ephemeral hosts
> (e.g. free Heroku-style dynos), mount a persistent disk and point
> `BALANCES_FILE` at it, or the data resets on restart.

## Admin

Add your Telegram user ID to `ADMIN_IDS` in `ducky.py` to access house balance
and admin commands.
