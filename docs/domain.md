# Domain Model

## MarketEvent

A timestamped market observation used by the replay engine.

## MarketState

Current interpreted state of the market.

Includes:

- symbol
- timeframe
- regime
- trend direction
- trend strength
- volatility
- price
- technical features
- confidence
- timestamp

## Setup

A candidate trading opportunity derived from market context and zone/retest analysis.

## Signal

An approved setup candidate containing direction, entry context, quality and execution constraints.

## Batch

A group of related micro-trades managed collectively.

Core state:

- batch_id
- symbol
- direction
- position_ids
- status
- aggregate P&L
- profitable positions
- losing positions
- exposure
- timestamps

## Position

An individual trade with:

- position_id
- batch_id
- symbol
- side
- quantity
- entry price
- current price
- stop loss
- take profit
- realized P&L
- unrealized P&L
- status
- timestamps

## ExecutionPort

Abstraction between the trading engine and the execution implementation.

Implementations:

- Simulated execution
- Future MT5 execution
