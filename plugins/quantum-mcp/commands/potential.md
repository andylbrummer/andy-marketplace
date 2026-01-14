---
name: potential
description: Create quantum potential functions (lattice, barrier, harmonic, custom)
---

# Potential Creation

Define potential energy functions for quantum simulations.

## Usage

Create various potentials to define the quantum mechanical system.

## Examples

**Harmonic oscillator:**
```
/quantum-mcp:potential harmonic with omega=1
```

**Double barrier:**
```
/quantum-mcp:potential double barrier at x=-2 and x=2, height=10
```

**Periodic lattice:**
```
/quantum-mcp:potential lattice with 10 wells, depth=5
```

**Custom potential:**
```
/quantum-mcp:potential V(x) = x^4 - x^2
```

## MCP Tools

**Harmonic potential:**
```
Call: mcp__quantum-mcp__create_harmonic_potential
Parameters: {
  "omega": <angular frequency>,
  "x0": <center>,
  "num_points": <grid points>
}
```

**Lattice potential:**
```
Call: mcp__quantum-mcp__create_lattice_potential
Parameters: {
  "num_wells": <number of wells>,
  "well_depth": <depth>,
  "well_width": <width>
}
```

**Custom potential:**
```
Call: mcp__quantum-mcp__create_custom_potential
Parameters: {
  "expression": "<V(x) expression>",
  "x_min": <minimum x>,
  "x_max": <maximum x>,
  "num_points": <grid points>
}
```
