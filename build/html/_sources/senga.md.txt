# SENGA‑specific notes

This project integrates **SENGA+** kernels with **OPS** backends. The repository layout is roughly:

```
SENGA-OPS/
├─ SENGA/        # SENGA+ sources and build logic
├─ OPS/          # OPS sources (as a submodule/vendor)
└─ README.md
```

### Build order

1. Build **OPS** for your target (CPU/GPU) – produces libs/headers.
2. Build **SENGA** with the corresponding target, pointing to `OPS_INSTALL_PATH`.

### Backends

- **CPU (MPI/OpenMP)** – portable and a good starting point.
- **CUDA / HIP** – for NVIDIA / AMD GPUs respectively.
- **F2C bridges** – use C wrappers where CUDA Fortran is unavailable, e.g. `f2c_mpi_cuda`, `f2c_mpi_hip`.

### Runtime knobs

- `OPS_DIAGS=2` – print decomposition and performance diagnostics.
- `OPS_FORCE_DECOMP_{X,Y,Z}` – force a 3D partitioning, e.g. `8×4×4`.
