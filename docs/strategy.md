# Strategy Specification

## Trading objective

Short-duration XAUUSD micro-scalping.

The system is designed to exploit small intraday price movements rather than hold conventional long-duration positions.

## Multi-timeframe model

### H1 — context

Identify:

- market structure
- major Supply zones
- major Demand zones
- directional context
- volatility context

### M15 — setup

Validate:

- price interaction with a valid H1 zone
- retest quality
- local structure
- directional compatibility

### M1 — entry

Validate:

- microstructure break
- momentum
- EMA alignment
- candle/price-action quality
- spread and execution conditions

## Signal pipeline

```
H1 context
   ↓
Valid zone
   ↓
M15 retest
   ↓
M15 setup validation
   ↓
M1 trigger
   ↓
Hard filters
   ↓
Setup score
   ↓
Decision Engine
```

## Hard rejection conditions

The strategy must be able to refuse a trade when:

- spread exceeds the configured maximum
- expected movement does not justify transaction costs
- volatility is outside the permitted regime
- market regime is unknown
- setup/zone is invalid
- risk limits are already reached

## Setup score

The score is a quality measure, not a guaranteed probability of profit.

Candidate features include:

- H1 structure
- zone quality
- zone freshness
- impulse strength
- retest quality
- M15 structure
- M1 microstructure
- momentum
- volatility
- spread
- expected movement
- execution quality

Weights are not considered final until validated with historical data.

## Exit

The system evaluates:

- individual P&L
- aggregate batch P&L
- profitable-position count
- microstructure reversal
- momentum deterioration
- time in trade
- risk state

The batch should not be closed solely because a percentage of positions are green.

## Validation

No live capital is required for the initial validation stage.

The strategy must first pass:

1. deterministic backtesting
2. out-of-sample testing
3. walk-forward testing
4. paper/simulation execution
5. cost and slippage sensitivity analysis
