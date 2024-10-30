# Problem 4-Density, Viscosity, Solubility, and Enthalpy of Real Gas Mixtures (EOS7C/SAM7C1)

This problem is from the example problem sam7c1 in TOUGH3/EOS7C user manual.  It is a simple test problem designed to demonstrate the gas mixture property calculations of TOUGH4/EOS7 through comparison of computed properties with independent reference values and results from TOUGH3/EOS7C. The problem is a series of gridblocks arranged in 10 columns with three rows. No connection exists between any two elements and all the elements are independent. Various initial conditions are assigned to different elements. Details for the initial conditions can be found in the [TOUGH3/EOS7C user manual](https://tough.lbl.gov/assets/docs/TOUGH2-EOS7C\_Users\_Guide.pdf).

The input file from TOUGH3/EOS7C can be directly used with minor modification by inserting a data section with keyword "[MODDE](../../preparation-of-model-input/keywords-and-input-data/modde.md)".  This keyword requests input of a parameter named InitCType, which is given as "EOS7C" in this example. InitCType equals to "EOS7C" indicating that the input files for current simulation are originally prepared for TOUGH3/EOS7C simulation, and the TOUGH4 model will have the same model setup as in TOUGH3/EOS7C. The gas definition is not required with this input file and two default gas components (CH4 and CO2), one tracer, and brine will be included in the simulation.

Simulation results from TOUGH4/EOS7 matches TOUGH3/EOS7C results, which has been confirmed by comparison to reference values from literatures.&#x20;

**Input File**:  [sam7c1.zip](https://drive.google.com/file/d/1x3KrFgJW6v-hUU-dMdJJCbKgS\_vPKokT/view?usp=sharing)

**Output Files**:  [outputs\_sam7c1.zip](https://drive.google.com/file/d/1wzB-JtwaGS0mfu4TIWUD36WR-JAtPWvY/view?usp=sharing)
