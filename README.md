> **⚠️ Warning / Disclaimer:** This repository contains a student project/assignment prepared as part of the Numerical Methods in Electromagnetics course. The mathematical models, analytical derivations, and code implementations may contain errors or limitations. Please keep in mind that this is an individual academic project when using the code or mathematical equations as a reference.

# 2D Laplace Equation Solver for a Rectangular Pipe

## About the Project

This project involves the numerical and analytical analysis of the two-dimensional Laplace equation \((\nabla^2 \phi(x,y) = 0)\) to calculate the potential distribution inside an infinitely long rectangular pipe. The problem is solved analytically using the Separation of Variables method, resulting in an infinite series solution, which is then numerically approximated using a finite number of terms (\(N\)).

## Contents

- **Mathematical Derivation:** Solution of the boundary-value problem using Fourier coefficients.
- **Potential Distribution (Heatmap):** Two-dimensional visualization of the potential distribution inside the pipe under the specified boundary conditions.
- **Error Analysis:** Investigation of the relationship between the number of terms included in the series (\(N\)) and the computational error using a logarithmic scale.

## Boundary Conditions

The system is solved using the following boundary conditions:

- \(\phi(0,y) = 0\)
- \(\phi(1,y) = 0\)
- \(\phi(x,0) = 0\)
- \(\phi(x,1) = 1\)

