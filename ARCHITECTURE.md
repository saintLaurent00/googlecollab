# Architecture

## System boundary

The trading logic is independent from the execution venue.

```
                    Trading Engine
                         |
                   Execution Port
                    /           \
             Simulator          MT5
```

## Engines

### Market Data
Provides historical/replayed market events and builds H1, M15 and M1 market views.

### Market Regime Engine
Classifies the current environment:

- UPTREND
- DOWNTREND
- RANGE
- UNKNOWN

It also tracks trend strength and volatility.

### Setup Engine
Finds and scores Supply/Demand zones, validates retests and evaluates M15 structure.

### Entry Engine
Works on M1 and identifies the precise micro-entry using microstructure, momentum and EMA context.

### Decision Engine
Consumes market, setup, batch and risk state and emits controlled actions:

- WAIT
- CREATE_BATCH
- OPEN_POSITION
- HOLD
- MODIFY_POSITION
- CLOSE_POSITION
- CLOSE_BATCH
- STOP_BATCH
- EMERGENCY_CLOSE

### Risk Engine
Authorizes or rejects actions based on exposure, drawdown, execution cost, volatility and configured risk limits.

### Batch Engine
Creates and manages groups of micro-trades. The working baseline is 7 positions, configurable.

### Position Engine
Maintains the complete state of every open and closed position.

### Execution Engine
Translates approved actions into execution requests through an ExecutionPort.

### Exit Engine
Evaluates batch and position exits using P&L, microstructure, momentum, time-in-trade and risk state.

### Performance Engine
Computes trading statistics from simulation results.

## Event flow

```
MarketEvent
    ↓
State Update
    ↓
Strategy Analysis
    ↓
Decision
    ↓
Risk Authorization
    ↓
Order
    ↓
Execution
    ↓
Position Update
    ↓
Portfolio / Batch Update
```

## Design principles

1. Simulation and live execution use the same trading logic.
2. The strategy never bypasses the risk layer.
3. Market state, setup state, batch state and portfolio state remain explicit.
4. No future market data may enter a decision made at an earlier timestamp.
5. Transaction costs and execution effects are part of evaluation.
6. Parameters are configurable and must be validated through out-of-sample testing.
