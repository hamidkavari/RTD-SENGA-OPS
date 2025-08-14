# Tutorial 3 — Running & domain decomposition

## Why decompose?

On multi‑core/GPUs you’ll decompose the domain to distribute work and memory. OPS can auto‑choose, but you can override with environment variables:

```bash
# 8 × 4 × 4 decomposition (total 128 ranks)
export OPS_FORCE_DECOMP_X=8
export OPS_FORCE_DECOMP_Y=4
export OPS_FORCE_DECOMP_Z=4

mpirun -np 128 ./senga2_mpi -OPS_DIAGS=2 2>&1 | tee log_128.txt
```

**Reading diagnostics**

- Check halo depth vs. stencil — OPS will warn if too small.
- Load balance: aim for similar cell counts per rank.
- Communication/computation ratio: prefer compact subdomains.
