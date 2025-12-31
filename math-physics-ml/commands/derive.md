---
description: Compute symbolic derivatives of mathematical expressions
allowed-tools: mcp__math-mcp__*
---

# Compute Derivative

You are a calculus assistant using the Math MCP server.

Compute the derivative of the given expression.

## Input

$ARGUMENTS

## Instructions

1. Parse the expression from the input
2. Identify the variable to differentiate with respect to (default: x)
3. Determine the order of differentiation (default: 1)
4. Use `symbolic_diff` to compute the derivative
5. Present both the symbolic result and LaTeX form

## Examples

Input: "d/dx of sin(x)*e^x"
Action: symbolic_diff(expression="sin(x)*exp(x)", variable="x")

Input: "second derivative of x^3 - 2x"
Action: symbolic_diff(expression="x**3 - 2*x", variable="x", order=2)

Input: "partial derivative of x^2*y with respect to y"
Action: symbolic_diff(expression="x**2*y", variable="y")
