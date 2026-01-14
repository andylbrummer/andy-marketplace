# Quantum-MCP Plugin

MCP server for wave mechanics and Schrodinger equation simulations.

## Features

- **Wave Mechanics**: Solve time-dependent Schrodinger equation in 1D and 2D
- **GPU Acceleration**: Optional CUDA support via CuPy for fast simulations
- **Visualization**: Generate plots and animations of quantum evolution
- **Flexible Potentials**: Built-in and custom potential functions

## Quick Start

1. Run `/quantum-mcp:setup-mcp` to install and configure the MCP server
2. Use `/quantum-mcp:potential` to define a potential
3. Use `/quantum-mcp:wavepacket` to create initial state
4. Use `/quantum-mcp:simulate` to evolve the system

## Requirements

- Python 3.11+
- uv package manager
- math-mcp repository (https://github.com/andylbrummer/math-mcp)

## Commands

| Command | Description |
|---------|-------------|
| `/quantum-mcp:simulate` | Run Schrodinger equation simulation |
| `/quantum-mcp:wavepacket` | Create wave packets |
| `/quantum-mcp:potential` | Define potential functions |

## Example: Double-Slit Interference

```
1. Create a double-slit potential
2. Initialize a Gaussian wavepacket
3. Evolve the system for 1000 time steps
4. Render video of the interference pattern
```

## Installation

The `setup-mcp` skill will guide you through installation via slop-mcp or standard Claude configuration.
