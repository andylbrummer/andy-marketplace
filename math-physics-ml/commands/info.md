---
description: Get information about available scientific computing tools
allowed-tools: mcp__math-mcp__info, mcp__quantum-mcp__info, mcp__molecular-mcp__info, mcp__neural-mcp__info
---

# Scientific Computing Info

Display an overview of all available MCP servers and their capabilities.

## Input

$ARGUMENTS

## Instructions

If the user asks about a specific domain, query that server's info tool.
Otherwise, provide a summary of all available servers.

## Available Servers

### Math MCP
Symbolic algebra and GPU-accelerated numerical computing.
- **Symbolic**: solve, differentiate, integrate, simplify
- **Numerical**: arrays, matrix operations, linear systems
- **Transforms**: FFT, IFFT
- **Optimization**: minimize, find roots

### Quantum MCP
Wave mechanics and Schrodinger equation simulations.
- **Potentials**: lattice, custom
- **Wavepackets**: Gaussian, plane wave
- **Solvers**: 1D/2D split-step Fourier
- **Analysis**: observables, visualization

### Molecular MCP
Classical molecular dynamics simulations.
- **Systems**: particle creation, initialization
- **Simulation**: NVE, NVT, NPT ensembles
- **Analysis**: RDF, MSD, trajectory analysis

### Neural MCP
Neural network training and experimentation.
- **Models**: ResNet, VGG, DenseNet, custom
- **Training**: optimizers, schedulers, callbacks
- **Evaluation**: metrics, predictions
- **Tuning**: hyperparameter search

## GPU Acceleration

All servers support GPU acceleration via CuPy when CUDA is available.
Use `use_gpu: true` on supported operations.

## Response

Based on the input, either:
1. Call the relevant `info` tool for detailed capability listing
2. Provide this overview if the query is general
