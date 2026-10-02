# Simulation Engine

## Goal

Reproduce trading as an event-driven virtual market so the strategy can be tested without sending real broker orders.

## Pipeline

```
Historical XAUUSD data
        ↓
Market Replay
        ↓
H1 / M15 / M1 state
        ↓
Trading Engine
        ↓
Risk Engine
        ↓
Simulated Broker
        ↓
Virtual Positions
        ↓
Performance
```

## Market Replay

The replay engine advances strictly forward in time.

At each event it exposes only information available at that timestamp.

No future candle, tick, price or outcome may be visible to the strategy.

## Simulated Broker

The virtual broker models:

- account balance
- equity
- margin
- positions
- order lifecycle
- spread
- commission
- slippage
- realized P&L
- unrealized P&L
- execution rejection

## Execution

The strategy submits an execution request.

The simulator decides whether and at what price that request is filled according to configured execution rules.

## Results

Every run should produce:

- trades
- batches
- equity curve
- P&L
- drawdown
- win/loss statistics
- transaction costs
- slippage impact
- trade duration
- batch statistics

## Reproducibility

A simulation run must record its configuration, data range and parameters so that results can be reproduced.
