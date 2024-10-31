# Problem 2 - Production from a Geothermal Reservoir with Hypersaline Brine and CO2 (rhbc)

This problem is from the  sample problem No. 2  in TOUGH3/EWASG user manual.&#x20;

The problem examines production from a hypothetical geothermal reservoir with high salinity and CO2. A single well produces at a constant rate of 65 kg/s from an infinite-acting reservoir in 1-D radial flow geometry. The reservoir is in two-phase conditions initially, with uniform initial conditions of P = 60 bar, T = 275.55 ˚C; other problem parameters are given in Table 10-3. The[ options choices](../../process-modeling/ewasg.md) made with SELEC-data are: no vapor pressure lowering (IE(24) = 0), a tubes-in-series model for permeability reduction from precipitation (IE(11) = 3), full dependence of thermophysical properties on salinity (IE(14) = 0), and Michaelides correlation for brine enthalpy (IE(15) = 1), and CO2 as non-condensible gas (IE(16) = 2, the IE(16) option is effect only when using TOUGH3/EWASG input file for current simulation. Otherwise, keyword [GASES](../../preparation-of-model-input/keywords-and-input-data/gases.md) must be used for gas definition). The permeability-porosity relationship for the parameters are used here with the options of IE(11) = 3 and  FE(1) = FE(2) = 0.8.

&#x20;_**Table 10-3 Model parameters for the simulation**_

| Reservoir thickness                                                                                                                            | 500 m                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Permeability                                                                                                                                   | $$50  \times10^{-15} m^2$$     |
| Porosity                                                                                                                                       | 0.05                           |
| <p>Relative permeability</p><p>       Corey curves with    <em>Slr</em> =</p><p>                                            <em>Sgr</em> =</p> | <p> </p><p>0.30</p><p>0.05</p> |
| Rock grain density                                                                                                                             | 2600 kg/ $$m^3$$               |
| Specific heat                                                                                                                                  | 1000 J/kg ˚C                   |
| Thermal conductivity                                                                                                                           | 2.1 W/m ˚C                     |
| Initial conditions                                                                                                                             |                                |
| Temperature                                                                                                                                    | 275.55 ˚C                      |
| Gas saturation                                                                                                                                 | 0.45                           |
| Pressure                                                                                                                                       | 60.0 bar                       |
| NaCl mass fraction in liquid phase                                                                                                             | 0.30                           |
| CO2 partial pressure                                                                                                                           | 14.79 bar                      |
| Wellblock radius                                                                                                                               | 5 m                            |
| Production rate                                                                                                                                | 65 kg/s                        |

Fluid withdrawal causes pressures to drop near the production well. Boiling of reservoir fluid gives rise to dilution of CO2 in the gas phase and to increased concentrations of dissolved NaCl, which begins to precipitate when the aqueous solubility limit is reached. As the boiling front recedes from the well, solid precipitate fills approximately 10 % of the original void space, causing permeability to decline to approximately 28 % of its original value.&#x20;

Difference to the TOUGH3/EWASG, TOUGH4/EWASG uses  a cubic equation of state (Peng-Robinson, Redlich- Kwong, or Soave-Redlich-Kwong equations of state) to calculate gas mixture density, enthalpy departure, and viscosity. Solubility of gases is calculated using chemical equilibrium approach (TOUGH3/EWASG uses Henry's law). Due to the differences in modeling approaches between TOUGH3/EWASG and TOUGH4/EWASG, some variation in simulation results is expected, though not necessarily significant. Figure 10-12 shows the comparison of simulation results of

