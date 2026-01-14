---
name: solve
description: Solve equations symbolically using SymPy
---

# Symbolic Equation Solver

Solve algebraic equations, systems of equations, and differential equations using symbolic computation.

## Usage

Provide an equation or system of equations to solve. The solver handles:
- Polynomial equations
- Transcendental equations
- Systems of linear/nonlinear equations
- Ordinary differential equations

## Examples

**Quadratic equation:**
```
/math-mcp:solve x^2 - 5x + 6 = 0
```

**System of equations:**
```
/math-mcp:solve x + y = 10, 2x - y = 5
```

**Differential equation:**
```
/math-mcp:solve y'' + 4y = 0
```

## MCP Tool

```
Call: mcp__math-mcp__symbolic_solve
Parameters: {
  "equations": "<equation string>",
  "variables": "<comma-separated variables>"
}
```
