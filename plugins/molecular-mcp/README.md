# Molecular-MCP Plugin

MCP server for classical molecular dynamics simulations with GPU acceleration.

## Features

- **Particle Systems**: Initialize random or lattice configurations
- **MD Simulation**: Velocity Verlet integration with Lennard-Jones potential
- **GPU Acceleration**: Optional CUDA support via CuPy
- **Analysis**: RDF, MSD, energy, temperature, pressure

## Quick Start

1. Run `/molecular-mcp:setup-mcp` to install and configure the MCP server
2. Use `/molecular-mcp:particles` to create a particle system
3. Use `/molecular-mcp:simulate` to run MD simulation
4. Use `/molecular-mcp:analyze` to compute properties

## Requirements

- Python 3.11+
- uv package manager
- math-mcp repository (https://github.com/andylbrummer/math-mcp)

## Commands

| Command | Description |
|---------|-------------|
| `/molecular-mcp:simulate` | Run MD simulation |
| `/molecular-mcp:particles` | Create particle systems |
| `/molecular-mcp:analyze` | Analyze trajectories |

## Example: Liquid Argon

```
1. Create 108 argon atoms at 300K
2. Equilibrate at 85K with velocity rescaling thermostat
3. Run NVE production for 50000 steps
4. Compute RDF and MSD
5. Calculate diffusion coefficient
```

## Installation

The `setup-mcp` skill will guide you through installation via slop-mcp or standard Claude configuration.
