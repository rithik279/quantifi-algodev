# QuantiFi Algorithmic Trading Competition — Top 3

## Overview

**Top 3 — UTEFA QuantiFi Algorithmic Trading Competition**

- **24.3% simulated return**
- **1.78 Sharpe ratio**
- **252-trading-day competition horizon**

This repository documents the systematic strategy development, parameter research, Monte Carlo analysis, and risk controls used for the QuantiFi competition. All performance figures are simulated competition results, not live investment returns.

## Competition Objective

The competition provided five synthetic stocks, macroeconomic indicators, volume and momentum fields, a starting portfolio of $100,000, and a 252-day evaluation period. Strategies had to operate within the supplied market and portfolio interfaces while paying a 0.5% transaction fee on both purchases and sales.

The goal was to maximize final risk-adjusted portfolio value under those constraints—not simply maximize turnover or in-sample returns.

## Strategy

The submitted strategy combined:

- an EMA-based regime signal;
- cross-sectional momentum ranking;
- an ADX trend-strength filter;
- volatility and volume tilts;
- macro-sensitive exposure scaling;
- a concentrated three-stock basket;
- a 5% trailing stop; and
- explicit transaction-cost accounting.

The system shifted between invested and defensive states based on the trend regime, ranked eligible securities by momentum, adjusted position weights using risk indicators, and limited unnecessary trading in a high-fee environment.

## Research Process

The research workflow moved from the supplied contestant template to a parameterized strategy and repeatable evaluation loop:

1. preserve the competition's `Market` and `Portfolio` interfaces;
2. implement strategy state and decision logic in `Context` and `update_portfolio()`;
3. compare moving-average, momentum, concentration, stop, volatility, volume, and macro parameters;
4. record return, fee, trade-count, and risk-adjusted outcomes;
5. examine the best candidates rather than relying on a single hand-selected configuration; and
6. retain the final competition implementation separately from exploratory scripts.

## Monte Carlo / Optimization

The repository includes several complementary research paths:

- grid-search tooling for comparing parameter combinations;
- correlated geometric-Brownian-motion experiments;
- bootstrap simulations that avoid imposing a single parametric return distribution;
- economic-regime and indicator-conditioned simulations;
- portfolio outcome distributions;
- Value at Risk, drawdown, and sensitivity analysis; and
- conservative return adjustments intended to expose overfitting risk.

These experiments supported robustness analysis and strategy selection. They should be read as research tools, not as proof that historical or synthetic distributions will persist.

## Risk Management

Risk controls were embedded directly in the strategy:

- trailing stops limited sustained reversals;
- macro inputs scaled total exposure within bounded limits;
- volatility and volume information adjusted allocations;
- stock-count constraints limited concentration;
- trade-count and fee tracking made turnover economically visible;
- trend-strength filtering reduced participation in weak regimes; and
- portfolio value was evaluated net of the competition's transaction costs.

## Results

| Result | Value |
|---|---:|
| Competition placement | **Top 3** |
| Simulated return | **24.3%** |
| Sharpe ratio | **1.78** |
| Evaluation horizon | **252 trading days** |

These are competition-simulation results. They are not live performance, audited investment results, or evidence of future returns.

## Repository Structure

```text
.
├── OriginalScripts/
│   ├── UTEFA_QuantiFi_Contestant_Template.py   # Final competition strategy
│   └── UTEFA_QuantiFi_Backtesting_Script.py    # Supplied backtest framework
├── MonteCarlo/                                 # Robustness and distribution experiments
├── UTEFA_QuantiFi_Contestant_Template_testing.py
├── UTEFA_QuantiFi_Backtesting_Script_testing.py
├── optimization.py                             # Parameter-search workflow
├── grid_top10.json                             # Retained optimization summary
├── UTEFA_QuantiFi_Contestant_Dataset.csv       # Competition dataset
└── requirements.txt
```

## Attribution

UTEFA supplied the contestant scaffold, market/portfolio interfaces, dataset, and backtesting infrastructure. My work focused on the trading strategy, indicators, portfolio construction, parameter research, optimization experiments, Monte Carlo analysis, and risk-management logic built within that framework.

## Limitations

- Results come from a synthetic competition environment rather than live markets.
- The 252-day sample is too short to establish durable out-of-sample performance.
- Parameter searches can overfit the supplied dataset even when conservative scoring is used.
- Some Monte Carlo experiments rely on simplified distributional or resampling assumptions.
- The optimization outputs are exploratory artifacts and do not reproduce the official competition score by themselves.
- Transaction costs are modelled using the competition's fixed fee schedule; real execution would introduce spread, slippage, liquidity, and market-impact effects.

## What This Project Demonstrates

- systematic strategy development under explicit rules;
- translation of market signals into portfolio decisions;
- parameter optimization with transaction-cost awareness;
- Monte Carlo and sensitivity analysis;
- risk-adjusted evaluation rather than return-only selection;
- honest separation of supplied infrastructure from original strategy work; and
- disciplined reporting of simulated results and methodological limitations.
