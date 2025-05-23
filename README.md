# Intraday Noise Area Momentum Strategy on NQ Futures (with Breadth Filter)

## Overview

This repository implements and backtests an intraday momentum strategy inspired by [this concept](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4824172), with an added **breadth-based risk filter** to avoid trading during unfavorable macro conditions.

The core idea:
- Define a “Noise Area” based on recent price action.
- Enter long or short trades when the price breaks above or below this Noise Area.
- Manage risk using the Noise Area boundaries and intraday VWAP as dynamic stops.
- **Trades are only allowed when the breadth model indicates a risk-on regime.**

The strategy is tested on NQ E-mini futures, incorporating realistic transaction costs.

---

## Strategy Logic

1. **Noise Area Calculation**:
   - Based on the recent intraday range or volatility.

2. **Entry Rules**:
   - **Long**: Price breaks above the upper Noise Area boundary.
   - **Short**: Price breaks below the lower Noise Area boundary.
   - **Condition**: No trade is taken unless the breadth model is in *risk-on* mode.

3. **Exit Rules**:
   - Stop-losses are dynamically set using the opposite boundary of the Noise Area or intraday VWAP.
   - No fixed profit targets; exits are reactive to intraday structure.

4. **Transaction Costs**:
   - A commission and slippage assumption of **$30 round-trip** is included.

---

## Backtest Details

- **Instrument**: NQ E-mini Futures (CME)
- **Data Frequency**: Intraday (e.g., 1-minute or 5-minute bars)
- **Initial Capital**: \$100,000
- **Transaction Costs**: \$30 per round-trip
- **Metrics Evaluated**:
  - Cumulative Returns
  - Volatility
  - Drawdown
  - Sharpe ratio
  - Calmar ratio

