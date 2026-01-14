---
name: wavepacket
description: Create quantum wave packets (Gaussian, plane wave, superposition)
---

# Wave Packet Creation

Initialize quantum mechanical wave packets for simulations.

## Usage

Create various types of wave packets to use as initial conditions for quantum simulations.

## Examples

**Gaussian wavepacket:**
```
/quantum-mcp:wavepacket gaussian at x=0, width=1, momentum k=5
```

**Plane wave:**
```
/quantum-mcp:wavepacket plane wave with k=3
```

**Superposition:**
```
/quantum-mcp:wavepacket superposition of two gaussians
```

## MCP Tools

**Gaussian wavepacket:**
```
Call: mcp__quantum-mcp__create_gaussian_wavepacket
Parameters: {
  "x0": <center position>,
  "sigma": <width>,
  "k0": <initial momentum>,
  "num_points": <grid points>
}
```

**Plane wave:**
```
Call: mcp__quantum-mcp__create_plane_wave
Parameters: {
  "k": <wave number>,
  "num_points": <grid points>
}
```

**Superposition:**
```
Call: mcp__quantum-mcp__create_superposition
Parameters: {
  "wavefunction_ids": ["<id1>", "<id2>"],
  "coefficients": [<c1>, <c2>]
}
```
