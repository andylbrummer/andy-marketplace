---
name: integrate
description: Compute symbolic integrals using SymPy
---

# Symbolic Integration

Compute indefinite and definite integrals symbolically.

## Usage

Provide an expression to integrate and optionally the variable and limits.

## Examples

**Indefinite integral:**
```
/math-mcp:integrate x^2 dx
```

**Definite integral:**
```
/math-mcp:integrate sin(x) from 0 to pi
```

**Multiple integrals:**
```
/math-mcp:integrate x*y dxdy over [0,1]x[0,1]
```

## MCP Tool

```
Call: mcp__math-mcp__symbolic_integrate
Parameters: {
  "expression": "<expression>",
  "variable": "<integration variable>",
  "lower": "<lower limit (optional)>",
  "upper": "<upper limit (optional)>"
}
```
