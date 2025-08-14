# Tutorial 2 — GPU build (CUDA or HIP)

> You must build on an actual GPU node.

1. **Get interactive node (Slurm example)**
   ```bash
   srun -A <account> --nodes=1 --time=01:00:00 --partition=gpu --gres=gpu:1 --pty /bin/bash
   ```
2. **Source OPS setup and build**
   ```bash
   cd SENGA-OPS/OPS
   source source_files/<cuda_or_hip_setup>.sh
   cd ops/fortran
   make mpi_cuda     # or: f2c_mpi_cuda / f2c_mpi_hip
   ```
3. **Build SENGA for the same backend**
   ```bash
   cd ../../../SENGA
   export OPS_INSTALL_PATH=$(pwd)/../OPS/ops/fortran
   make -f Makefile.codegen senga2_mpi_cuda   # or f2c_mpi_hip
   ```
4. **Run one‑GPU test**
   ```bash
   ./senga2_mpi_cuda -OPS_DIAGS=2 OPS_FORCE_DECOMP_X=1 OPS_FORCE_DECOMP_Y=1 OPS_FORCE_DECOMP_Z=1
   ```
