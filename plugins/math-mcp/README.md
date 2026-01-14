# Math-MCP Plugin

MCP server for symbolic algebra and GPU-accelerated numerical computing.

## Features

- **Symbolic Mathematics**: Solve equations, compute derivatives and integrals using SymPy
- **GPU Acceleration**: Optional CUDA support via CuPy for numerical operations
- **Linear Algebra**: Matrix operations, eigenvalue decomposition, system solving
- **Signal Processing**: FFT/IFFT with automatic GPU offloading

## Quick Start

1. Run `/math-mcp:setup-mcp` to install and configure the MCP server
2. Use `/math-mcp:solve` to solve equations
3. Use `/math-mcp:integrate` or `/math-mcp:derive` for calculus

## Requirements

- Python 3.11+
- uv package manager
- math-mcp repository (https://github.com/andylbrummer/math-mcp)

## Commands

| Command | Description |
|---------|-------------|
| `/math-mcp:solve` | Solve equations symbolically |
| `/math-mcp:integrate` | Compute integrals |
| `/math-mcp:derive` | Compute derivatives |
| `/math-mcp:fft` | Fast Fourier Transform |

## Installation

The `setup-mcp` skill will guide you through installation via slop-mcp or standard Claude configuration.
