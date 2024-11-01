# Problem 1 -Five-spot Geothermal Production/Injection (rfp)

This is an alternative simulation for  for [EOS1/problem3](../eos1/problem-3-five-spot-geothermal-production-injection-rfp.md), and here is run with the EOS2 module. The model setup and parameters are identical to  [EOS1/problem3](../eos1/problem-3-five-spot-geothermal-production-injection-rfp.md). The only difference is initial condition of the reservoir. The reservoir is in two-phase condition with a gas saturation=0.01. The gas phase contains steam in EOS1 simulation, but  the gas phase contains the mixture of steam and CO2 in EOS2 simulation. A CO2 partial pressure of 5 bars is specified for this problem.&#x20;

The flow system is modeled as a fractured medium with embedded impermeable matrix blocks in the shape of cubes. The matrix blocks were assigned a non-vanishing porosity of 10-10, so that they will contain a small amount of water. This has no noticeable impact on fluid and heat flows, and is done to prevent the water mass balance equation from degenerating into the singular form 0 = 0.&#x20;





Running the problem with  = 0 in the matrix blocks (domain MATRX) is also possible, but this results in more sluggish convergence and considerably smaller time steps. The MESHMaker module is used to perform MINC-partitioning of the primary grid (partition type THRED with three equal fracture spacings). The first MINC continuum, corresponding to the fracture domain, occupies a volume fraction of 0.02 and has an intrinsic porosity of 50 %, for an effective fracture porosity of 1 %. By inserting an ENDCY record in front of the MESHM data block, the MINC process can be disabled and the problem can be run as an effective porous medium. A CO2 partial pressure of 5 bars is specified. To select variables to print out, data block OUTPU is used as shown in Figure 4. Figure 5 shows part of the printout of the flow simulation run.

