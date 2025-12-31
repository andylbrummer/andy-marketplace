# Molecular MCP Assistant

Use this skill when the user asks about molecular dynamics simulations, particle systems, or needs to:
- Create particle systems for simulation
- Run classical MD simulations (NVE, NVT, NPT ensembles)
- Analyze trajectories and compute structural properties
- Calculate radial distribution functions (RDF) or mean squared displacement (MSD)

## Available Tools

The Molecular MCP server provides these tools:

### System Setup
- `create_particles` - Create particle systems with positions, velocities, and masses
- `info` - Get overview of server capabilities

### Simulation
- `run_md` - Run molecular dynamics simulation
- `get_task_status` - Monitor long-running simulation progress

### Analysis
- `analyze_trajectory` - Compute properties from simulation trajectory
- `compute_rdf` - Calculate radial distribution function g(r)
- `compute_msd` - Calculate mean squared displacement for diffusion analysis

## Usage Examples

### Simple Lennard-Jones fluid simulation
```
1. Use create_particles with n_particles=1000, box_size=[10, 10, 10], arrangement="random"
2. Use run_md with system_id, n_steps=10000, dt=0.001, ensemble="NVE"
3. Use compute_rdf with trajectory_id to analyze structure
```

### Temperature-controlled simulation
```
1. Use create_particles with n_particles=500, box_size=[8, 8, 8]
2. Use run_md with ensemble="NVT", temperature=1.0, thermostat="nose-hoover"
```

### Diffusion coefficient calculation
```
1. Run an NVE or NVT simulation
2. Use compute_msd with the trajectory_id
3. Fit the MSD vs time slope: D = MSD / (6 * t)
```

## Ensembles

- **NVE** - Microcanonical (constant energy)
- **NVT** - Canonical (constant temperature via thermostat)
- **NPT** - Isothermal-isobaric (constant T and P)

## GPU Acceleration

Set `use_gpu: true` for GPU-accelerated force calculations and neighbor list construction. Provides >10x speedup for large systems.

## Units

The system uses reduced Lennard-Jones units:
- Energy: epsilon
- Length: sigma
- Mass: m
- Time: tau = sigma * sqrt(m/epsilon)

## Performance Tips

- Use neighbor lists for large systems (>1000 particles)
- GPU acceleration recommended for >500 particles
- Typical dt: 0.001-0.005 in reduced units
- Equilibrate 1000-5000 steps before production runs
