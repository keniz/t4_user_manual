# Problem 1-Demonstration of Initialization Options (ECO2N/rtab)

ECO2 provides different initialization options. It accepts  initial condition files from TOUGH3/ECO2N, ECO2M, and ECO2N V2.0. This example is originally included in the TOUGH2/ECO2N user manual. It performs a single infinitesimal time step (Δt = 10E-9 s) and includes neither flow connections between grid blocks nor sinks or sources. Therefore, there is no flow and no changes in the initially specified thermodynamic conditions. The purpose of this problem is simply to demonstrate different options for initializing thermodynamic conditions.

The definition of the model is through keyword "MODDE". Figure 10-1 shows the inputs in the data section of this keyword. The first line specifies the EOS module to be run in this simulation and the initial condition in TOUGH3/ ECO2N format (or indicating this input file was originally prepared for TOUGH3/ECO2). The third lines indicates that the simulation is in non-isothermal, does not  account diffusion, includes brine,  does not perform wellbore simulation., and runs the simulation in two phases (treats gas and supercritical CO2 as "supercritical" phase). &#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Figure 10-1 Input for model definition</p></figcaption></figure>

Model initialization with TOUGH3/ECO2N primary variables is made for a number of grid blocks in single-phase liquid conditions (_a   1_, _a    3_, _a    5_), single-phase gas (_a  10_), and two-phase fluid (_A  14_,    _A  15_, _A  19_). Several grid blocks are initialized with single-phase type primary variables, but with a CO2 mass fraction that is larger than can be dissolved in the aqueous phase, and smaller than required for single-phase gas conditions (_a   2_, _a   6_, _a   9_, _A  18_). The CO2 mass fractions for these blocks correspond to two-phase (liquid-gas) fluid conditions, and are internally converted to the appropriate gas saturation in the initialization phase. Many different initialization options are used in this example. Detailed discussion can be found in the TOUGH2/ECO2N user manual. TOUGH4 accepts all the TOUGH3/ECO2N initialization options through specifying _InitCType_="ECO2N" in keyword "MODDE" input.

The results from this example are identical to the results from simulation with TOUGH3/ECO2N. An alternative simulation of this example  is to run it in 3-phases. The simulation results remain the same except gridblock "a   2" which changes from supercritical-liquid to gas-liquid two phase condition.&#x20;

**Input Files:**                  [ rtab.zip](https://drive.google.com/file/d/1\_uo37CuAuys-vsXkPc-6m1G09ECyBqeE/view?usp=sharing)

**Output Files:**              [outputs\_rtab.zip](https://drive.google.com/file/d/1UyipBA8RFcqJvSNzHb8auoW7QfiiC\_ka/view?usp=sharing)   &#x20;
