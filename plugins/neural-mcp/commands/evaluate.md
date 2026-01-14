---
name: evaluate
description: Evaluate neural network performance
---

# Model Evaluation

Evaluate trained models on test datasets.

## Usage

Provide a trained model and test dataset to compute metrics.

## Examples

**Evaluate on test set:**
```
/neural-mcp:evaluate my_model on test_dataset
```

**Get detailed metrics:**
```
/neural-mcp:evaluate classifier with confusion matrix and per-class metrics
```

## MCP Tool

```
Call: mcp__neural-mcp__evaluate_model
Parameters: {
  "model_id": "<model identifier>",
  "dataset_id": "<test dataset identifier>",
  "metrics": ["accuracy", "loss", "precision", "recall", "f1"]
}
```

## Available Metrics

| Metric | Description |
|--------|-------------|
| `accuracy` | Classification accuracy |
| `loss` | Loss function value |
| `precision` | Precision score |
| `recall` | Recall score |
| `f1` | F1 score |
| `confusion_matrix` | Full confusion matrix |
| `roc_auc` | ROC AUC score |
