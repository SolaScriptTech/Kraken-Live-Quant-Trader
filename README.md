# Kraken Live Quant Trader

An experimental, auditable cryptocurrency trading engine for Kraken with real-order execution, multi-asset scanning, adaptive exits, cooldowns, and portfolio-level risk controls.

> [!CAUTION]
> This program can place real orders using real money. It is research software, not financial advice, and it has not been independently audited. Read [RISK_DISCLOSURE.md](RISK_DISCLOSURE.md), review the entire source, restrict API permissions, and validate the strategy in paper trading before considering live use.

## Highlights

- Multi-asset Kraken universe scan
- Closed-candle signal evaluation to reduce look-ahead bias
- MACD, volume, regime, and conviction gates
- Hard stops, break-even floors, adaptive trailing exits, and cooldowns
- Atomic JSON state writes
- CSV audit trail and event logging
- Background pattern-engine integration
- Account-wide drawdown kill switch

## Requirements

- Python 3.10+
- A Kraken account and API key
- API permissions limited to balance/order queries and trading
- **Withdrawals disabled**

Install dependencies:

```sh
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
```

## Configuration

Copy the example file and enter your own credentials locally:

```sh
cp .env.example .env
```

Never commit `.env`. Create a dedicated API key and leave withdrawal permissions disabled.

## Running

```sh
python quant_trader.py
```

The script writes runtime state, audit rows, pattern data, and logs beside the source. Those files are excluded from version control.

## Before live use

1. Read every order-placement and exit path.
2. Confirm pair names, minimum order sizes, precision, and fee assumptions against current Kraken rules.
3. Run with a sandbox or paper-trading adaptation.
4. Start with capital you can afford to lose.
5. Monitor the first sessions continuously.
6. Confirm the kill switch behaves as expected.

## Architecture

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## License

[MIT](LICENSE)
