---
name: particles
description: Create and initialize particle systems
---

# Particle System Initialization

Create particle configurations for molecular dynamics simulations.

## Usage

Initialize particles with specified positions, velocities, and properties.

## Examples

**Random configuration:**
```
/molecular-mcp:particles 108 argon atoms in a box of size 10
```

**FCC lattice:**
```
/molecular-mcp:particles fcc lattice of 256 particles, density 0.8
```

**Custom velocities:**
```
/molecular-mcp:particles 64 atoms at temperature 300K
```

## MCP Tools

**Random configuration:**
```
Call: mcp__molecular-mcp__create_particles
Parameters: {
  "num_particles": <number of particles>,
  "box_size": <simulation box size>,
  "temperature": <initial temperature>,
  "particle_type": "<argon|custom>"
}
```

**Lattice structure:**
```
Call: mcp__molecular-mcp__create_lattice
Parameters: {
  "lattice_type": "<fcc|bcc|sc>",
  "num_cells": <number of unit cells per dimension>,
  "density": <target density>,
  "temperature": <initial temperature>
}
```

## Particle Types

| Type | Sigma (A) | Epsilon (K) | Mass (amu) |
|------|-----------|-------------|------------|
| argon | 3.4 | 120 | 40 |
| custom | user-defined | user-defined | user-defined |
