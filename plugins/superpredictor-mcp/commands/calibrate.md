---
name: calibrate
description: Track prediction calibration and scoring
---

# Calibration Tracking

Track your prediction accuracy and calibration over time.

## Usage

Resolve predictions and analyze your forecasting performance.

## Examples

**Resolve prediction:**
```
/superpredictor-mcp:calibrate resolve prediction-123 as true
```

**Get calibration stats:**
```
/superpredictor-mcp:calibrate stats for all predictions
```

**Category breakdown:**
```
/superpredictor-mcp:calibrate stats for tag:technology
```

## MCP Tools

**Resolve prediction:**
```
Call: mcp__superpredictor-mcp__resolve_prediction
Parameters: {
  "prediction_id": "<prediction identifier>",
  "outcome": <true|false>
}
```

**Get calibration:**
```
Call: mcp__superpredictor-mcp__get_calibration
Parameters: {
  "tags": ["<optional tag filter>"],
  "date_range": {"start": "YYYY-MM-DD", "end": "YYYY-MM-DD"}
}
```

**List predictions:**
```
Call: mcp__superpredictor-mcp__list_predictions
Parameters: {
  "status": "<pending|resolved|all>",
  "tags": ["<tag filter>"]
}
```

## Metrics

| Metric | Description | Ideal |
|--------|-------------|-------|
| Brier Score | Mean squared error | 0 (perfect) |
| Log Score | Logarithmic scoring | Higher better |
| Calibration | Predicted vs actual | Diagonal line |
| Resolution | Separation of outcomes | Higher better |
