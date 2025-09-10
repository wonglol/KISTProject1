# KISTProject1

It performs a **3D FDTD** simulation in MEEP that launches the **fiber LP01 eigenmode** into the chip facet and measures the **per‑facet coupling efficiency** into the **six‑waveguide (2 layers × 3)** array’s **fundamental supermode** using **eigenmode decomposition**.

**Main methodology (step‑by‑step)**

**1. Build a 3D geometry**

-Background is SiO₂ (oxide).

-A **fiber core cylinder** (n≈1.449, radius≈4.3 µm) runs along **x** to provide a uniform section where the LP01 eigenmode is well defined.

-On the chip side (x≥0), you create **six SiN blocks** (n≈2.0): three at **z=+t_mid/2** and three at **z=−t_mid/2**, with widths w_center (middle) and w_outer (outer) at y = 0, ±pitch. This is the **2‑layer × 3 array**.

**2. Inject the correct physical mode**

-You use an **EigenModeSource** placed inside the uniform fiber region to inject the **LP01** of the fiber, not a plane wave.

-This matters because coupling depends on **mode shape** (overlap), not just on power.

**3. Absorb outgoing radiation**

-**PML** boundaries on all sides absorb fields that leave the device to avoid non‑physical reflections.

**4. Measure input and output power in modes (not raw flux)**

-At the input plane (in the fiber) you compute the forward eigenmode amplitude a_in => P_in = a_in^2

-At the array plane (just inside the six-WG region) you compute the foward amplitude of the **array's fundamental supermode** => P_out = a_out^2

**5. Report the coupling efficiency**


Each time step updates multiple field arrays over all cells, so you’re doing billions of floating‑point operations per second.
