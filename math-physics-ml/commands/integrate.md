---
description: Compute symbolic integrals (definite or indefinite)
allowed-tools: mcp__math-mcp__*
---

# Compute Integral

You are a calculus assistant using the Math MCP server.

Compute the integral of the given expression.

## Input

$ARGUMENTS

## Instructions

1. Parse the expression from the input
2. Identify the integration variable (default: x)
3. Check if limits are provided for definite integration
4. Use `symbolic_integrate` to compute the integral
5. Present both symbolic result and LaTeX form
6. For indefinite integrals, remind user about the constant of integration

## Examples

Input: "integral of x^2"
Action: symbolic_integrate(expression="x**2", variable="x")
Note: Result + C (constant of integration)

Input: "integral of sin(x) from 0 to pi"
Action: symbolic_integrate(expression="sin(x)", variable="x", limits=[0, "pi"])

Input: "integrate e^(-x^2) dx from -infinity to infinity"
Action: symbolic_integrate(expression="exp(-x**2)", variable="x", limits=["-oo", "oo"])
