# Introduction

**SENGA‑OPS** combines the SENGA+ solver family with the **OPS** DSL. The goal is to express physics kernels once and run them efficiently on multiple targets (MPI, OpenMP, CUDA, HIP) through code generation/transformation.

**Why OPS?**

- *Single source, many backends:* The same high‑level loops generate code for CPU (MPI/OpenMP/SIMD) and GPU (CUDA/HIP) targets.
- *Halo/partition management:* OPS manages multi‑block halos and decomposition so you focus on algorithms not plumbing.
- *Diagnostics & tuning:* Built‑in diagnostics, decomposition hints, and profiling help you get scalable performance.

**What this documentation covers**

- An overview of the **numerical model** used by SENGA+ (`theory.md`).
- How **OPS** abstractions map to SENGA kernels (`ops.md`).
- SENGA‑specific build and run notes (`senga.md`, `install.md`).
- Step‑by‑step **tutorials** for CPU/GPU builds, domain decomposition and post‑processing (`tutorials/`).
