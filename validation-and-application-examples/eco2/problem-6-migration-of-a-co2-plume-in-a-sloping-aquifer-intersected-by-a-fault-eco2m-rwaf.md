# Problem 6-Migration of a CO2 Plume in a Sloping Aquifer, Intersected by a Fault (ECO2M/rwaf)

The purpose of this problem is to illustrate application of ECO2 module  to a scenario that includes the primary CO2 storage reservoir, as well as a leakage pathway that extends all the way to the land surface. The problem explores the large-scale long-time migration of a CO2 plume in a sloping aquifer that is intersected by a leaky fault. Aquifer parameters are patterned after the Carrizo-Wilcox aquifer at the Texas Gulf coast (Nicot, 2008; Hesse et al., 2008). We assume that a substantial number of CO2 storage projects will be operating in the Wilcox, and we consider a 2-D vertical section along the dip of the aquifer. The aquifer is modeled as a rectangular domain of 200 m thickness and 110 km length, sandwiched between impermeable cap and base rocks, and tilted with an angle of  $$\alpha =1.5^o$$ against the horizontal (Fig. 10-n). We consider the upper right hand corner of the domain to be at the land surface; the lower left hand corner is then at a depth of 110,000 sin(α) + 200 cos(α), which for a tilt angle of   $$\alpha =1.5^o$$  corresponds to 3,079.4 m. Formation properties include a uniform and isotropic permeability of 500 mD, a porosity of 15 %, and a compressibility of $$4.5 \times10^{-10}Pa^{-1}$$ (similar to compressibility of water at ambient conditions).&#x20;

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Figure 10-n Geometric dimensions of the 2-D rectangular domain modeled. The domain is dipping upward by an angle α. The initial CO2 plume is shown by light shading.</p></figcaption></figure>

Discussion of preparation of the computational grid for such a scenario, the development of appropriate initial conditions and boundary conditions, setting up the model, running the simulation and understanding simulation results  can be found in TOUGH3/ECO2M user manual (example problem no. 4) . We will not repeat here. TOUGH4 simulation can directly use the input files from TOUGH3 simulation, except including of the MODDE data section in the main input file:

_MODDE----1--------2--------3--------4--------5--------6--------7----\*----8_&#x20;

_ECO2, ECO2M,                      // module name for the simulation, initial condition-using ECO2M input,_&#x20;

_5                                               //length of gridblock name_&#x20;

_true, false, **false**, false           // nonisothermal, accounting\_for\_diffusion, including brine,_&#x20;

In TOUGH3 simulation, the brine component must be included in the simulation even though there is no brine in the system. TOUGH4 allows to exclude the brine component in the simulation and one equation less to be solved. Tests show saving about 23% running time for the simulation, if the brine component is excluded.  To exclude brine in the simulation, user needs to set the third variable in the third data record of the MODDE data section to "false". &#x20;

In general, simulation results with TOUGH4 match results from TOUGH3 well. Slight differences at the phase transition zone may be due to using of different numerical methods.  Discussion of simulation results can be found in [TOUGH3/ECO2M user manual](https://tough.lbl.gov/assets/docs/TOUGH2-ECO2M_Users_Guide.pdf).



Input files:                  [rwaf.zip](https://drive.google.com/file/d/1QKCSg7SF24rvGyLkz0QaYcnXWZC04tsu/view?usp=sharing)

Output files:               [outputFiles\_noBrine.zip](https://drive.google.com/file/d/16hKBBrxA_Gq1kV8J6Wvj8lEE-QNypq08/view?usp=sharing)     [outputFiles\_withbrine.zip](https://drive.google.com/file/d/1RHVAeKGkRJNFsZVD_7k_QnfWnRyp_Dcb/view?usp=sharing)
