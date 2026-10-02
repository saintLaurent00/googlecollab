# GoogleCollab

Automated XAUUSD micro-scalping research and simulation engine.

## Objective

Build an automated trading system that can identify market conditions, detect trading setups, manage batches of micro-trades, and evaluate the strategy in a fully simulated environment before any live broker integration.

## Timeframes

- **H1** — market context and major structure
- **M15** — setup and Supply/Demand retest validation
- **M1** — precise micro-scalping entry trigger
- **Tick data** — execution and position monitoring when available

## Core flow

Market Data → Market Regime → Setup → Entry → Decision → Risk → Batch → Execution → Exit → Performance

## Simulation first

The first execution target is a virtual broker. No real orders are part of the initial system.

The same trading engine will later be able to target different execution adapters:

- Simulator
- MT5/Broker adapter

## Batch model

A batch groups multiple micro-trades and is managed collectively.

The initial design uses a configurable batch size (7 as the working baseline), while decisions are based on:

- profitable-position count
- aggregate batch P&L
- exposure
- drawdown
- market regime
- setup validity
- execution costs

A profitable-position count alone is never sufficient to close a batch.

## Architecture

```
H1
 ↓
Market Regime
 ↓
M15 Setup
 ↓
M1 Entry
 ↓
Decision Engine
 ↓
Risk Engine
 ↓
Batch Engine
 ↓
Simulated Broker
 ↓
Exit / Performance
```

## Status

Architecture phase → simulation core implementation.
