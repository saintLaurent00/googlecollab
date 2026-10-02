# Development

## Initial target

Build the simulation environment before broker integration.

## Development order

1. Domain types
2. Market event/replay engine
3. Simulated broker
4. Portfolio and position accounting
5. Batch engine
6. Market regime engine
7. Setup engine
8. Entry engine
9. Decision engine
10. Exit engine
11. Performance engine
12. Backtesting and validation tooling

## Non-negotiable tests

- deterministic market replay
- no look-ahead bias
- order/position accounting
- batch accounting
- spread/commission/slippage
- stop and emergency close behavior
- simultaneous position tracking
- reproducible backtest results
