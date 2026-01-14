---
name: derive
description: Compute symbolic derivatives using SymPy
---

# Symbolic Differentiation

Compute derivatives, partial derivatives, and higher-order derivatives symbolically.

## Usage

Provide an expression and the variable(s) to differentiate with respect to.

## Examples

**First derivative:**
```
/math-mcp:derive x^3 + 2x with respect to x
```

**Partial derivative:**
```
/math-mcp:derive x^2*y^3 with respect to y
```

**Higher order:**
```
/math-mcp:derive sin(x) twice with respect to x
```

## MCP Tool

```
Call: mcp__math-mcp__symbolic_diff
Parameters: {
  "expression": "<expression>",
  "variable": "<differentiation variable>",
  "order": <order (default 1)>
}
```
