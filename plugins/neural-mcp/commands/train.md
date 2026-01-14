---
name: train
description: Train neural networks with PyTorch
---

# Neural Network Training

Train neural network models with automatic GPU support.

## Usage

Provide a model definition and dataset to train. Supports various optimizers, learning rate schedules, and training callbacks.

## Examples

**Train MNIST classifier:**
```
/neural-mcp:train mnist_model on mnist dataset for 10 epochs
```

**Train with custom settings:**
```
/neural-mcp:train my_model with lr=0.001, batch_size=64, optimizer=adam
```

**Fine-tune pretrained:**
```
/neural-mcp:train pretrained_model with frozen base layers for 5 epochs
```

## MCP Tool

```
Call: mcp__neural-mcp__train_model
Parameters: {
  "model_id": "<model identifier>",
  "dataset_id": "<dataset identifier>",
  "epochs": <number of epochs>,
  "batch_size": <batch size>,
  "learning_rate": <learning rate>,
  "optimizer": "<optimizer name>"
}
```

## Notes

- Training automatically uses GPU if available
- Progress and loss are logged in real-time
- Checkpoints saved automatically
- Early stopping available
