# Phase Diagram of Dzyaloshinskii-Moriya Model with Exchange Interaction

This program discretizes three functionals, each corresponding to a physical phase of a 2D material with **Exchange** and **Dzyaloshinskii-Moriya (DM) interactions**. After discretization, each phase is minimized with respect to thermodynamic parameters: **Temperature (T)**, **external magnetic field (H)**, and **uniaxial anisotropy (A)**. The value of the free energy after the minimization process is stored in a file, and the next round of minimization uses these results as the initial condition.

The minimization is performed using the external library **alglib**, specifically with the method for minimization under **non-linear constraints**.

## Entropy File

The entropy file consists of an interpolation of a set of points that relate **entropy**, **mean magnetization (`m`)**, and a **variational parameter (`h`)**. Originally, the entropy is a function of `h` and `m`, and these parameters are related by the Langevin function:

$$m = \frac{1}{h} - \mathrm{coth}(h)$$

Since the Langevin function is not analytically invertible and we want the entropy as a function only of magnetization, we proceed by concatenating values of `m` with corresponding entropy values. That is, for a chosen value of `h`, we obtain a value of `m` and the corresponding entropy, creating a function **S(m)** that expresses entropy solely as a function of magnetization.

## Program Structure

Each phase in the model has its own file describing its functional and the entire minimization process. The entropy function is separate, as it is used by all functionals. The `main.cpp` file runs the minimization process for each functional in a loop, varying certain thermodynamic parameters to create an **interpolated function of free energy** for each phase.

## Running the Program

The easiest way to run the program is to place all **functional** and **entropy `.cpp` and `.hpp` files** in the same folder, and compile with:

```bash
g++ main.cpp -lm -O3 alglib/*.cpp functionals_folder/*.cpp
```

This will compile the program and prepare it to execute the minimization and generate the phase diagram data.
