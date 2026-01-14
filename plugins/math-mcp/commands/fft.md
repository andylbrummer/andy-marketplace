---
name: fft
description: Compute Fast Fourier Transform with optional GPU acceleration
---

# Fast Fourier Transform

Perform FFT and inverse FFT operations with optional GPU acceleration via CuPy.

## Usage

Provide data or an array ID to transform. Results can be used for spectral analysis, filtering, and signal processing.

## Examples

**Compute FFT:**
```
/math-mcp:fft [1, 2, 3, 4, 5, 6, 7, 8]
```

**Inverse FFT:**
```
/math-mcp:fft --inverse <array_id>
```

## MCP Tools

**Forward FFT:**
```
Call: mcp__math-mcp__fft
Parameters: {
  "array_id": "<array identifier>"
}
```

**Inverse FFT:**
```
Call: mcp__math-mcp__ifft
Parameters: {
  "array_id": "<array identifier>"
}
```

## Notes

- Automatically uses GPU if CuPy is available
- Supports 1D, 2D, and N-dimensional transforms
- Results stored in session for further processing
