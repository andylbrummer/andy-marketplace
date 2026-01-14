---
name: model
description: Create and configure language model architectures
---

# Model Definition

Create GPT, Mamba, or custom language model architectures.

## Usage

Specify architecture type and configuration to create a model.

## Examples

**Small GPT:**
```
/llm-mcp:model gpt with 6 layers, 384 dim, 6 heads
```

**Mamba model:**
```
/llm-mcp:model mamba with 12 layers, 768 dim
```

**Load pretrained:**
```
/llm-mcp:model load gpt2-medium
```

## MCP Tools

**Create GPT:**
```
Call: mcp__llm-mcp__create_model
Parameters: {
  "architecture": "gpt",
  "num_layers": <number of layers>,
  "hidden_size": <hidden dimension>,
  "num_heads": <attention heads>,
  "vocab_size": <vocabulary size>,
  "max_seq_len": <max sequence length>
}
```

**Create Mamba:**
```
Call: mcp__llm-mcp__create_model
Parameters: {
  "architecture": "mamba",
  "num_layers": <number of layers>,
  "hidden_size": <hidden dimension>,
  "state_size": <SSM state size>,
  "vocab_size": <vocabulary size>
}
```

**Load pretrained:**
```
Call: mcp__llm-mcp__load_pretrained
Parameters: {
  "model_name": "<huggingface model name>"
}
```

## Architectures

| Type | Description |
|------|-------------|
| `gpt` | GPT-style decoder-only transformer |
| `mamba` | Mamba state-space model |
| `hybrid` | Transformer + SSM hybrid |
