# Quickstart (run your first case)

Assuming you built `senga2_mpi` or a GPU variant, you can run test problems with `mpirun` or a scheduler like Slurm.

## CPU (MPI)

```bash
mpirun -np 4 ./senga2_mpi -OPS_DIAGS=2           OPS_FORCE_DECOMP_X=2 OPS_FORCE_DECOMP_Y=2 OPS_FORCE_DECOMP_Z=1           2>&1 | tee log_mpi.txt
```

## GPU (Slurm example)

```bash
srun -A <account> --nodes=1 --time=01:00:00              --partition=gpu --gres=gpu:1 --ntasks=1 --cpus-per-task=8              ./senga2_mpi_cuda -OPS_DIAGS=2              OPS_FORCE_DECOMP_X=1 OPS_FORCE_DECOMP_Y=1 OPS_FORCE_DECOMP_Z=1              2>&1 | tee log_gpu.txt
```

### Tips

- Start with small grids to test correctness; scale up gradually.
- Use `OPS_DIAGS` to confirm halo depths and partitioning.
- Compare integrated quantities (e.g. total mass) between backends.
