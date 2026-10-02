# GoogleCollab

Automated XAUUSD micro-scalping system connected to a real MetaTrader 5 account.

## Objective

Analyze XAUUSD, detect short-duration opportunities, manage batches of micro-trades, and send real orders to MetaTrader 5 through a dedicated execution gateway.

This repository is designed for real execution. Strict risk controls are mandatory. Initial operation should use a demo account or minimal permitted exposure.

## Timeframes

- H1 — market context and major structure
- M15 — setup and Supply/Demand retest
- M1 — precise micro-scalping entry
- Ticks — real-time execution and monitoring

## Production flow

MT5 → Gateway → Market Data → Regime → Setup → M1 Entry → Decision → Risk → Batch → Order Manager → MT5

## Execution boundary

The Rust trading engine is broker-agnostic. A dedicated MT5 gateway handles communication with the installed MetaTrader 5 terminal.

The official MetaTrader Python integration communicates with the terminal; therefore the gateway must run on a machine where MT5 is installed and logged into the target account. Google Colab is the research/engine environment, not the MT5 terminal.

## Batch

Working baseline: XAUUSD, 7 positions, configurable.

Batch closure depends on aggregate P&L, profitable-position count, exposure, drawdown, market state and execution conditions. Green-position count alone is never sufficient.

## Security

Never commit MT5 credentials or gateway tokens.

## Status

Real MT5 execution architecture.
