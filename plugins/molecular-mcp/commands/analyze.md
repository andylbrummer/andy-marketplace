---
name: analyze
description: Analyze molecular dynamics trajectories
---

# Trajectory Analysis

Compute structural and dynamical properties from MD trajectories.

## Usage

Load a trajectory and compute various physical properties.

## Examples

**Radial distribution function:**
```
/molecular-mcp:analyze rdf from trajectory over last 5000 frames
```

**Mean square displacement:**
```
/molecular-mcp:analyze msd to compute diffusion coefficient
```

**Energy analysis:**
```
/molecular-mcp:analyze energy fluctuations and heat capacity
```

## MCP Tools

**Radial distribution function:**
```
Call: mcp__molecular-mcp__compute_rdf
Parameters: {
  "trajectory_id": "<trajectory identifier>",
  "num_bins": <number of bins>,
  "r_max": <maximum radius>
}
```

**Mean square displacement:**
```
Call: mcp__molecular-mcp__compute_msd
Parameters: {
  "trajectory_id": "<trajectory identifier>",
  "max_lag": <maximum lag time>
}
```

**Energy:**
```
Call: mcp__molecular-mcp__compute_energy
Parameters: {
  "particles_id": "<particles identifier>"
}
```

## Available Analyses

| Property | Description |
|----------|-------------|
| `rdf` | Radial distribution function g(r) |
| `msd` | Mean square displacement |
| `vacf` | Velocity autocorrelation function |
| `energy` | Potential, kinetic, total energy |
| `temperature` | Instantaneous temperature |
| `pressure` | Virial pressure |
