---
description: Train a neural network model
allowed-tools: mcp__neural-mcp__*
---

# Train Neural Network

You are a machine learning assistant using the Neural MCP server.

Set up and train neural network models.

## Input

$ARGUMENTS

## Instructions

1. Parse the user's request to determine:
   - Dataset (MNIST, CIFAR10, custom)
   - Architecture (ResNet, VGG, custom)
   - Training parameters (epochs, learning rate, optimizer)
2. Load the dataset
3. Define the model
4. Train with appropriate settings
5. Evaluate on test set

## Workflow

### Step 1: Load Dataset
```
load_dataset(
  dataset_name="CIFAR10" | "MNIST" | "ImageNet",
  split="train",
  augmentation=true
)
```

### Step 2: Define Model
```
define_model(
  architecture="resnet18" | "vgg16" | "custom",
  num_classes=<N>,
  pretrained=false
)
```

### Step 3: Train
```
train_model(
  model_id=<id>,
  dataset_id=<id>,
  epochs=50,
  optimizer="adam",
  lr=0.001,
  batch_size=64,
  scheduler="cosine"
)
```

### Step 4: Evaluate
```
evaluate_model(model_id=<id>, dataset_id=<test_dataset_id>)
```

## Examples

Input: "train resnet18 on cifar10 for 100 epochs"
Action:
1. load_dataset(dataset_name="CIFAR10", split="train")
2. define_model(architecture="resnet18", num_classes=10)
3. train_model(model_id=<id>, dataset_id=<id>, epochs=100, optimizer="adam", lr=0.001)
4. evaluate_model on test split

Input: "quick mnist classifier"
Action: Simple CNN, 10 epochs, evaluate

Input: "hyperparameter search for best learning rate"
Action: hyperparameter_tuning with lr search space
