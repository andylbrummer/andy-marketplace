# Neural-MCP Plugin

MCP server for neural network training and experimentation with PyTorch.

## Features

- **Model Definition**: Define MLP, CNN, RNN, Transformer architectures
- **Training**: GPU-accelerated training with logging and checkpoints
- **Evaluation**: Comprehensive metrics and visualization
- **Hyperparameter Tuning**: Automated search for optimal parameters

## Quick Start

1. Run `/neural-mcp:setup-mcp` to install and configure the MCP server
2. Use `/neural-mcp:model` to define an architecture
3. Use `/neural-mcp:train` to train the model
4. Use `/neural-mcp:evaluate` to assess performance

## Requirements

- Python 3.11+
- uv package manager
- math-mcp repository (https://github.com/andylbrummer/math-mcp)
- PyTorch (installed automatically)

## Commands

| Command | Description |
|---------|-------------|
| `/neural-mcp:train` | Train neural networks |
| `/neural-mcp:model` | Define architectures |
| `/neural-mcp:evaluate` | Evaluate performance |

## Example: MNIST Classification

```
1. Define MLP model with 784 inputs, hidden [256, 128], 10 outputs
2. Load MNIST dataset
3. Train for 10 epochs with Adam optimizer
4. Evaluate on test set
```

## Installation

The `setup-mcp` skill will guide you through installation via slop-mcp or standard Claude configuration.
