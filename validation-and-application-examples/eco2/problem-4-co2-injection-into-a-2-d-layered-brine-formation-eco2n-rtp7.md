# Problem 4-CO2 Injection into a 2-D Layered Brine Formation (ECO2N/rtp7)

This example is from TOUGH2/ECO2N user manual,  test problem 4-rtp7. &#x20;

The model is patterned after the CO2 injection project at the Sleipner Vest field in the Norwegian sector of the North Sea, and is intended to investigate the dominant physical processes associated with the injection of supercritical CO2 into a layered medium. Significant simplifications have been made, the most important of which is the assumption of isothermal conditions (37 °C, the ambient temperature of the formation). CO2 injection rates (1,000,000 tonnes per year), system geometry, and system permeabilities correspond approximately to those at Sleipner, although no attempt was made to represent details of the permeability structure within the host formation. Injection of the supercritical CO2, which is less dense than the saline formation waters into which it is injected, causes it to rise through the formation. Its rate of ascent, however, is limited by the presence of four relatively low permeability shales. The top and bottom of the formation is assumed to be impermeable. The only reactive chemistry considered in this problem is the dissolution of CO2 in the aqueous phase.

The modeling system is idealized as a two dimensional symmetric domain perpendicular to the horizontal injection well which has a screen length of 100 meters (Figure 10-5). A one meter thick section perpendicular to the horizontal well is considered. The thickness of the formation at the injection site is 184 meters. The injection point is 940 meters below the sea floor, while the ocean depth at the site is 80 meters. The formation is assumed to consist of four lower permeability shale units 3 meters thick which are distributed within the high permeability sand. Each shale unit is separated by 30 meters. The well is 30 meters below the lowest shale unit, while the bottom of the aquifer is another 22 meters below the well.

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption><p>Figure 10-5 Schematic representation of geometry for CO2 injection in Utsira Formation.</p></figcaption></figure>

Boundary conditions: No heat or mass flux is allowed across any of the boundaries except the vertical boundary 6,000 meters from the injection well. This boundary is fixed at hydrostatic pressure, thus allowing flow into and out of the domain so as to avoid overpressuring the formation. The 6,000 meter boundary is chosen, however, to be far enough from the injection well that the CO2 does not reach this boundary after 2 years of injection.

Initial conditions: (a) T = 37 °C (isothermal throughout),  (b) P = hydrostatic (approximately 110 bars at injection point, approximately 90 bars at top of formation), (c) CO2 in the aqueous phase in equilibrium with a PCO2 of 0.5 bars, a typical value for sedimentary formation waters at the temperature we are considering.

CO2 injections: 0.1585 kg/s in half space.

The grid should be designed in such a way as to obtain “adequate” spatial resolution in regions where significant gradients occur, i.e., near the injection well, and near the shale layers. The TOUGH internal mesh maker can be used to generate the model mesh.  Mesh generation,  gravity equilibration and preparation for the other model inputs were discussed in TOUGH2/ECO2N user manual and do not repeat here. We directly use the initial conditions and boundary conditions obtained from TOUGH3 simulation which was done in accordance with the above list conditions and a salinity of 3.2 wt.-% NaCl.

The main input file from the TOUGH3 simulation require minor modification for using in TOUGH4 simulation. The "MODDE" data section must be inserted (Figure 10-6).  The record MODDE1.2 have a value "ECO2N" indicating the input files (INFILE and INCON) prepared for TOUGH3/ECO2N simulation are used for current simulation. The data record MODDE3 specifies that the simulation is in isothermal mode,  does not account diffusion, includes brine, does not consider wellbore simulation, and treats both gas and supercritical CO2  as  "supercritical" phase.  In addition,  the source/sink type must change to "COM3" from "COM2" in the GENER data section. &#x20;

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption><p>Figure 10-6 Inputs for  "MODDE" data section </p></figcaption></figure>



