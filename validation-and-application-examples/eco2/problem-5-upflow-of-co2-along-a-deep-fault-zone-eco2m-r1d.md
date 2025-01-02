# Problem 5-Upflow of CO2 along a Deep Fault Zone (ECO2M/r1d)

This example simulates leakage of CO2 from a deep storage reservoir along a vertical fault zone of 5 m thickness. The fault is assumed to intersect the CO2 reservoir at a depth of Z = -1500 m. Fault zone permeability is assumed as $$k=100 \times 10^{-15} m^2$$, porosity φ = 0.15, with wall rocks assumed completely impermeable.&#x20;

Setup and solution of the problem involves several steps, (1) MESH generation followed by some hand-editing, (2) generation of a geothermal-hydrostatic profile as initial conditions for the CO2 leakage scenario, and (3) upflow of CO2 along the fault zone. This example is originally present in [TOUGH3/ECO2M user manual](https://tough.lbl.gov/assets/docs/TOUGH2-ECO2M_Users_Guide.pdf). A detailed description of the these steps can be found in the manual and do not repeat here. The scenario considered here does not model the CO2 storage reservoir as such; instead, we assume that a CO2 plume from a nearby storage reservoir reaches the bottom of a fault zone at some pressure in excess of hydrostatic. The model mesh is generated to represent a vertical fault with 1  width, 5m thickness and 1500m length. The boundary  conditions include maintaining atmospheric condition at the top of the fault and imposing a constant pressure at the bottom boundary. Initial conditions in the fault correspond to hydrostatic equilibrium in a typical geothermal gradient.&#x20;

The simulation of CO2 upflow is initialized using the SAVE file with the geothermal hydrostatic conditions obtained from the simulation for geothermal-hydrostatic profile, with only one essential change: the conditions at the bottom boundary are changed from single-phase water at P = 147.476 bar to single-phase liquid CO2 at a 10 bar overpressure, P = 157.476 bar. TOUGH4 allows using the SAVE file from TOUGH3 simulation directly, even though the primary variables are slightly different. &#x20;

TOUGH4 may require slight changes to the main input file of TOUGH3 for remaining the same simulation computing parameters by:

(1) insert MODDE data section for specifying the EOS module to be run and the initial condition SAVE file being from TOUGH3/ECO2M simulation.&#x20;

(2) set IE(16)=1 for using exactly the same mutual solubility model as implemented in ECO2M.

(3) set IE(31)=-1 for ignoring the impact of water on density, viscosity and enthalpy of CO2-rich phase (same as ECO2M).

In general, simulation results for TOUGH4 match results from TOUGH3 well. Slight differences at the phase transition zone may be due to using of different numerical methods.  Discussion of simulation results can be found in [TOUGH3/ECO2M user manual](https://tough.lbl.gov/assets/docs/TOUGH2-ECO2M_Users_Guide.pdf).



Input files:                [r1d.zip](https://drive.google.com/file/d/1BgBhK6LjWgXol8YspEM9B0TkXr7ATXHX/view?usp=sharing)

Output files:            [outputFiles.zip](https://drive.google.com/file/d/10qrF5qOBjvymNQ4m3krtZdQKeO9ZE7XZ/view?usp=sharing)
