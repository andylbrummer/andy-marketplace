---
name: fermi
description: Perform Fermi estimates with uncertainty propagation
---

# Fermi Estimation

Break down complex questions into simpler factors and multiply with uncertainty propagation.

## Usage

Decompose a question into estimable factors, assign ranges, and compute the combined estimate.

## Examples

**Simple estimation:**
```
/superpredictor-mcp:fermi "How many piano tuners in Chicago?"
```

**With explicit factors:**
```
/superpredictor-mcp:fermi multiply:
  - population: 2.7M (2.5M - 3M)
  - pianos per household: 0.03 (0.02 - 0.05)
  - tunings per year: 1 (0.5 - 2)
  - tunings per tuner per year: 500 (400 - 600)
```

**Get decomposition suggestions:**
```
/superpredictor-mcp:fermi decompose "Annual revenue of street food vendors in NYC"
```

## MCP Tools

**Fermi estimate:**
```
Call: mcp__superpredictor-mcp__fermi_estimate
Parameters: {
  "factors": [
    {"name": "factor1", "low": 100, "high": 200, "best": 150},
    {"name": "factor2", "low": 0.1, "high": 0.3, "best": 0.2}
  ],
  "operation": "multiply"
}
```

**Get decomposition:**
```
Call: mcp__superpredictor-mcp__fermi_decompose
Parameters: {
  "question": "<question to decompose>"
}
```

## Notes

- Uses log-normal distribution for multiplicative factors
- Propagates uncertainty correctly through multiplication
- Returns confidence intervals for final estimate
