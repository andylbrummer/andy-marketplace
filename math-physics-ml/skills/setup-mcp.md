---
name: setup-mcp
description: Install Math-Physics-ML MCP servers with intelligent detection - supports local installation, slop-mcp, or standard Claude configuration
---

# Math-Physics-ML MCP Server Setup

This skill provides adaptive installation of the Math-Physics-ML MCP servers. It detects your environment and configures the MCP servers appropriately.

## Overview

The Math-Physics-ML plugin includes 5 MCP servers:
1. **math-mcp** - Symbolic algebra (SymPy) and GPU-accelerated numerical computing
2. **quantum-mcp** - Wave mechanics and Schrodinger equation simulations
3. **molecular-mcp** - Classical molecular dynamics simulations
4. **neural-mcp** - Neural network training and experimentation
5. **superpredictor-mcp** - Probabilistic forecasting with Bayesian updates, Fermi estimation, and prediction markets

These can be registered in two ways:
1. **Via slop-mcp** - Centralized management with search, discovery, and orchestration
2. **Via Claude config** - Standard MCP configuration in Claude Code settings

## Prerequisites

The Math-Physics-ML servers require:
- **Python 3.10+**
- **uv** package manager (preferred) or pip
- **math-mcp repository** cloned locally

Install uv if not present:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Installation Flow

### Step 1: Locate Math-MCP Repository

Check common installation locations:

```bash
# Check common locations
MATH_MCP_DIRS=(
  "$HOME/work/math-mcp"
  "$HOME/projects/math-mcp"
  "$HOME/math-mcp"
  "$PWD/math-mcp"
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
git clone https://github.com/beagle/math-mcp.git ~/work/math-mcp
cd ~/work/math-mcp
uv sync
```

**Record the math-mcp directory path** for use in registration.

### Step 2: Verify Installation

Test that the MCP servers can start:

```bash
cd /path/to/math-mcp
uv run math-mcp --help
uv run quantum-mcp --help
uv run molecular-mcp --help
uv run neural-mcp --help
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

When slop-mcp is available, register all 5 MCP servers for centralized management.

#### Ask User for Scope Preference

Present the user with scope options:

| Scope | Location | Use Case |
|-------|----------|----------|
| `user` | `~/.config/slop-mcp/config.kdl` | Personal setup, persists across projects |
| `project` | `.slop-mcp.kdl` | Team-shared, committed to repo |
| `memory` | Runtime only | Temporary, CI environments |

Default recommendation: `user` for persistent personal installation.

#### Check if Already Registered

Look for any of the math-mcp servers in the manage_mcps list response. Report status for each.

#### Register All MCP Servers

Replace `<MATH_MCP_PATH>` with the actual path to the math-mcp repository.

**Register math-mcp:**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "math-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "math-mcp"],
  "scope": "<user's choice>"
}
```

**Register quantum-mcp:**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "quantum-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "quantum-mcp"],
  "scope": "<user's choice>"
}
```

**Register molecular-mcp:**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "molecular-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "molecular-mcp"],
  "scope": "<user's choice>"
}
```

**Register neural-mcp:**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "neural-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<MATH_MCP_PATH>", "neural-mcp"],
  "scope": "<user's choice>"
}
```

**Register superpredictor-mcp:**
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
Parameters: { "query": "symbolic", "mcp_name": "math-mcp" }
```

If tools are returned, registration was successful. Repeat for other servers:
- quantum-mcp: search for "wavefunction"
- molecular-mcp: search for "particles"
- neural-mcp: search for "train"
- superpredictor-mcp: search for "bayesian"

### Step 4B: Standard Installation (No slop-mcp)

When slop-mcp is not available, configure via Claude Code's MCP settings.

#### Verify math-mcp Repository

```bash
# Check if math-mcp directory exists and is configured
if [ -d "/home/beagle/work/math-mcp" ]; then
  cd /home/beagle/work/math-mcp
  uv sync  # Ensure dependencies are installed
  echo "Math-MCP repository ready"
else
  echo "Math-MCP repository not found"
  echo "Clone it: git clone https://github.com/beagle/math-mcp.git ~/work/math-mcp"
fi
```

#### Create MCP Configuration

Create or update Claude Code's MCP configuration file:

**Location**: `~/.config/claude/claude_desktop_config.json`

Add all five MCP servers:

```json
{
  "mcpServers": {
    "math-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "math-mcp"]
    },
    "quantum-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "quantum-mcp"]
    },
    "molecular-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "molecular-mcp"]
    },
    "neural-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "neural-mcp"]
    },
    "superpredictor-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/math-mcp", "scicomp-superpredictor-mcp"]
    }
  }
}
```

Replace `/path/to/math-mcp` with your actual math-mcp installation path.

#### Restart Claude Code

After configuration, restart Claude Code to load the new MCP servers.

#### Troubleshooting

If tools are not available:
1. Verify paths in configuration are correct
2. Ensure uv is installed and in PATH
3. Run `uv sync` in the math-mcp directory to install dependencies
4. Check Claude Code logs for errors
5. Restart Claude Code completely

## Available Tools After Setup

### math-mcp Tools
| Tool | Description |
|------|-------------|
| `symbolic_solve` | Solve equations symbolically |
| `symbolic_diff` | Compute symbolic derivatives |
| `symbolic_integrate` | Compute symbolic integrals |
| `symbolic_simplify` | Simplify expressions |
| `create_array` | Create NumPy/CuPy arrays |
| `matrix_multiply` | GPU-accelerated matrix multiplication |
| `solve_linear_system` | Solve Ax=b systems |
| `fft` | Fast Fourier Transform |
| `ifft` | Inverse FFT |
| `optimize_function` | Numerical optimization |
| `find_roots` | Root finding algorithms |

### quantum-mcp Tools
| Tool | Description |
|------|-------------|
| `create_lattice_potential` | Create periodic lattice potentials |
| `create_custom_potential` | Create custom potential functions |
| `create_gaussian_wavepacket` | Initialize Gaussian wave packets |
| `create_plane_wave` | Initialize plane wave states |
| `solve_schrodinger` | Time-evolve 1D Schrodinger equation |
| `solve_schrodinger_2d` | Time-evolve 2D Schrodinger equation |
| `analyze_wavefunction` | Extract physical observables |
| `visualize_potential` | Generate potential plots |
| `render_video` | Create animation of time evolution |

### molecular-mcp Tools
| Tool | Description |
|------|-------------|
| `create_particles` | Initialize particle configurations |
| `run_md` | Run molecular dynamics simulation |
| `analyze_trajectory` | Analyze simulation trajectories |
| `compute_rdf` | Radial distribution function |
| `compute_msd` | Mean square displacement |

### neural-mcp Tools
| Tool | Description |
|------|-------------|
| `define_model` | Define neural network architecture |
| `load_dataset` | Load training/test datasets |
| `train_model` | Train neural network |
| `evaluate_model` | Evaluate model performance |
| `hyperparameter_tuning` | Automated hyperparameter search |

### superpredictor-mcp Tools (27)
| Tool | Description |
|------|-------------|
| `bayesian_update` | Update probability with Bayes' theorem |
| `bayesian_chain` | Apply multiple sequential Bayesian updates |
| `fermi_estimate` | Multiply factors with uncertainty propagation |
| `fermi_decompose` | Get suggestions for decomposing a question |
| `aggregate_forecasts` | Combine forecasts (mean, median, geometric, extremized) |
| `confidence_interval` | Calculate Wilson score confidence intervals |
| `create_prediction` | Store a new prediction |
| `resolve_prediction` | Record actual outcome |
| `get_calibration` | Calculate calibration statistics (Brier score, log score) |
| `list_predictions` | Query stored predictions |
| `search_metaculus` | Search Metaculus questions |
| `get_metaculus_question` | Get community prediction |
| `search_polymarket` | Search Polymarket prediction markets |
| `get_polymarket_market` | Get market prices and volume |
| `compare_to_markets` | Compare forecast to market consensus |
| `search_base_rates` | Search for historical base rates |
| `get_base_rate` | Get a specific base rate |
| `suggest_base_rate` | Find relevant base rates for a question |
| `fuzzy_evidence_confidence` | Evaluate confidence from evidence quality |
| `fuzzy_risk_assessment` | Assess risk from probability, impact, controllability |
| `problog_run` | Run raw ProbLog program |
| `problog_diagnostic` | Diagnostic reasoning with test sensitivity/specificity |
| `problog_causal` | Causal chain analysis |

## Quick Test

Test math-mcp:
```
Call: mcp__math-mcp__symbolic_solve
Parameters: { "equations": "x**2 - 4", "variables": "x" }
```

Test quantum-mcp:
```
Call: mcp__quantum-mcp__create_gaussian_wavepacket
Parameters: { "x0": 0, "sigma": 1, "k0": 5, "num_points": 256 }
```

Test superpredictor-mcp:
```
Call: mcp__superpredictor-mcp__bayesian_update
Parameters: { "prior": 0.1, "likelihood_given_h": 0.9, "likelihood_given_not_h": 0.3 }
```

## Summary Output

After setup, provide the user with:

1. **Math-MCP repository location**: Path to the installation
2. **Installation method used**: slop-mcp or standard
3. **Scope** (if slop-mcp): user/project/memory
4. **Registered servers**: List of all 5 MCP servers
5. **Verification status**: Tools available and working
6. **GPU availability**: Whether CUDA/CuPy is available for acceleration
7. **Next steps**: Suggest running `/solve`, `/integrate`, `/quantum-sim`, `/predict`, or `/fermi` commands
