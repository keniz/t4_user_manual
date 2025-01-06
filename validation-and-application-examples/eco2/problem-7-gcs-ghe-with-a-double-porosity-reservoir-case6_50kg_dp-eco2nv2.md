# Problem 7-GCS/GHE with a double-porosity reservoir (Case6\_50kg\_DP/ECO2NV2)

This example is originally present as problem No. 6 in TOUGH3/ECO2N V2 user manual.  It simulates  one injection-well/production-well pair (known as a doublet) of the five-spot pattern that makes up a geothermal heat extraction (GHE) system combined with geological carbon sequestration (GCS). The geothermal reservoir we consider here is an idealized 100 m thick, double porosity reservoir. In the double porosity model, one continuum represents the mobile (higher permeability) regions and the other represents the immobile (lower permeability) regions. The reservoir is assumed to be initially filled with pure CO2 in the mobile continuum and pure water in the immobile continuum, under the same hydraulic static pressure (29.15 MPa) and temperature (152.2 $$^oC$$). Because the mobile continuum makes up 20% of the reservoir, this initial condition is equivalent to an initial bulk gas saturation of 20%. Details of the model setup, parameters, initial conditions, and boundary conditions can be found  in the  [TOUGH3/ECO2N V2 user manual](https://tough.lbl.gov/assets/files/02/documentation/TOUGH2-ECO2N_V2.0_Users_Guide.pdf).

In ECO2 module, the partitioning of H2O and CO2 among co-existing aqueous and gas phases is calculated based on the correlations developed by Spycher and Pruess (2005) for the low temperature range (<99 $$^oC$$) and Spycher and Pruess (2010) for the high temperature range (109 to \~300 $$^oC$$). These correlations were derived from the requirement that chemical potentials of all components must be equal in different phases. TOUGH4 uses the same approach as TOUGH3/ECO2N V2 in handling the temperatures between 99 and 109 $$^oC$$, for which a cubic function is used to interpolate both the equilibrium mass fraction of CO2 in the aqueous phase and the equilibrium mass fraction of H2O in the gas (CO2 rich) phase. Numerical experiment indicates that bad convergence may be experienced for temperature at this transition zone. TOUGH4 provides a flexibility for user to define  lower and upper bound of the transition zone through [FE(54) and FE(55)](../../process-modeling/eco2.md). A narrow and reasonable transition zone may significantly improve the convergence performance. We use FE(54)=99.0 , FE(55)=99.5 (transition zone: 99.0\~99.5 $$^oC$$) for this example.&#x20;

&#x20;

Input files:                 [Case6\_50kg\_DP.zip](https://drive.google.com/file/d/13CwQZJTWI4u6fC05xMzoni4jTTAKzOst/view?usp=drive_link)

Output files:              [outputFiles.zip](https://drive.google.com/file/d/1aRLtKnNs7_gDEGJ_0mOJ0wsLO6gIS8kn/view?usp=sharing)