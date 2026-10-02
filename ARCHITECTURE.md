# Production Architecture

## Topology

MT5 Terminal (real account)
→ MT5 Gateway
→ authenticated connection
→ Rust Trading Engine
→ Decision/Risk/Batch/Order Management
→ MT5 Gateway
→ Broker

## Engines

- Market Data
- Market Regime
- Setup
- Entry
- Decision
- Risk
- Batch
- Position
- Exit
- Execution
- State

## MT5 Gateway

The gateway is the only component allowed to communicate with MetaTrader 5.

Responsibilities:
- connect to terminal
- retrieve account state
- retrieve ticks and candles
- retrieve positions
- validate orders
- send orders
- close/modify positions
- report execution results
- expose connection health

## Real execution lifecycle

MT5 tick
→ Market State
→ Regime
→ Setup
→ M1 Entry
→ Decision
→ Risk
→ Order Request
→ order_check
→ order_send
→ Broker
→ Position Synchronization

## Position synchronization

Local state is never assumed to be authoritative.

At startup and continuously:
MT5 positions → Position Sync → Local State → Batch State

This handles restarts, rejected orders, manual intervention and connection loss.

## Order identity

Every bot order uses a unique magic number and correlation ID.

The bot must distinguish its own positions from manual positions and other EAs and must never close unrelated positions.

## Failure policy

If MT5 connectivity is lost:
- stop opening new positions
- mark market/account state stale
- reconnect
- resynchronize positions
- resume only after synchronization succeeds

## Deployment

Recommended:
Google Colab / Rust Engine
→ authenticated outbound connection
→ Windows VPS
→ MT5 Terminal + MT5 Gateway

A local Windows host can be used during development.

## Security

Credentials belong only in environment variables or a secret manager.
