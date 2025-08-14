# OPS in a nutshell

**OPS (Oxford Parallel library for Structured mesh solvers)** is an embedded DSL for multi‑block structured grids. You express computation as *parallel loops* over *datasets* on a *block*. OPS handles dependency analysis, halo exchanges, and generates target code for each backend.

## Core abstractions

- **Block:** a structured domain (3D by default in SENGA‑OPS).
- **Datasets (`ops_dat`):** arrays defined on a block (e.g. `rho`, `vel`, `temp`).
- **Stencil:** neighbour pattern used by a kernel (e.g. 10‑point in x).
- **Parallel loop:** `ops_par_loop(kernel, block, range, arg1, arg2, ...)`.

## Mini example (illustrative)

```c
// Pseudo‑C illustrating the idea
ops_block b = ops_decl_block(3, "domain");
ops_dat rho = ops_decl_dat(b, 3, size, "double", data_ptr, "rho");
ops_stencil S10 = ops_decl_stencil(3, 10, s_points, "S10");

ops_par_loop(update_rho, b, range,
  ops_arg_dat(rho, S10, OPS_READ),
  ops_arg_dat(rho, S10, OPS_WRITE));
```

## Backends and targets

- **CPU:** MPI (distributed), OpenMP (shared), vectorised.
- **GPU:** CUDA (NVIDIA), HIP (AMD). Fallback "F2C" backends exist when CUDA Fortran isn’t available.

## Practical notes

- Always build **OPS first** for your target backend and ensure `OPS_INSTALL_PATH` is exported or referenced by the SENGA build system.
- Use `OPS_DIAGS` and `OPS_FORCE_DECOMP_{X,Y,Z}` at runtime to control diagnostics and decomposition.
