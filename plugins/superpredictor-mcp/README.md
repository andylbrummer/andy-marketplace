# Superpredictor-MCP Plugin

MCP server for probabilistic forecasting with Bayesian updates, Fermi estimation, and calibration tracking.

## Features

- **Bayesian Reasoning**: Update probabilities with evidence
- **Fermi Estimation**: Break down questions into estimable factors
- **Prediction Tracking**: Record and score your forecasts
- **Market Integration**: Query Metaculus and Polymarket
- **Calibration Analysis**: Track your forecasting accuracy

## Quick Start

1. Run `/superpredictor-mcp:setup-mcp` to install and configure the MCP server
2. Use `/superpredictor-mcp:predict` to make predictions
3. Use `/superpredictor-mcp:fermi` for estimation problems
4. Use `/superpredictor-mcp:calibrate` to track accuracy

## Requirements

- Python 3.11+
- uv package manager
- math-mcp repository (https://github.com/andylbrummer/math-mcp)

## Commands

| Command | Description |
|---------|-------------|
| `/superpredictor-mcp:predict` | Make and update predictions |
| `/superpredictor-mcp:fermi` | Fermi estimation |
| `/superpredictor-mcp:calibrate` | Track calibration |
| `/superpredictor-mcp:markets` | Query prediction markets |

## 27 Available Tools

### Bayesian
- `bayesian_update` - Single Bayes update
- `bayesian_chain` - Sequential updates

### Fermi
- `fermi_estimate` - Multiply with uncertainty
- `fermi_decompose` - Decomposition suggestions

### Predictions
- `create_prediction`, `resolve_prediction`, `list_predictions`, `get_calibration`

### Markets
- `search_metaculus`, `get_metaculus_question`
- `search_polymarket`, `get_polymarket_market`
- `compare_to_markets`

### Base Rates
- `search_base_rates`, `get_base_rate`, `suggest_base_rate`

### Advanced
- `fuzzy_evidence_confidence`, `fuzzy_risk_assessment`
- `problog_run`, `problog_diagnostic`, `problog_causal`
- `aggregate_forecasts`, `confidence_interval`

## Installation

The `setup-mcp` skill will guide you through installation via slop-mcp or standard Claude configuration.
