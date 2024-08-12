# cuBLAS

- NVIDIA CUDA Basic Linear Algebra Subprograms is a GPU-accelerated library for accelerating AI and HPC (high performance compute) applications. It includes several API extensions for providing drop-in industry standard BLAS APIs and GEMM (general matrix multiplication) APIs with support for fusions that are highly optimized for NVIDIA GPUs.
<br>
- Pay attention to your shaping (https://stackoverflow.com/questions/56043539/cublassgemm-row-major-multiplication)

## cuBLAS-Lt
- **cuBLASLt (cuda BLAS Lightweight)** is an extension of the cuBLAS library that provides a more flexible API, primarily aimed at improving performance for specific workloads like deep learning models. Close to all the datatypes and API calls are tied back to matmul

- In cases where a problem cannot be run by a single kernel, cuBLASLt will attempt to decompose the problem into multiple sub-problems and solve it by running the kernel on each sub-problem.

- this is where fp16/fp8/int8 kicks in

## cuBLAS-Xt
- cublas-xt for host + gpu solving (way slower)
- since we have to transfer between motherboard DRAM and GPU VRAM, we get memory bandwidth bottlenecks and can't compute as fast as doing everything on-chip
- **cuBLASXt** is an extension to cuBLAS that enables multi-GPU support. Key features include:

**Multiple GPUs:** Ability to run BLAS operations across multiple GPUs, allowing for GPU scaling and potentially significant performance improvements on large datasets.

**Thread Safety:** Designed to be thread-safe, enabling concurrent execution of multiple BLAS operations on different GPUs.

Ideal for large-scale computations that can benefit from distributing workloads across multiple GPUs.

Choose XT for large-scale linear algebra that exceeds GPU memory

- cuBLAS vs cuBLAS-Xt
    - `(M, N) @ (N, K)` where M = N = K = 16384
    - ![](../assets/cublas-vs-cublasxt.png)

## cuBLASDx

Highlight that we **ARE NOT** using this in the course

The cuBLASDx library (preview) is a device side API extension for performing BLAS calculations inside CUDA kernels. By fusing numerical operations you can decrease latency and further improve performance of your applications.

- You can access cuBLASDx documentation [here](https://docs.nvidia.com/cuda/cublasdx).
- cuBLASDx is not a part of the CUDA Toolkit. You can download cuBLASDx separately from [here](https://developer.nvidia.com/cublasdx-downloads).