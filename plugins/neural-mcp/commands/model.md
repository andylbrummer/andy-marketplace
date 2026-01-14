---
name: model
description: Define neural network architectures
---

# Model Definition

Define neural network architectures for training.

## Usage

Specify the architecture type and configuration to create a model.

## Examples

**Multi-layer perceptron:**
```
/neural-mcp:model mlp with 784 inputs, hidden [256, 128], 10 outputs
```

**Convolutional network:**
```
/neural-mcp:model cnn for 28x28 images, 10 classes
```

**Custom architecture:**
```
/neural-mcp:model custom with layers: conv2d(32), relu, maxpool, flatten, linear(10)
```

## MCP Tool

```
Call: mcp__neural-mcp__define_model
Parameters: {
  "architecture": "<mlp|cnn|rnn|transformer|custom>",
  "input_size": <input dimensions>,
  "hidden_sizes": [<hidden layer sizes>],
  "output_size": <output dimensions>,
  "activation": "<relu|tanh|sigmoid|gelu>"
}
```

## Supported Architectures

| Type | Description |
|------|-------------|
| `mlp` | Multi-layer perceptron |
| `cnn` | Convolutional neural network |
| `rnn` | Recurrent neural network |
| `lstm` | Long short-term memory |
| `transformer` | Transformer architecture |
| `custom` | Custom layer specification |
