# Phase diagram of Dziyaloshinskii-Moriya model with exchange interaction 

The program discretize three functionals, each of it relative to a phisical phase of a 2-D material that has
Exchange and Dziyaloshinskii-Moriya interaction. After the discretization, each phase is minimized with respect
to thermodynamics parameters (Temperature (T), external magnetic field (H) and uniaxial anisotropy (A)). The value
of free energy after the minimization process is storage in a file, and the next round of minimization utilizes the
later results as the initial condition. 

The minimization process was made using the external library 'alglib', more precisely with the method of minimization
with non-linear constrains. 

The entropy file consists of an interpolation of a set of points that relates entropy, mean magnetization 'm' and a 
variational parameter 'h'. Origanally, the entropy is a funcition of 'h' and 'm', and these parameters are related 
by the langevin function m = 1/h - coth(h). Since the langevin function is not analitically invertible, and we want
the entropy as a funciton only of magnetization, we proceed to concatenated values of 'm' with values of entropy, 
that is, choosing a value of h, we can find a value of m, and a value of entropy, relating the last two, and creating
a function entropy S of m.

The program works as it follows:
Each phase known in the model has it's own file that describes the functional and all the process of the minimization
of it. The entropy function is apart, since all functionals use it. the main.cpp file will run the process of minimization
of each one of the functionals in a loop, varing some thermodynamical parameter to create an interprolated funciton of 
free energy for each of the phases.

The easiest way to run the program is to put all the functionals and entropy .cpp and .hpp files in the same folder, and run in the 
terminal:
g++ main.cpp -lm -O3 alglib/*.cpp functionals_folder/*.cpp
