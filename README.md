# AE370Project2
# Advection-Diffusion Solver Using Crank-Nicolson Method

## Overview

This repository contains a numerical solver for the **one-dimensional advection-diffusion equation** using the **Crank–Nicolson finite difference method**.

The physical problem models the **transport of a pollutant in a wind-driven tunnel**, accounting for both advection (drift) and diffusion (spreading) effects.

The governing equation is:

$$
\frac{\partial u}{\partial t} + v \frac{\partial u}{\partial x} = D \frac{\partial^2 u}{\partial x^2}
$$

where:
- $u(x,t)$: Pollutant concentration
- $v$: Constant advection speed (wind velocity)
- $D$: Constant diffusion coefficient
- $x$: Position along the tunnel
- $t$: Time

The **initial condition** is zero pollutant concentration everywhere:
$$
u(x, 0) = 0
$$

The **boundary conditions** are:
- At the tunnel entrance ($x=0$): fixed pollutant concentration $u(0,t) = 1$ (Dirichlet boundary condition)
- At the tunnel exit ($x=L$): zero spatial gradient $\frac{\partial u}{\partial x}(L,t) = 0$ (Neumann boundary condition)

---

## Numerical Method

The solution is obtained by:
- Discretizing the domain using a uniform spatial grid and a uniform time grid.
- Applying the **Crank–Nicolson scheme**, which is **second-order accurate** in both time and space.
- Solving the resulting **tridiagonal system** at each time step using an efficient banded matrix solver (`scipy.linalg.solve_banded`).

The code also compares the numerical solution to the **true analytical solution**:

$$
u(x,t) = \frac{1}{2} \left(1 - \operatorname{erf}\left( \frac{x - vt}{2\sqrt{Dt}} \right)\right)
$$

where $\operatorname{erf}$ is the error function.

---

## Features and Outputs

The code automatically produces the following plots:

- ✅ **Contour Plot**:  
  A contour plot of pollutant concentration $u(x,t)$ over the full space-time domain.

- ✅ **Numerical vs True Solution Comparison**:  
  Line plots comparing the numerical and exact solutions at several representative times during the simulation.

- ✅ **Pollutant Front Location**:  
  Tracks the position of the "front" (where $u=0.5$) as it moves through the tunnel.

- ✅ **Spatial Convergence Study**:  
  Examines how reducing $\Delta x$ (the grid spacing) affects the solution accuracy.  
  Relative and absolute $L^2$ errors vs. $\Delta x$ are plotted, with reference $\mathcal{O}(\Delta x^2)$ lines.

- ✅ **Temporal Convergence Study**:  
  Examines how reducing $\Delta t$ (the timestep size) affects the solution accuracy.  
  Relative and absolute $L^2$ errors vs. $\Delta t$ are plotted, with reference $\mathcal{O}(\Delta t^2)$ lines.

> **Note**:  
> Mass conservation plots, error profiles at final time, and effective convergence rate plots have been intentionally removed to keep the analysis focused.

---

## Repository Structure

```text
├── README.md          <- This file
├── main.ipynb         <- Full organized Jupyter Notebook (modular with Markdown explanations)
├── Figures/           <- (Optional) Folder to save generated figures if saving is desired
