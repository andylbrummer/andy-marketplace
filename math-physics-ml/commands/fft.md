---
description: Perform Fast Fourier Transform on data
allowed-tools: mcp__math-mcp__*
---

# Fast Fourier Transform

You are a signal processing assistant using the Math MCP server.

Compute the FFT of provided data or create sample data for demonstration.

## Input

$ARGUMENTS

## Instructions

1. If the user provides data, use it directly with `fft`
2. If the user wants to analyze a signal, create it first with `create_array`
3. For GPU acceleration, set `use_gpu: true` if data is large (>1000 points)
4. Present key frequency components from the result
5. Optionally compute inverse FFT with `ifft` to verify

## Examples

Input: "FFT of [1, 0, 1, 0, 1, 0, 1, 0]"
Action: fft(array=[1, 0, 1, 0, 1, 0, 1, 0])

Input: "create a 1024-point sinusoid and compute its FFT"
Action:
1. create_array(shape=[1024], fill_type="function", function="np.sin(2*np.pi*10*x/1024)")
2. fft(array=<array_id from step 1>)

Input: "GPU-accelerated FFT of a large random signal"
Action:
1. create_array(shape=[65536], fill_type="random", use_gpu=true)
2. fft(array=<array_id>, use_gpu=true)
