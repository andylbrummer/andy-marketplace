---
name: setup-mcp
description: Install llm-mcp MCP server with intelligent detection - supports local installation via uv, slop-mcp registration
---

# LLM-MCP Server Setup

This skill provides adaptive installation of the llm-mcp MCP server for LLM training and experimentation.

## Overview

llm-mcp can be registered in two ways:
1. **Via slop-mcp** - Centralized management with search, discovery, and orchestration
2. **Via Claude config** - Standard MCP configuration in Claude Code settings

The MCP server runs via uv from the math-mcp monorepo.

## Prerequisites

- **Python 3.11+**
- **uv** package manager
- **math-mcp repository** cloned locally
- **PyTorch** (installed automatically)
- **Transformers** (installed automatically)

Install uv if not present:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Installation Flow

### Step 1: Locate Math-MCP Repository

Check common installation locations:

```bash
MATH_MCP_DIRS=(
  "$HOME/work/math-mcp"
  "$HOME/projects/math-mcp"
  "$HOME/math-mcp"
)

for dir in "${MATH_MCP_DIRS[@]}"; do
  if [ -d "$dir" ] && [ -f "$dir/pyproject.toml" ]; then
    echo "FOUND: $dir"
    break
  fi
done
```

If not found, clone the repository:
```bash
git clone https://github.com/andylbrummer/math-mcp.git ~/work/math-mcp
cd ~/work/math-mcp
uv sync
```

**Record the math-mcp directory path** for use in registration.

### Step 2: Verify Installation

Test that the MCP server can start:

```bash
cd /path/to/math-mcp
uv run scicomp-llm-mcp --help
```

### Step 3: Detect slop-mcp Availability

Check if slop-mcp is available:

```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: { "action": "list" }
```

**If successful** (returns list of MCPs): slop-mcp is available, proceed to Step 4A
**If tool not found or errors**: slop-mcp not available, proceed to Step 4B

### Step 4A: Install via slop-mcp

When slop-mcp is available, register llm-mcp for centralized management.

#### Check if Already Registered

Look for "llm-mcp" in the manage_mcps list response. If already registered, report status and skip registration.

#### Ask User for Scope Preference

Present the user with scope options:

| Scope | Location | Use Case |
|-------|----------|----------|
| `user` | `~/.config/slop-mcp/config.kdl` | Personal setup, persists across projects |
| `project` | `.slop-mcp.kdl` | Team-shared, committed to repo |
| `memory` | Runtime only | Temporary, CI environments |

Default recommendation: `user` for persistent personal installation.

#### Register llm-mcp

Replace `<MATH_MCP_PATH>` with the actual path (e.g., `/home/username/work/math-mcp`):

```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "llm-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "scicomp-llm-mcp"],
  "scope": "<user's choice>"
}
```

#### Verify Registration

```
Call: mcp__plugin_slop-mcp_slop-mcp__search_tools
Parameters: { "query": "tokenize", "mcp_name": "llm-mcp" }
```

If tools are returned, registration was successful.

### Step 4B: Standard Installation (No slop-mcp)

When slop-mcp is not available, configure via Claude Code's MCP settings.

#### Create MCP Configuration

Create or update Claude Code's MCP configuration file:

**Location**: `~/.config/claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "llm-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "scicomp-llm-mcp"]
    }
  }
}
```

Replace `/path/to/math-mcp` with your actual math-mcp installation path.

#### Restart Claude Code

After configuration, restart Claude Code to load the new MCP server.

## Available Tools After Setup

| Tool | Description |
|------|-------------|
| `create_model` | Create GPT or Mamba model |
| `load_pretrained` | Load pretrained model |
| `tokenize_text` | Tokenize text with various tokenizers |
| `load_dataset` | Load training datasets |
| `train_model` | Train/fine-tune LLM |
| `generate_text` | Generate text from model |
| `evaluate_perplexity` | Compute perplexity on dataset |
| `save_checkpoint` | Save model checkpoint |
| `load_checkpoint` | Load model checkpoint |

## Quick Test

Tokenize some text:
```
Call: mcp__llm-mcp__tokenize_text
Parameters: {
  "text": "Hello, world!",
  "tokenizer": "gpt2"
}
```

## Summary Output

After setup, provide the user with:

1. **Math-MCP repository location**: Path to the installation
2. **Installation method used**: slop-mcp or standard
3. **Scope** (if slop-mcp): user/project/memory
4. **Verification status**: Tools available and working
5. **GPU availability**: Whether CUDA is available for training
6. **Next steps**: Suggest running `/llm-mcp:model` or `/llm-mcp:train` commands
