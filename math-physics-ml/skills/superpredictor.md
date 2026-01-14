# Superpredictor MCP Assistant

Use this skill when the user asks about probabilistic forecasting, prediction, estimation, or reasoning under uncertainty involving:
- Bayesian probability updates with new evidence
- Fermi estimation and back-of-envelope calculations
- Aggregating multiple forecasts or expert opinions
- Tracking predictions and measuring calibration
- Consulting prediction markets (Metaculus, Polymarket)
- Reference class forecasting with base rates
- Fuzzy logic for qualitative uncertainty
- Probabilistic logic programming (ProbLog)

## Available Tools (27)

The Superpredictor MCP server provides these tools:

### Bayesian Reasoning
- `bayesian_update` - Update probability with single piece of evidence using Bayes' theorem
- `bayesian_chain` - Apply multiple sequential Bayesian updates

### Fermi Estimation
- `fermi_estimate` - Multiply factors with uncertainty propagation (90% confidence bounds)
- `fermi_decompose` - Get suggestions for decomposing a question into estimable factors

### Forecast Aggregation
- `aggregate_forecasts` - Combine forecasts (mean, median, geometric, extremized, trimmed)
- `confidence_interval` - Calculate Wilson score confidence intervals

### Prediction Tracking
- `create_prediction` - Store a new prediction with probability and reasoning
- `resolve_prediction` - Record actual outcome for calibration
- `get_calibration` - Calculate calibration statistics (Brier score, log score)
- `list_predictions` - Query stored predictions

### External Markets
- `search_metaculus` - Search Metaculus questions
- `get_metaculus_question` - Get community prediction for a question
- `search_polymarket` - Search Polymarket prediction markets
- `get_polymarket_market` - Get market prices and volume
- `get_polymarket_events` - Browse trending events
- `compare_to_markets` - Compare your forecast to market consensus

### Base Rate Database
- `search_base_rates` - Search for historical base rates
- `get_base_rate` - Get a specific base rate by event type
- `list_base_rate_categories` - List categories (startups, markets, science, etc.)
- `suggest_base_rate` - Find relevant base rates for a question

### Fuzzy Logic
- `fuzzy_evidence_confidence` - Evaluate confidence from evidence quality
- `fuzzy_risk_assessment` - Assess risk from probability, impact, controllability
- `list_fuzzy_systems` - List available pre-built fuzzy systems

### Probabilistic Logic (ProbLog)
- `problog_run` - Run raw ProbLog program
- `problog_diagnostic` - Diagnostic reasoning with test sensitivity/specificity
- `problog_causal` - Causal chain analysis
- `problog_alarm_example` - Classic Bayesian network example
- `list_problog_examples` - List available examples

## Usage Examples

### Update probability with new evidence
```
Use bayesian_update with prior=0.1, likelihood_given_h=0.9, likelihood_given_not_h=0.3
```
Result: posterior ~0.25 (likelihood ratio = 3)

### Fermi estimation
```
Use fermi_estimate with question="Piano tuners in Chicago" and factors:
- Population: 2M-4M
- Pianos per capita: 1%-5%
- Tunings per year: 1-3
- Tunings per tuner/year: 500-2000
```
Returns estimate with 90% confidence bounds.

### Find base rates for reference class forecasting
```
Use suggest_base_rate with question="Will this AI startup succeed?"
```
Returns: startup_failure (75%), startup_unicorn (1%), ai_capability_claim_true (30%)

### Diagnostic reasoning (medical test interpretation)
```
Use problog_diagnostic with:
- disease_prior=0.01 (1% base rate)
- test_sensitivity=0.95 (95% true positive)
- test_specificity=0.90 (90% true negative)
- test_result=true (got positive result)
```
Returns posterior probability of disease (~8.8%)

### Compare your forecast to prediction markets
```
Use compare_to_markets with your_forecast=0.7, metaculus_id=12345
```
Returns comparison with market consensus and calibration insights.

## Base Rate Categories

| Category | Examples |
|----------|----------|
| startups | Failure rates, unicorn odds, funding success |
| technology | Software project failure, AI claims accuracy |
| geopolitics | War, regime change, sanctions |
| markets | Market crashes, recessions, IPOs |
| science | Clinical trials, replication rates |
| personal | Resolutions, diets, marriage |

## Best Practices

1. **Start with base rates** - Use `suggest_base_rate` before making predictions
2. **Decompose uncertainty** - Use `fermi_decompose` to break down complex questions
3. **Update incrementally** - Use `bayesian_chain` for multiple evidence pieces
4. **Check markets** - Use `compare_to_markets` to sanity-check your forecasts
5. **Track calibration** - Use `create_prediction` and `resolve_prediction` to improve over time
