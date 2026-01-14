---
name: simulate
description: Run time-dependent Schrodinger equation simulation
---

# Quantum Simulation

Simulate quantum mechanical systems by solving the time-dependent Schrodinger equation.

## Usage

Set up a potential and initial wavefunction, then evolve the system in time. Supports 1D and 2D simulations with optional GPU acceleration.

## Examples

**Double-slit interference:**
```
/quantum-mcp:simulate double slit with 5 slits, evolve for 1000 steps
```

**Tunneling through barrier:**
```
/quantum-mcp:simulate wavepacket tunneling through potential barrier
```

**Harmonic oscillator:**
```
/quantum-mcp:simulate harmonic oscillator ground state
```

## MCP Tools

**1D Simulation:**
```
Call: mcp__quantum-mcp__solve_schrodinger
Parameters: {
  "potential_id": "<potential identifier>",
  "wavefunction_id": "<wavefunction identifier>",
  "dt": <time step>,
  "num_steps": <number of steps>
}
```

**2D Simulation:**
```
Call: mcp__quantum-mcp__solve_schrodinger_2d
Parameters: {
  "potential_id": "<potential identifier>",
  "wavefunction_id": "<wavefunction identifier>",
  "dt": <time step>,
  "num_steps": <number of steps>
}
```

## Notes

- Results can be rendered to video with `render_video` tool
- Physical observables extracted with `analyze_wavefunction`
- GPU acceleration available with CuPy
