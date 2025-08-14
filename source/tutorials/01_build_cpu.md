# Tutorial 1 — CPU build

1. **Clone with submodules**
   ```bash
   git clone --recurse-submodules https://github.com/senga-ops/SENGA-OPS.git
   ```
2. **Build OPS (MPI backend)**
   ```bash
   cd SENGA-OPS/OPS/ops/fortran
   make mpi
   ```
3. **Build SENGA (MPI)**
   ```bash
   cd ../../../SENGA
   export OPS_INSTALL_PATH=$(pwd)/../OPS/ops/fortran
   make -f Makefile.codegen senga2_mpi
   ```
4. **Smoke test**
   ```bash
   mpirun -np 2 ./senga2_mpi -OPS_DIAGS=2
   ```
