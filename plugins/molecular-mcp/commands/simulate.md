---
name: simulate
description: Run molecular dynamics simulations
---

# Molecular Dynamics Simulation

Run classical molecular dynamics simulations with Lennard-Jones potentials.

## Usage

Initialize a particle system and evolve it in time using velocity Verlet integration.

## Examples

**Argon liquid simulation:**
```
/molecular-mcp:simulate 108 argon atoms at 300K for 10000 steps
```

**Equilibration run:**
```
/molecular-mcp:simulate particles with thermostat at 85K
```

**Production run:**
```
/molecular-mcp:simulate NVE ensemble for 50000 steps, save trajectory
```

## MCP Tool

```
Call: mcp__molecular-mcp__run_md
Parameters: {
  "particles_id": "<particles identifier>",
  "num_steps": <number of steps>,
  "dt": <time step in reduced units>,
  "thermostat": "<none|velocity_rescale|nose_hoover>",
  "target_temperature": <target T (if thermostat)>,
  "save_interval": <steps between saves>
}
```

## Notes

- Uses Lennard-Jones potential for interactions
- Periodic boundary conditions applied
- GPU acceleration available with CuPy
- Trajectories saved in HDF5 format
