---
description: Run a molecular dynamics simulation
allowed-tools: mcp__molecular-mcp__*
---

# Molecular Dynamics Simulation

You are a computational chemistry assistant using the Molecular MCP server.

Set up and run classical molecular dynamics simulations.

## Input

$ARGUMENTS

## Instructions

1. Parse the user's request to determine:
   - Number of particles
   - System size (box dimensions)
   - Ensemble (NVE, NVT, NPT)
   - Simulation length and timestep
2. Create the particle system
3. Run the MD simulation
4. Analyze the trajectory

## Workflow

### Step 1: Create System
```
create_particles(
  n_particles=<N>,
  box_size=[Lx, Ly, Lz],
  arrangement="random" or "fcc",
  temperature=<T>  # for initial velocity distribution
)
```

### Step 2: Run Simulation
```
run_md(
  system_id=<id>,
  n_steps=<steps>,
  dt=0.001,
  ensemble="NVE" | "NVT" | "NPT",
  temperature=<T>,  # for NVT/NPT
  pressure=<P>,     # for NPT
  use_gpu=true      # for large systems
)
```

### Step 3: Analyze
- `compute_rdf(trajectory_id=<id>)` - Structure analysis
- `compute_msd(trajectory_id=<id>)` - Diffusion coefficient
- `analyze_trajectory(trajectory_id=<id>)` - Energy, temperature, pressure

## Examples

Input: "simulate 1000 argon atoms at room temperature"
Action:
1. create_particles(n_particles=1000, box_size=[15, 15, 15], temperature=1.0)
2. run_md(system_id=<id>, n_steps=10000, dt=0.002, ensemble="NVT", temperature=1.0)
3. compute_rdf(trajectory_id=<id>)

Input: "liquid-gas phase transition simulation"
Action: NVT simulation at multiple temperatures, analyze RDF evolution

Input: "compute diffusion coefficient"
Action: NVE/NVT production run, compute_msd, fit slope to get D
