# Math-Physics-ML Plugin

GPU-accelerated MCP plugin for computational mathematics, quantum physics simulations, molecular dynamics, and neural network training.

## Features

This plugin provides access to 4 MCP servers:

| Server | Description | Tools |
|--------|-------------|-------|
| **math-mcp** | Symbolic algebra & GPU numerical computing | 12 tools |
| **quantum-mcp** | Wave mechanics & Schrodinger simulations | 12 tools |
| **molecular-mcp** | Classical molecular dynamics | 13 tools |
| **neural-mcp** | Neural network training | 15 tools |

## Installation

### Prerequisites

1. Install the math-mcp project:
```bash
cd ~/work/math-mcp
uv sync --all-extras
```

2. Install the plugin:
```bash
# From Claude Code
claude plugins install ./math-physics-ml

# Or add to your plugins directory
cp -r math-physics-ml ~/.claude/plugins/
```

## Usage

### Slash Commands

| Command | Description |
|---------|-------------|
| `/math-physics-ml:solve` | Solve mathematical equations |
| `/math-physics-ml:derive` | Compute symbolic derivatives |
| `/math-physics-ml:integrate` | Compute symbolic integrals |
| `/math-physics-ml:fft` | Fast Fourier Transform |
| `/math-physics-ml:quantum-sim` | Run quantum simulations |
| `/math-physics-ml:md-sim` | Run molecular dynamics |
| `/math-physics-ml:train` | Train neural networks |
| `/math-physics-ml:info` | Server capabilities overview |

### Skills (AI-Invocable)

The plugin includes skills that Claude can invoke automatically:

- **math** - Symbolic math and numerical computing
- **quantum** - Quantum mechanics simulations
- **molecular** - Molecular dynamics simulations
- **neural** - Neural network training

### Direct MCP Tool Access

All MCP tools are available with the prefix `mcp__<server>__<tool>`:

```
mcp__math-mcp__symbolic_solve
mcp__quantum-mcp__create_gaussian_wavepacket
mcp__molecular-mcp__run_md
mcp__neural-mcp__train_model
```

## Quick Start Examples

Just describe what you want in natural language:

### Mathematics & Calculus
```
Find all solutions to x^4 - 13x^2 + 36 = 0

Compute the integral of e^(-x^2) from negative infinity to infinity

What's the Taylor series expansion of ln(1+x) around x=0 to 5th order?

Solve the system: 3x + 2y - z = 1, x - y + 2z = 4, 2x + y - z = -1
```

### Signal Processing
```
Analyze a noisy signal with hidden frequencies at 50Hz and 120Hz

Create a 1024-point chirp signal and show its spectrogram

Filter out frequencies above 100Hz from my audio data
```

### Quantum Physics
```
Create a video of a Gaussian wave packet passing through a triple slit

Simulate quantum tunneling through a potential barrier and compute transmission probability

Show the time evolution of a particle in a 2D hexagonal lattice potential

Compare interference patterns for single, double, and triple slit experiments
```

### Molecular Dynamics
```
Simulate 500 argon atoms equilibrating to a liquid at reduced temperature 0.8

Run an NVT simulation of a Lennard-Jones fluid and compute the radial distribution function

Calculate the diffusion coefficient of particles in a dense fluid

Model a phase transition by slowly heating a solid from T=0.5 to T=1.5
```

### Neural Networks
```
Train a ResNet-18 to classify CIFAR-10 images with cosine annealing

Compare Adam vs SGD optimizers on MNIST with learning rates from 0.0001 to 0.01

Find the best hyperparameters for a VGG-16 model on my image dataset

Train a custom CNN with 3 conv layers and evaluate on the test set
```

### Multi-Domain Problems
```
Use FFT to analyze the frequency spectrum of a quantum wavefunction

Compute the diffusion coefficient from MD and compare to Einstein relation

Train a neural network to predict molecular potential energy surfaces
```

## GPU Acceleration

All servers support CUDA GPU acceleration via CuPy. Set `use_gpu: true` on supported operations for significant speedups:

| Operation | CPU | GPU | Speedup |
|-----------|-----|-----|---------|
| Matrix multiply (1000x1000) | ~100ms | ~1ms | 100x |
| 1D Schrodinger (1000 steps) | ~30s | ~5s | 6x |
| MD simulation (100k steps) | minutes | seconds | >10x |

## Configuration

The MCP servers are configured in `.mcp.json`. Modify paths if your math-mcp installation is in a different location:

```json
{
  "mcpServers": {
    "math-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "math-mcp"]
    }
  }
}
```

## Testing

```bash
# Test the plugin loads correctly
claude --plugin-dir ./math-physics-ml

# Verify MCP servers are accessible
claude mcp list
```

## License

MIT
