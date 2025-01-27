# ☑️ C: ADDITIONAL PROGRAM OPTIONS

TOUGH4 provides more additional options through arrays IE and FE. The flexible input for IE and FE makes the use of these options very easy. Their inputs are through keyword [SELEC](../preparation-of-model-input/keywords-and-input-data/selec.md).  Some IE and FE elements with lower subscripts have been used for module specific inputs, which may have different purposes for different EOS modules. For details, users may refer to the specific input requirements for each EOS module in the "[Process Modeling](../process-modeling/)" section. The default values for both IE and FE are 0. Followings are the list of additional options:

**IE(17)**               allows choice of different mass balance output&#x20;

0:                      Output mass balance for the whole system only.

-1:                     Output mass balance for all rocks and the whole system.

n (n>0):           Output mass balance for rock _n_ and the whole system.

**IE(18)**               controls the impact of solid on permeability (effect for ECO2 and EWASG only).

0:                      no impact.

1:                       the impact is on, see [EWASG process modeling](../process-modeling/ewasg.md) for details.

**IE(19)**               Accounts water vapor for real gas property (effect for EOS7 and EWASG only).

0:                      True.

1:                       False.

**IE(20)**             allows choice of different random number generator

0:                      use FORTRAN pseudorandom number RANDOM\_NUMBER.

1:                       use TOUGH2 internal random number generator.

**IE(21)**             Multiplies the linear equation of each element by inverse of its diagonal matrix (the diagonal term will be all 1.0 after multiplication) . This may avoid error in solving linear equations.&#x20;

0:                     True.  &#x20;

1:                       False.

**IE(22)**              Selects ECO2 simulation phase conditions (equivalent to the input of [MODDE 3.4](../preparation-of-model-input/keywords-and-input-data/modde.md)) .

0:                      in 3 phases&#x20;

1:                       in 2 phases (treat both gas and supercritical CO2 as “gas”).  &#x20;

**IE(23)**              &#x20;

**IE(24)**             allows to turn vapor pressure lowering on/off. It can be overridden by specific inputs of EOS4 and EWASG module for VPL on/off option.&#x20;

0: VPL is off.&#x20;

1: VPL is on.

**IE(25)**             The input for tracer distribution coefficient (_XKD1)_ and fraction of organic carbon (_FOCM_) through [_ROCKS.1.1_](../preparation-of-model-input/keywords-and-input-data/rocks.md) is conflict for TMVOC. For maintaining the compatibility of input file from TOUGH3/TMVOC and other TOUGH4 modules, IE(25) is used to coordinate the inputs. The input is through lot 6-10 of ROCKS.1.1. (for TMVOC only)

0:                    lot 6 is for FOCM input, lot7-lot10 for XKD1-XKD4 input.

1:                     lot 6-10 is for XKD1-XKD5 input, no FOCM input.&#x20;

**IE(26)**             Checks whether wellbore flow turns direction (wellbore simulation only).&#x20;

0: off.&#x20;

1: on.

**IE(27)**             Selects calculation method for thermal conductance along wellbore (for wellbore simulation only)&#x20;

0: no special treatment, in the same way as in porous media.

1: ignore the conductive heat flow.

2: consider conduction in well wall only.

3: Fully consider conduction in fluids and well wall.&#x20;

**IE(28)**             Accounts for mist flow (wellbore simulation only).&#x20;

0: on.&#x20;

1: off.

**IE(29)**             Applies calculated geothermal gradient to (wellbore simulation only):&#x20;

0: wellbore grid elements only.&#x20;

1: all model grid elements.

**IE(30)**             Inputs the frequency for scanning the file "[Update\_Simulation\_Parameters](../preparation-of-model-input/adjustment-of-computing-parameters-at-run-time.md)" to see if this file has been updated during run time. The default frequency is 1000, which means the code will check the file every 1000 time steps.

**IE(31)**             Selects the effects of water on the thermophysical properties of the CO2-rich phase (for ECO2 only).&#x20;

0: ignore the impact of water on the density and viscosity of the CO2-rich phase.&#x20;

1: fully consider impact of water on the CO2-rich phase thermophysical properties.

-1: ignore the impact of water on density, viscosity and enthalpy of CO2-rich phase (IE(31)=-1 is compatible with ECO2N v1.0).&#x20;

**IE(32)**             Selects decay mass for mass balance calculation.&#x20;

0: decay mass calculated from current time step parameters.

1:  use average of decay mass calculated from previous and current time steps.&#x20;

**IE(33)**             Performs supercritical water simulation

0: on.&#x20;

1: off, supercritical water is neglected and treated as high temperature vapor.

**IE(34)**             Adjusts calculated CO2 enthalpy using the analytical solution by Altunin et al. (1975) to match the value from NIST Chemistry Web Book

0: no adjustment (compatible with ECO2N V1.0).&#x20;

1: do the adjustment to match NIST reference state (If you use enthalpy data from NIST Chemistry Web Book as input for source/sinks, IE(34) must be 1.

**IE(35)**             Write SAVE file in different format

0: write SAVE file in free format (TOUGH4 format)

1:  write SAVE file in TOUGH3 format.

**IE(37)**         Selection of a GPU for solving linear equations when multiple GPUs are available, default selection is number 0.

**IE(38)** When running a MPI parallel simulation, if AMGCL linear solver is used, user has the option to select parallelization scheme for solving linear equations

0: using OPENMP

1: using MPI

**IE(50)**              Number of the pressure points (allow 50-1000) in the table of CO2 thermophysical properties. (See [ECO2 process modeling](../process-modeling/eco2.md) for details)

**IE(51)**               number of the temperature points (allow 50-1000) in the table of CO2 thermophysical properties.

**IE(52)**               Use the maximum change of primary variables as Newton iteration  convergence criteria.

0:  Turn on (see [**PARAM.3**](../preparation-of-model-input/keywords-and-input-data/param.md) for detail&#x73;**).**

1:    Turn off          &#x20;

**IE(53)**              When in 3-phase ECO2 module simulation, CO2 near the critical point is allowed: &#x20;

0:    co-existing of liquid and gas phase CO2.

1:   either in liquid or in gas phase, not bot&#x68;**.**        &#x20;

**IE(54)**              In calculation of energy balance: &#x20;

0:   potential energy is not include&#x64;**.**

1:    potential energy is included. The Z coordinates for each element in the MESH file must be elevation for using this option.

**IE(55)**              In GENER input, the production or injection rate can be in a volume rate (see ITAB input with record [ GENER.1](../preparation-of-model-input/keywords-and-input-data/gener.md)). If a volume rate is used, user must specified the phase condition of produced /injected fluid at the standard temperature and pressure condition (STP, it can be different in different industry, see **IE(56)** for more information)

0, 1:   Gas phase (default)**.**

2:      Aqueous phase.

3:      Oil/Liquid CO2 phase.  &#x20;

**IE(56)**              TOUGH4 allows using different standard temperature and pressure condition: &#x20;

0:  The American Petroleum Institute STP: 288.7 K and 101,325 Pa  (default).

1:   International Union of Pure and Applied Chemistry (IUPAC) STP: 273.15 K and 100,000 Pa.   &#x20;

2:  ISO 13443 STP: 288.15 K and 101,325 Pa

3:  User defined STP, the standard temperature and pressure must be inputted through FE(70) and FE(71) respectively.&#x20;

**IE(57)**              In real gas property module (used by EOS7 and EWASG),  calculated CO2 density may have big error when CO2 is in liquid phase, along the saturation line or near the critical point.  As an alternative, user may use the CO2 property module for the CO2 density calculation (other thermophysical parameters are remain calculated using the real gas property module):

0:  Use real gas property module.

1:   Analytical solution by Altunin (1975) implemented in CO2 property module.   &#x20;

2:  Read from file 'CO2TAB'.&#x20;

**IE(58)**              In previous version TOUGH codes,  the time-stepping or log information and simulation output results are written into a single file. In TOUGH4, they are stored separatory in two files.  TOUGH4 remains the option to have log information and simulation results stored in a single file:

0:  Log information and simulation results are written in two separated files. &#x20;

1:   Log information and simulation results are written into a single file (same as TOUGH2 or TOUGH3) .   &#x20;

**IE(59)**              The output of primary variable changes (DX) at a time step could be interested to some users.  DX can be printed to the output file through this option. User may specify the contents for output file through keyword "[OUTPU](../preparation-of-model-input/keywords-and-input-data/outpu.md)".  If "PRIMARY" is specified for output, either primary variables or  changes of them will be printed, controlled by IE(59):

0:  Primary variables. &#x20;

1:   Changes of  the primary variables.

**IE(61)**              When conduct MPI parallel computing simulations.  The model domain (mesh) must be partitioned. Different partition methods can be used:

0:  METIS, multilevel k-way. &#x20;

1:   METIS, multilevel recursive-bisection.

2:  A simple direct method. The portioning is based on the sequence of the elements in the mesh.&#x20;

3:  Read from data file "_part.dat"._ The first line of data file contains three numbers: the partition subdomain number (must be equal to the MPI tasks for current simulation), edge cut number (not be used), and the total number of mesh elements (NumElem) in Format(3I10).  Following NumElem lines contain the partition number for each element in the Format(10I8).

**IE(101)-IE(126)**       If are non-zero values, they are equivalent to [MOP2(1)-MOP2(26)](../preparation-of-model-input/keywords-and-input-data/momop.md).

**IE(111)**            Selects thermodynamic formulation.

0:  IFC-67; for subcritical conditions only&#x20;

1:   IAPWS-IF97&#x20;

2:  IAPWS-IF97 for T<800°C, IAPWS-95 for T≥800°C

**IE(130)**            Control output of flux time-series using[ ROFT](../preparation-of-model-input/keywords-and-input-data/roft.md).

0:  output phase/component fluxes as discussed in [ROFT](../preparation-of-model-input/keywords-and-input-data/roft.md).

1:   output diffusive flux for different phases/components.

**IE(131)**            Control output of flux time-series using[ ](../preparation-of-model-input/keywords-and-input-data/roft.md)[COFT](../preparation-of-model-input/keywords-and-input-data/coft.md).

0:  output phase/component fluxes as discussed in [COFT](../preparation-of-model-input/keywords-and-input-data/coft.md).

1:   output diffusive flux for different phases/components.

**IE(402)**           Selects air solubility calculation method

0:  solubility is a function of temperature

1:   solubility is independent of temperature (compatible with TOUGH3/EOS7 and TMVOC)

**FE(56)**             The density of injected fluid at standard temperature and pressure (STP)  which is needed when the fluid injection rate is in volume   ( $$kg/m^3$$).

**FE(57)-FE(69)**    The densities of the model components 1-12 at standard temperature and pressure (STP), respectively. These densities are used for calculation of the produced mixture fluid density which only needed when the fluid production is in volume rate (see ITAB input with record [ GENER.1](../preparation-of-model-input/keywords-and-input-data/gener.md)). The density of the produced mixture fluid at STP condition using the known component mass fractions and densities of each component is calculated as follows:

$$\rho _{mix}=1/(x1/ \rho_1+x2/ \rho_2+x3/ \rho_3......)$$

where:

$$\rho_{mix}$$is the density of the mixture at STP.

$$x_i$$ is the mass fraction of component (_i)_.

$$\rho_i$$ is the density of component (_i_) at STP.

FE(57) is for first model component (water or water vapor) density at STP. TOUGH4 provides default values for them and also for most gas components. In most case, the input of **FE(57)-FE(69)** is needed only when the produced fluid is in aqueous or oil/Liquid CO2 phase (see **IE(55)** for the phase specification, **IE(56)** for STP definition).&#x20;

**FE(70)**             User specified  standard temperature (in _K_) It is required only when **IE(56)**=3.

**FE(71)**             User specified  standard pressure (in _Pa_) It is required only when **IE(56)**=3.

**FE(72)**            The highest pressure allowed in a TOUGH simulation is 1.0e8 Pa. A higher pressure may still work for some EOS modules. If user want to rise the high-pressure limitation, FE(72) can be used for setting the new high-pressure limitation. It must be in the range 1.0e8-1.0e9.&#x20;

**FE(100)**          When Jacobian matrix has zero diagonal term, we need to add tiny digit ( $$\epsilon$$) to it to avoid numerical error in inversion of diagonal submatrix. $$\epsilon$$ may have magic effect on solving the linear equations for some problems.   The default $$\epsilon =10.0^{-200}$$.  The $$\epsilon$$ will be assigned a value $$10.0^{FE(100)}$$, if FE(100)<=-50 and FE(100)>=-300.
