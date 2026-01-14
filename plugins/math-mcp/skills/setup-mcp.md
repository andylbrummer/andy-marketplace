---
name: setup-mcp
description: Install math-mcp MCP server with intelligent detection - supports local installation via uv, slop-mcp registration
---

# Math-MCP Server Setup

This skill provides adaptive installation of the math-mcp MCP server for symbolic algebra and GPU-accelerated numerical computing.

## Overview

math-mcp can be registered in two ways:
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
uv run scicomp-math-mcp --help
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

When slop-mcp is available, register math-mcp for centralized management.

#### Check if Already Registered

Look for "math-mcp" in the manage_mcps list response. If already registered, report status and skip registration.

#### Ask User for Scope Preference

Present the user with scope options:

| Scope | Location | Use Case |
|-------|----------|----------|
| `user` | `~/.config/slop-mcp/config.kdl` | Personal setup, persists across projects |
| `project` | `.slop-mcp.kdl` | Team-shared, committed to repo |
| `memory` | Runtime only | Temporary, CI environments |

Default recommendation: `user` for persistent personal installation.

#### Register math-mcp

Replace `<MATH_MCP_PATH>` with the actual path (e.g., `/home/username/work/math-mcp`):

```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "math-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "scicomp-math-mcp"],
  "scope": "<user's choice>"
}
```

#### Verify Registration

```
Call: mcp__plugin_slop-mcp_slop-mcp__search_tools
Parameters: { "query": "symbolic", "mcp_name": "math-mcp" }
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
    "math-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "scicomp-math-mcp"]
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
| `symbolic_solve` | Solve equations symbolically |
| `symbolic_diff` | Compute symbolic derivatives |
| `symbolic_integrate` | Compute symbolic integrals |
| `symbolic_simplify` | Simplify expressions |
| `symbolic_expand` | Expand expressions |
| `symbolic_factor` | Factor expressions |
| `create_array` | Create NumPy/CuPy arrays |
| `matrix_multiply` | GPU-accelerated matrix multiplication |
| `solve_linear_system` | Solve Ax=b systems |
| `fft` | Fast Fourier Transform |
| `ifft` | Inverse FFT |
| `optimize_function` | Numerical optimization |
| `find_roots` | Root finding algorithms |
| `eigenvalues` | Compute eigenvalues/eigenvectors |

## Quick Test

Test symbolic solving:
```
Call: mcp__math-mcp__symbolic_solve
Parameters: { "equations": "x**2 - 4", "variables": "x" }
```

Expected result: `x = -2, 2`

## Summary Output

After setup, provide the user with:

1. **Math-MCP repository location**: Path to the installation
2. **Installation method used**: slop-mcp or standard
3. **Scope** (if slop-mcp): user/project/memory
4. **Verification status**: Tools available and working
5. **GPU availability**: Whether CUDA/CuPy is available for acceleration
6. **Next steps**: Suggest running `/math-mcp:solve` or `/math-mcp:integrate` commands
