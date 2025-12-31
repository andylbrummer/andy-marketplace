# Math MCP Assistant

Use this skill when the user asks about symbolic mathematics, numerical computing, or needs to perform calculations involving:
- Solving algebraic equations symbolically
- Computing derivatives or integrals
- Matrix operations and linear algebra
- Fast Fourier transforms (FFT)
- Function optimization and root finding
- GPU-accelerated numerical operations

## Available Tools

The Math MCP server provides these tools:

### Symbolic Mathematics (via SymPy)
- `symbolic_solve` - Solve equations symbolically (supports systems of equations)
- `symbolic_diff` - Compute symbolic derivatives (any order)
- `symbolic_integrate` - Compute definite or indefinite integrals
- `symbolic_simplify` - Simplify expressions (auto, trigsimp, expand, factor)

### Numerical Computing (GPU-accelerated)
- `create_array` - Create arrays (zeros, ones, random, linspace, function-based)
- `matrix_multiply` - GPU-accelerated matrix multiplication
- `solve_linear_system` - Solve Ax = b systems

### Transforms
- `fft` - Fast Fourier Transform (GPU-accelerated)
- `ifft` - Inverse FFT

### Optimization
- `optimize_function` - Minimize functions (BFGS, Nelder-Mead, Powell)
- `find_roots` - Find roots of equations

## Usage Examples

### Solve a quadratic equation
```
Use symbolic_solve with equations="x**2 - 4"
```

### Compute a derivative
```
Use symbolic_diff with expression="sin(x)*exp(x)", variable="x"
```

### GPU-accelerated FFT
```
1. Use create_array with shape=[1024], fill_type="random", use_gpu=true
2. Use fft with the returned array_id, use_gpu=true
```

### Minimize a function
```
Use optimize_function with function="x**2 + y**2", variables=["x", "y"], initial_guess=[1, 1]
```

## GPU Acceleration

Set `use_gpu: true` on supported tools for CUDA acceleration. Falls back gracefully to CPU if CUDA unavailable.

## Resources

The server exposes:
- `constants://math/pi` - Mathematical constant pi
- `constants://math/e` - Euler's number e
- `constants://math/golden_ratio` - Golden ratio phi
- `array://{id}` - Cached arrays from computations
- `expr://{id}` - Cached symbolic expressions
