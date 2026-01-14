---
name: setup-mcp
description: Install superpredictor-mcp MCP server with intelligent detection - supports local installation via uv, slop-mcp registration
---

# Superpredictor-MCP Server Setup

This skill provides adaptive installation of the superpredictor-mcp MCP server for probabilistic forecasting and prediction tracking.

## Overview

superpredictor-mcp can be registered in two ways:
1. **Via slop-mcp** - Centralized management with search, discovery, and orchestration
2. **Via Claude config** - Standard MCP configuration in Claude Code settings

The MCP server runs via uv from the math-mcp monorepo.

## Prerequisites

- **Python 3.11+**
- **uv** package manager
- **math-mcp repository** cloned locally

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
uv run scicomp-superpredictor-mcp --help
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

When slop-mcp is available, register superpredictor-mcp for centralized management.

#### Check if Already Registered

Look for "superpredictor-mcp" in the manage_mcps list response. If already registered, report status and skip registration.

#### Ask User for Scope Preference

Present the user with scope options:

| Scope | Location | Use Case |
|-------|----------|----------|
| `user` | `~/.config/slop-mcp/config.kdl` | Personal setup, persists across projects |
| `project` | `.slop-mcp.kdl` | Team-shared, committed to repo |
| `memory` | Runtime only | Temporary, CI environments |

Default recommendation: `user` for persistent personal installation.

#### Register superpredictor-mcp

Replace `<MATH_MCP_PATH>` with the actual path (e.g., `/home/username/work/math-mcp`):

```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "superpredictor-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "scicomp-superpredictor-mcp"],
  "scope": "<user's choice>"
}
```

#### Verify Registration

```
Call: mcp__plugin_slop-mcp_slop-mcp__search_tools
Parameters: { "query": "bayesian", "mcp_name": "superpredictor-mcp" }
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
    "superpredictor-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "scicomp-superpredictor-mcp"]
    }
  }
}
```

Replace `/path/to/math-mcp` with your actual math-mcp installation path.

#### Restart Claude Code

After configuration, restart Claude Code to load the new MCP server.

## Available Tools After Setup

### Bayesian Reasoning
| Tool | Description |
|------|-------------|
| `bayesian_update` | Update probability with Bayes' theorem |
| `bayesian_chain` | Apply multiple sequential updates |

### Fermi Estimation
| Tool | Description |
|------|-------------|
| `fermi_estimate` | Multiply factors with uncertainty propagation |
| `fermi_decompose` | Get suggestions for decomposing a question |

### Forecast Aggregation
| Tool | Description |
|------|-------------|
| `aggregate_forecasts` | Combine forecasts (mean, median, geometric, extremized) |
| `confidence_interval` | Calculate Wilson score confidence intervals |

### Prediction Tracking
| Tool | Description |
|------|-------------|
| `create_prediction` | Store a new prediction |
| `resolve_prediction` | Record actual outcome |
| `get_calibration` | Calculate calibration statistics |
| `list_predictions` | Query stored predictions |

### Prediction Markets
| Tool | Description |
|------|-------------|
| `search_metaculus` | Search Metaculus questions |
| `get_metaculus_question` | Get community prediction |
| `search_polymarket` | Search Polymarket markets |
| `get_polymarket_market` | Get market prices |
| `compare_to_markets` | Compare forecast to consensus |

### Base Rates
| Tool | Description |
|------|-------------|
| `search_base_rates` | Search for historical base rates |
| `get_base_rate` | Get a specific base rate |
| `suggest_base_rate` | Find relevant base rates |

### Fuzzy Logic & ProbLog
| Tool | Description |
|------|-------------|
| `fuzzy_evidence_confidence` | Evaluate confidence from evidence quality |
| `fuzzy_risk_assessment` | Assess risk from multiple factors |
| `problog_run` | Run ProbLog program |
| `problog_diagnostic` | Diagnostic reasoning |
| `problog_causal` | Causal chain analysis |

## Quick Test

Bayesian update:
```
Call: mcp__superpredictor-mcp__bayesian_update
Parameters: {
  "prior": 0.1,
  "likelihood_given_h": 0.9,
  "likelihood_given_not_h": 0.3
}
```

## Summary Output

After setup, provide the user with:

1. **Math-MCP repository location**: Path to the installation
2. **Installation method used**: slop-mcp or standard
3. **Scope** (if slop-mcp): user/project/memory
4. **Verification status**: Tools available and working
5. **Next steps**: Suggest running `/superpredictor-mcp:predict` or `/superpredictor-mcp:fermi` commands
