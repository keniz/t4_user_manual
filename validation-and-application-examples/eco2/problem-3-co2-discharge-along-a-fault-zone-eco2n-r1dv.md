# Problem 3-CO2 Discharge Along a Fault Zone (ECO2N/r1dv)

This example is from TOUGH2/ECO2N user manual, the third problem r1dv.&#x20;

When CO2 disposed of into brine formations, CO2 injection plumes would over time extend to large distances of the order of ten kilometers or more, making it likely that geologic discontinuities such as faults and fractures will be encountered, with an associated potential for CO2 losses from the primary disposal aquifer. CO2 leaks through caprock discontinuities have a potential for self-enhancement, because pressures can actually decrease and/or flow rates increase as escaping CO2 creates a pathway towards shallower strata. It is not known whether or not it may be possible for a runaway process to develop where an initially “small” leak could accelerate and grow over time to the point of an eruptive release. Migration of CO2 along a water-saturated fault zone would be subject to gravitational and viscous instabilities, and would likely involve complex two- and three-dimensional flow effects. As a approximation to this kind of problem, we consider here a highly simplified situation in which a potential CO2 leakage path is modeled as a 1-D column (Figure 10-3).&#x20;

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption><p>Figure 10-3. Schematic of the fault zone model (a) and applied boundary conditions (b).</p></figcaption></figure>

This example will investigate the immiscible displacement of water by CO2 subject to pressure, gravity, and capillary pressure effects, change of fluid density, viscosity, and CO2 solubility with pressure, and formation dry-out.&#x20;

For this simple 1-D problem, the 500 m vertical extent of the fault zone is evenly divided into 100 grid blocks of 5 _m_ height. Additional blocks _top 0_ and _bot 0_ are used to represent boundary conditions. For the 1 m length of the 25 _m_ wide fault zone modeled, interface areas are 25 $$m^2$$.&#x20;

The problem is run in two segments. A first run segment obtains gravity equilibrium relative to a pressure of 100 bar prescribed at the top boundary. The gravity-equilibrated conditions are then used as initial conditions in a second run segment, where conditions of P = 240 bar and a mass fraction XCO2 = 1 are maintained at the lower boundary, while upper boundary conditions are unchanged. Note that the CO2 discharge conditions correspond to a large overpressure, exceeding initial hydrostatic pressure by approximately 60 %. It is unlikely that overpressures this large would be used in practical CO2 storage systems. Capillary pressure parameters were chosen so that maximum Pcap is $$10^7$$ Pa, and Pcap vanishes for small gas saturations of Sg ≤ 0.001. These and other simulation parameters can be seen in the following input files. All runs are performed for pure water (no salinity) in isothermal mode at T = 45 °C. Different to the TOUGH3/ECO2 simulation, TOUGH4 does not require including brine component in the model and solves one less equation for each gridblock. &#x20;

Current simulation results match corresponding results from TOUGH3/ECO2 simulation well. Discussion of the results can be found in TOUGH2/ECO2N user manual.

Input Files:        [InputFiles\_gravityEQ.zip](https://drive.google.com/file/d/1BPDEeRkSlLv31QhSm2wGGZBhHixBdvT\_/view?usp=sharing),  [InputFiles.zip](https://drive.google.com/file/d/1hp0xSVbwoH4k4l1ojhbhWTK8nDsPtRoR/view?usp=sharing)

Output Files:    [OutputFiles\_gravityEQ.zip](https://drive.google.com/file/d/1jiuOvgTWmGAitlFSXy4Om\_J4o10Y5CFC/view?usp=sharing), [OutputFiles.zip](https://drive.google.com/file/d/1GNoeJAXbbszug7RPKAEH34PHoBs7WFBS/view?usp=sharing)&#x20;
