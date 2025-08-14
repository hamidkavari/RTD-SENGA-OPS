# Theory — numerical model overview

SENGA+ targets **compressible reacting flows**. At a high level the governing equations are the compressible Navier–Stokes system coupled to species transport and energy with **finite-rate chemistry**. Time integration is explicit multi-stage Runge–Kutta, and spatial derivatives use high-order centered stencils with optional filtering.

> **Note**  
> This page provides the *modeling context* to help users understand setups and stability constraints. Implementation details live in the SENGA sources.

## Unknowns and equations

- Conservative variables (per cell): $\rho, \rho\mathbf{u}, \rho E$  
- Species mass fractions $Y_s$, temperature $T$  
- Source terms from reaction rates $\dot{\omega}_s(T,\{Y\})$

## Discretisation (typical)

- **Space:** high-order centered differences (e.g. 10-point/10th-order) with optional filtering  
- **Time:** low-storage explicit **RK3** (or similar), CFL from max acoustic speed  
- **Parallelisation:** domain decomposition + halo exchanges each stage

## Stability & accuracy tips

- Start with CFL `0.2–0.4` for reacting cases; increase cautiously  
- For strong shocks, enable filtering or reduce order locally  
- Use OPS diagnostics to verify halo depths and decomposition quality
