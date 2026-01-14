---
name: train
description: Train and fine-tune language models
---

# LLM Training

Train language models from scratch or fine-tune pretrained models.

## Usage

Provide a model and dataset to train. Supports distributed training and mixed precision.

## Examples

**Train small GPT:**
```
/llm-mcp:train gpt-small on shakespeare dataset for 1000 steps
```

**Fine-tune pretrained:**
```
/llm-mcp:train gpt2 fine-tuned on custom_corpus
```

**Mamba model:**
```
/llm-mcp:train mamba-130m on wikitext for 5000 steps
```

## MCP Tool

```
Call: mcp__llm-mcp__train_model
Parameters: {
  "model_id": "<model identifier>",
  "dataset_id": "<dataset identifier>",
  "num_steps": <training steps>,
  "batch_size": <batch size>,
  "learning_rate": <learning rate>,
  "warmup_steps": <warmup steps>,
  "gradient_accumulation": <accumulation steps>
}
```

## Training Features

| Feature | Description |
|---------|-------------|
| Mixed precision | FP16/BF16 training |
| Gradient checkpointing | Memory efficient |
| Learning rate schedules | Cosine, linear, constant |
| Logging | Wandb, TensorBoard |
| Checkpointing | Auto-save and resume |
