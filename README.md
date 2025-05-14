# AE370Project2
# Advection-Diffusion Solver Using Crank-Nicolson Method

## Overview

This repository contains a numerical solver for the **one-dimensional advection-diffusion equation** using the **Crank–Nicolson finite difference method**.

The physical system being modeled is the transport and spreading of a pollutant through a wind-driven tunnel. The mathematical model accounts for both:
- **Advection**: the drift of the pollutant downstream due to a constant wind velocity,
- **Diffusion**: the spreading of the pollutant caused by molecular diffusion.

The governing partial differential equation (PDE) is:

$$
\frac{\partial u}{\partial t} + v \frac{\partial u}{\partial x} = D \frac{\partial^2 u}{\partial x^2}
$$

where:
- $u(x,t)$ is the pollutant concentration,
- $v$ is the constant advection velocity (wind speed),
- $D$ is the constant diffusion coefficient,
- $x$ is the position along the tunnel,
- $t$ is time.

The **initial condition** specifies that the pollutant concentration is zero throughout the tunnel:

$$
u(x, 0) = 0
$$

The **boundary conditions** are:
- At the entrance ($x=0$), the pollutant concentration is fixed at unity:

$$
u(0, t) = 1
$$

- At the exit ($x=L$), a zero-gradient (Neumann) boundary condition is imposed:

$$
\frac{\partial u}{\partial x}(L, t) = 0
$$

This setup models a scenario where a constant source of pollutant enters the tunnel and then is carried downstream with both drift and spread effects.

---

## Numerical Methodology

The Crank–Nicolson method, an implicit finite difference scheme, is used to solve the advection-diffusion equation numerically.  
This method is:
- **Second-order accurate** in both time and space,
- **Unconditionally stable** for linear problems,
- Particularly well-suited for stiff problems involving diffusion.

The main steps include:
- Discretization of the spatial domain using a uniform grid with $N_x$ points,
- Discretization of the temporal domain using $N_t$ time steps,
- Formation of a **tridiagonal system** at each time step,
- Efficient solution of the system using a **banded matrix solver** (`scipy.linalg.solve_banded`).

The numerical results are compared against the known **true analytical solution**:

$$
u(x,t) = \frac{1}{2} \left(1 - \text{erf}\left( \frac{x - vt}{2\sqrt{Dt}} \right)\right)
$$

where $\text{erf}$ denotes the error function.

---

## Features and Outputs

Upon running the notebook, the following analyses and visualizations are automatically generated:

### 1. Contour Plot
- A filled contour plot showing the evolution of pollutant concentration $u(x,t)$ over both space and time.
- Illustrates the combined effects of advection and diffusion on the pollutant plume.

### 2. Numerical vs. Analytical Solution Comparison
- Line plots at selected times comparing the numerical solution and the exact analytical solution.
- Verifies the accuracy of the Crank–Nicolson method by visual inspection.

### 3. Pollutant Front Location Tracking
- Tracks the spatial location where the concentration first reaches a threshold value (typically $u=0.5$).
- Provides insight into how the pollutant front propagates over time due to advection and diffusion.

### 4. Spatial Convergence Study
- Investigates how the numerical solution error behaves as the spatial grid spacing $\Delta x$ is refined.
- Plots both the **relative $L^2$ error** and **absolute $L^2$ error** versus $\Delta x$ on a log-log scale.
- Includes a reference slope line corresponding to $\mathcal{O}(\Delta x^2)$ to confirm second-order spatial accuracy.

### 5. Temporal Convergence Study
- Investigates how the numerical solution error behaves as the time step size $\Delta t$ is refined.
- Plots both the **relative $L^2$ error** and **absolute $L^2$ error** versus $\Delta t$ on a log-log scale.
- Includes a reference slope line corresponding to $\mathcal{O}(\Delta t^2)$ to confirm second-order temporal accuracy.
