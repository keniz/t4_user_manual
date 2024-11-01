# Problem 3 - Heat Pipe in Cylindrical Geometry (rhp)

This problem is from the  sample problem No. 2  in TOUGH3/EOS3 user manual.&#x20;

Heat pipes are systems in which an efficient heat transfer takes place by means of a liquid-vapor counterflow process, with vaporization and condensation occurring at the hot and cold ends, respectively. Heat pipe processes occur naturally on a large scale (kilometers) in two-phase geothermal reservoirs, and they may be induced artificially if heat-generating nuclear waste packages are emplaced above the water table in partially saturated geologic formations.

The present problem models such high-level nuclear waste emplacement in an approximate way. The input file  specifies a cylindrical heater of 0.3 m radius and 4.5 m height, that provides a constant output of 3 kW into a porous medium with uniform initial conditions of 18 ˚C temperature, 1 bar pressure, and 20 % gas saturation. The MESHMAKER module is used to generate a one-dimensional radial grid of 120 active elements extending to a radius of 10,000 m (practically infinite for the time scales of interest here), with an additional element of a very large volume representing constant boundary conditions. Properly speaking, the problem represents one unit of an infinite linear string of identical heaters; if a single heater were to be modeled, important end effects would occur at the top and bottom, and a two-dimensional R-Z grid would have to be used.&#x20;

Most of the formation parameters are identical to data used in previous modeling studies of high-level nuclear waste emplacement at Yucca Mountain (Pruess et al., 1990). As we do not include fracture effects in the present simulation, heat pipe effects would be very weak at the low rock matrix permeabilities (of order 1 microdarcy) encountered at Yucca Mountain. To get a more interesting behavior, we have arbitrarily increased absolute permeability by something like a factor 10,000, to 20 millidarcy, and for consistency have reduced capillary pressures by a factor  $$(10,000)^{0.5}$$ = 100 in comparison to typical Yucca Mountain data. To provide a benchmark for proper code installation, the output files are provided for download. Users can abstract the results from output files. The input file  includes data for vapor-air diffusion, which can be engaged by setting _**af\_diff**_  to "TRUE" in [MODDE](../../preparation-of-model-input/keywords-and-input-data/modde.md).3 data section.  Comparison to the results without diffusion shows that some air remains in the boiling region near the heater when diffusion is active. Vapor is removed from the hot region at somewhat larger rates, causing liquid saturations to be somewhat smaller. This makes the heat pipe less efficient, and leads to slightly higher temperatures.

The simulation results match very well with the corresponding results from TOUGH3, except the heater element (first element). This is because the  MESHMAKER in TOUGH4 generates slightly different mesh for the first several elements compared to the MESH of TOUGH3.   In TOUGH4 MESH, the distance from heater element to the connection interface with the second element is 0.3 m (d1), but it is 0.15m in TOUGH3.  This can be proven by directly using the MESH from TOUGH3 model for TOUGH4 simulation. We believe TOUGH4 has the correct d1 value.

**Input Files:**      [INFILE\_rhp.zip](https://drive.google.com/file/d/1KyF8BpjR7PuyT2yqVA81FqCvaTquHZn5/view?usp=sharing)

**Output Files:**  [output\_rhp.zip](https://drive.google.com/file/d/19-2GNXWOvANUr7rnvHfxp7OjEInFcJ3d/view?usp=sharing)