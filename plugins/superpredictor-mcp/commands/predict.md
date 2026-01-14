---
name: predict
description: Make and track probabilistic predictions with Bayesian updates
---

# Probabilistic Prediction

Create, update, and track probabilistic predictions with Bayesian reasoning.

## Usage

Make predictions, update them with new evidence, and track your calibration over time.

## Examples

**Create prediction:**
```
/superpredictor-mcp:predict "AI will pass Turing test by 2030" at 65%
```

**Bayesian update:**
```
/superpredictor-mcp:predict update prior 10% given evidence sensitivity 90%, false positive 30%
```

**Chain multiple updates:**
```
/superpredictor-mcp:predict chain updates: [weak evidence for], [strong evidence for], [moderate against]
```

## MCP Tools

**Create prediction:**
```
Call: mcp__superpredictor-mcp__create_prediction
Parameters: {
  "question": "<prediction question>",
  "probability": <probability 0-1>,
  "resolution_date": "<YYYY-MM-DD>",
  "tags": ["<tag1>", "<tag2>"]
}
```

**Bayesian update:**
```
Call: mcp__superpredictor-mcp__bayesian_update
Parameters: {
  "prior": <prior probability>,
  "likelihood_given_h": <P(evidence|hypothesis)>,
  "likelihood_given_not_h": <P(evidence|not hypothesis)>
}
```

**Chain updates:**
```
Call: mcp__superpredictor-mcp__bayesian_chain
Parameters: {
  "prior": <starting prior>,
  "evidence_chain": [
    {"likelihood_given_h": 0.8, "likelihood_given_not_h": 0.3},
    {"likelihood_given_h": 0.9, "likelihood_given_not_h": 0.1}
  ]
}
```

## Calibration

Track your predictions and measure calibration:
- **Brier Score**: Mean squared error of predictions
- **Log Score**: Logarithmic scoring rule
- **Calibration Curve**: Predicted vs. actual frequencies
