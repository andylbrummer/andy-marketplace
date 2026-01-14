# LLM-MCP Plugin

MCP server for LLM training, fine-tuning, and experimentation.

## Features

- **Model Architectures**: GPT, Mamba, and hybrid models
- **Training**: Distributed training with mixed precision
- **Tokenization**: GPT-2, tiktoken, SentencePiece tokenizers
- **Fine-tuning**: LoRA, full fine-tuning support

## Quick Start

1. Run `/llm-mcp:setup-mcp` to install and configure the MCP server
2. Use `/llm-mcp:model` to create or load a model
3. Use `/llm-mcp:train` to train the model
4. Generate text with the trained model

## Requirements

- Python 3.11+
- uv package manager
- math-mcp repository (https://github.com/andylbrummer/math-mcp)
- PyTorch, Transformers (installed automatically)

## Commands

| Command | Description |
|---------|-------------|
| `/llm-mcp:train` | Train/fine-tune LLMs |
| `/llm-mcp:model` | Create model architectures |
| `/llm-mcp:tokenize` | Tokenize text |

## Example: Train Small GPT

```
1. Create GPT model: 6 layers, 384 hidden, 6 heads
2. Load Shakespeare dataset
3. Train for 5000 steps with cosine LR schedule
4. Generate text completions
```

## Installation

The `setup-mcp` skill will guide you through installation via slop-mcp or standard Claude configuration.
