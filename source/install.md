# Installation & build

## Prerequisites

- **GNU Make** and a recent C/C++ & Fortran toolchain
- **MPI** (`mpicc`, `mpif90`)
- **HDF5** development libraries
- **CUDA** (for NVIDIA GPUs) or **ROCm/HIP** (for AMD GPUs)

## 1) Get the sources

```bash
git clone --recurse-submodules https://github.com/senga-ops/SENGA-OPS.git
cd SENGA-OPS
```

## 2) Build OPS for your target

```bash
# Example (sketch): build Fortran OPS libraries for your backend
echo "source the appropriate setup file (compiler/paths/backends)"
source OPS/source_files/<your_setup>.sh

# If using the Python translator tools, activate the venv
cd OPS/ops_translator && source setup_venv.sh && cd -

# Build Fortran side of OPS
cd OPS/ops/fortran
make <target>   # e.g. mpi, mpi_cuda, f2c_mpi_cuda, f2c_mpi_hip
```

Once built, you should see libraries under `OPS/ops/fortran/lib/`.

## 3) Build SENGA

```bash
cd SENGA-OPS/SENGA
# If the Makefile needs it, export the install path
export OPS_INSTALL_PATH=$(pwd)/../OPS/ops/fortran
make -f Makefile.codegen senga2_<target>
```

> If a build fails, re‑run with `VERBOSE=1` and verify compilers, HDF5, and `OPS_INSTALL_PATH`.
