# Neural MCP Assistant

Use this skill when the user asks about neural network training, deep learning experiments, or needs to:
- Define neural network architectures
- Load and prepare datasets
- Train models with various optimizers
- Evaluate model performance
- Run hyperparameter tuning

## Available Tools

The Neural MCP server provides these tools:

### Model Definition
- `define_model` - Create neural network architectures (ResNet, VGG, custom)
- `info` - Get overview of available architectures and options

### Data Loading
- `load_dataset` - Load standard datasets (MNIST, CIFAR10, ImageNet, etc.)
- `create_dataloader` - Create data loaders with batching and augmentation

### Training
- `train_model` - Train models with configurable optimizer, scheduler, and callbacks
- `get_training_status` - Monitor training progress

### Evaluation
- `evaluate_model` - Compute metrics on test sets
- `get_predictions` - Generate predictions on new data

### Hyperparameter Tuning
- `hyperparameter_tuning` - Search for optimal hyperparameters

## Usage Examples

### Train a CNN on CIFAR-10
```
1. Use define_model with architecture="resnet18", num_classes=10
2. Use load_dataset with dataset_name="CIFAR10", split="train"
3. Use train_model with model_id, dataset_id, epochs=50, optimizer="adam", lr=0.001
```

### Custom architecture
```
Use define_model with architecture="custom", layers=[
  {"type": "conv2d", "in_channels": 3, "out_channels": 64, "kernel": 3},
  {"type": "relu"},
  {"type": "maxpool", "kernel": 2},
  {"type": "flatten"},
  {"type": "linear", "out_features": 10}
]
```

### Hyperparameter search
```
Use hyperparameter_tuning with:
  model_id, dataset_id,
  search_space={
    "lr": [0.0001, 0.001, 0.01],
    "batch_size": [32, 64, 128],
    "optimizer": ["adam", "sgd"]
  },
  n_trials=20
```

## Available Architectures

- **ResNet**: resnet18, resnet34, resnet50, resnet101
- **VGG**: vgg11, vgg16, vgg19
- **DenseNet**: densenet121, densenet169
- **MobileNet**: mobilenet_v2, mobilenet_v3
- **Custom**: Define layer-by-layer

## Optimizers

- `sgd` - Stochastic Gradient Descent (with momentum option)
- `adam` - Adaptive Moment Estimation
- `adamw` - Adam with weight decay
- `rmsprop` - RMSProp

## Learning Rate Schedulers

- `step` - Step decay
- `cosine` - Cosine annealing
- `plateau` - Reduce on plateau
- `warmup` - Linear warmup

## GPU Acceleration

Training automatically uses available GPUs. For multi-GPU:
- Set `distributed: true` for DataParallel
- Use `n_gpus` to limit GPU count

## Callbacks

Available training callbacks:
- `early_stopping` - Stop when validation loss plateaus
- `checkpoint` - Save best model weights
- `tensorboard` - Log metrics for visualization
