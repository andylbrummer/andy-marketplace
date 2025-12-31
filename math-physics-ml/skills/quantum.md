# Quantum MCP Assistant

Use this skill when the user asks about quantum mechanics simulations, wave mechanics, or needs to:
- Create and simulate quantum potentials
- Generate wave packets (Gaussian, plane waves)
- Solve the time-dependent Schrodinger equation
- Analyze wavefunctions and compute observables
- Visualize quantum simulations

## Available Tools

The Quantum MCP server provides these tools:

### Potential Creation
- `create_lattice_potential` - Create crystalline lattice potentials (square, hexagonal, triangular)
- `create_custom_potential` - Create custom potentials from mathematical functions

### Wavepacket Creation
- `create_gaussian_wavepacket` - Create localized Gaussian wave packets with momentum
- `create_plane_wave` - Create plane wave states

### Schrodinger Equation Solver
- `solve_schrodinger` - 1D time-dependent solver using split-step Fourier method
- `solve_schrodinger_2d` - 2D time-dependent solver

### Async Task Management
- `get_task_status` - Monitor long-running simulation status
- `get_simulation_result` - Retrieve completed simulation data

### Analysis & Visualization
- `analyze_wavefunction` - Compute observables (position, momentum, energy, norm)
- `visualize_potential` - Plot potential energy landscape
- `render_video` - Animate probability density evolution

## Usage Examples

### Simulate a particle in a harmonic oscillator
```
1. Use create_custom_potential with grid_size=[256], function="0.5 * (x - 128)**2"
2. Use create_gaussian_wavepacket with grid_size=[256], position=[100], momentum=[2.0], width=5.0
3. Use solve_schrodinger with the potential_id, initial_state, time_steps=1000, dt=0.1
```

### Create and analyze a wavepacket
```
1. Use create_gaussian_wavepacket with grid_size=[512], position=[256], momentum=[1.0]
2. Use analyze_wavefunction with the returned wavefunction
```

### 2D Lattice simulation
```
1. Use create_lattice_potential with lattice_type="hexagonal", grid_size=[128, 128], depth=5.0
2. Use create_gaussian_wavepacket with grid_size=[128, 128], position=[64, 64], momentum=[0.5, 0.5]
3. Use solve_schrodinger_2d with the potential and wavepacket
```

## GPU Acceleration

Set `use_gpu: true` on solver tools for CUDA-accelerated FFT operations. Provides 5-10x speedup on typical simulations.

## Async Operations

Long-running simulations (>100 time steps) run asynchronously:
1. `solve_schrodinger` returns a `task_id` immediately
2. Use `get_task_status` to poll progress
3. Use `get_simulation_result` to retrieve completed data

## Physical Units

Default units are dimensionless. The solver uses:
- hbar = 1
- m = 1
- dx = 1
Scale parameters accordingly for physical systems.
