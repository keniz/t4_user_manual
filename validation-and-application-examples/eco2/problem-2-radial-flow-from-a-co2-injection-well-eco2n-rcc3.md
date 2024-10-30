# Problem 2-Radial Flow from a CO2 Injection Well (ECO2N/rcc3)

This example is from TOUGH2/CO2N problem rcc3. It is basic problem of CO2 injection into a saline aquifer, examining two-phase flow with CO2 displacing (saline) water under conditions that may be encountered in brine aquifers at a depth of the order of 1.2 km. A CO2 injection well fully penetrates a homogeneous, isotropic, infinite-acting aquifer of 100 m thickness (Figure 10-2), at conditions of 120 bar pressure, 45 °C temperature, and a salinity of 15 % by weight. CO2 is injected uniformly at a constant rate of 100 kg/s. Full specifications can be found in TOUGH2/CO2N user manual.

<figure><img src="../../.gitbook/assets/image (70).png" alt="" width="375"><figcaption><p>Figure 10-2 Schematic of sample problem 2</p></figcaption></figure>

The simulation uses a two-dimensional radical mesh. The well is modeled as a circular grid element of R = 0.3 m. The numerical grid is extended to a large distance of 100 km, so that the system would be infinite-acting for the time period simulated (10,000 days, 27.38 years). Input file from TOUGH3 simulation with minor modifications can be directly used in current simulation.  Modification to the input file includes: (1) inserting the "MODDE" data section , (2) change of well type in "GENER" data section from "COM3" to "COM2" or "CO2".  CO2 is component number 2 in TOUGH4, but it is COM3 in TOUGH3.&#x20;

TOUGH4 can reproduce the simulation results by TOUGH3/ECO2N well. Discussion of the results can be found in  TOUGH2/CO2N user manual.&#x20;

A separate ROCKS domain 'well ' with "infinite" rock grain density was included in the input file to enable running of a non-isothermal variation simply by turning on it (through data record MODDE3.1); the well block "A1 1" is assigned to domain 'well ' with "infinite" rock grain density, so that CO2 injection would effectively occur at initial temperature of 45 °C, obviating the need for specifying an injection enthalpy. Similarly,  including/excluding the salt component in the simulation also be easily turn on/off through data record MODDE3.3.

This example was also included in TOUGH3/ECO2M and TOUGH3/ECO2NV2. As the CO2 remains in supercritical condition and the temperature remains less than 100.0 °C in whole injection procedure, the simulation results should be same with different EOS module. TOUGH4 can run the "ECO2M" type simulation by turning off two-phase simulation (default is for three-phase simulation) through through data record MODDE3.5. &#x20;



Input Files:          [rcc3.zip](https://drive.google.com/file/d/1tSB\_5rbpeTipgcYVM825VLAgALgzPLQW/view?usp=sharing)

Output Files:      [outputs\_rcc3.zip](https://drive.google.com/file/d/1TfyQCDJUaVc5K\_aJKwGfehu8Y7zyzNCN/view?usp=sharing)      &#x20;
