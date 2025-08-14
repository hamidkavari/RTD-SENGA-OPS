\
        # Numerical model (high level)

        SENGA+ targets **compressible reacting flows**. At a high level the governing equations are the compressible Navier–Stokes system coupled to species transport and energy with **finite‑rate chemistry**. Time integration is explicit multi‑stage Runge–Kutta, and spatial derivatives use high‑order centered stencils with optional filtering.

        > **Note**
        > This page provides the *modeling context* to help users understand setups and stability constraints. Implementation details live in the SENGA sources.

        ## Unknowns and equations

        - Conservative form variables (per cell): $\rho, \, \rho\mathbf{u}, \, \rho E$.
        - Species mass fractions $Y_s$ (one per species), temperature $T$.
        - Source terms from reaction rates $\dot{\omega}_s(T, \{Y\})$.

        ## Discretisation (typical)

        - **Space:** high‑order centered differences (e.g. 10‑point/10th‑order for smooth problems) with optional dissipation/filtering near discontinuities.
        - **Time:** low‑storage explicit **RK3** (or similar) with CFL chosen from max acoustic speed.
        - **Parallelisation:** domain decomposition with halo exchanges each stage.

        ## Stability & accuracy tips

        - Start with a CFL of `0.2–0.4` for reacting cases; increase cautiously.
        - For strong shocks, enable numerical filtering or reduce order locally.
        - Use OPS diagnostics to verify halo depths and decomposition quality.
