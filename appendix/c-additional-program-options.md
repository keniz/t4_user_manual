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

**IE(23)**              Selects enthalpy calculation method (for EOS7 and EWASG module only)

0:                      water vapor and other gases are treated as real gas, and enthalpy of the mixture is calculated using the RealGas module.

1:                       Enthalpy of water vapor will be calculated using the equations of IFC-1967, or IAPWS-IF97,  and enthalpy of the mixture of other gases will be calculated using RealGas module. The enthalpy of their mixture is mass fraction weighted sum of the two enthalpies (enthalpy for water vapor and for all other gases). &#x20;

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

**IE(30)**             Inputs the frequency (in minutes) for scanning the file "[Update\_Simulation\_Parameters](../preparation-of-model-input/adjustment-of-computing-parameters-at-run-time.md)" to see if this file has been updated during run time. The default frequency is 10, which means the code will check the file every 10 minutes.

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

**IE(52)**               Use the maximum change of primary variables as Newton iteration  convergence criteria. Default is on (default is off for wellbore simulation).&#x20;

0:  Turn on (see [**PARAM.3**](../preparation-of-model-input/keywords-and-input-data/param.md) for detail&#x73;**).**&#x20;

1:    Turn off.          &#x20;

**IE(53)**              When in 3-phase ECO2 module simulation, CO2 near the critical point is allowed: &#x20;

0:    co-existing of liquid and gas phase CO2.

1:   either in liquid or in gas phase, not bot&#x68;**.**        &#x20;

**IE(54)**              In calculation of energy balance: &#x20;

0:   potential energy is not include&#x64;**.**

1:    potential energy is included. The Z coordinates for each element in the MESH file must be elevation for using this option.

**IE(55)**              In GENER input, the production or injection rate can be in a volume rate (see ITAB input with record [ GENER.1](../preparation-of-model-input/keywords-and-input-data/gener.md)). If a volume rate is used, user must specified the phase condition of produced /injected fluid at the standard temperature and pressure condition (STP, it can be different in different industry, see **IE(56)** for more information), or at the reservoir condition. If the phase condition can be figured out through well "TYPE", the input of IE(55) will be ignored.&#x20;

0, 1:   Gas phase (default)**.**

2:      Aqueous phase.

3:      Oil/Liquid CO2 phase.  &#x20;

**IE(56)**              TOUGH4 allows using different temperature and pressure condition or reservoir condition for input of the produced/injected fluid volume: &#x20;

0:  The American Petroleum Institute STP: 288.7 K and 101,325 Pa  (default).

1:   International Union of Pure and Applied Chemistry (IUPAC) STP: 273.15 K and 100,000 Pa.   &#x20;

2:  ISO 13443 STP: 288.15 K and 101,325 Pa

3:  User defined STP, the standard temperature and pressure must be inputted through FE(70) and FE(71) respectively.&#x20;

4: At reservoir condition, volume in RB (for production only).

5: At reservoir condition,  volume in m<sup>3</sup> (for production only).

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

**IE(62)**               For a well-formation connection, if IE(62)>0, d1 or d2 at the wellbore side will be set to be 0.0. This option could be sensitive  for the heat exchange between wellbore and formation (for wellbore simulation only).

**IE(63)**               At two-phase flow condition in a EOS7 or EWASG simulation, the first gas component can be forced to be 0.0 mass fraction (no existence). This may help to improve the convergence performance, if first gas indeed not exist in the flow system (for EOS7 and EWASG module only).

0:  off.&#x20;

1:   on.&#x20;

**IE(64)**              For preventing oscillatory phase transitions.  A larger IE(64) value represents that, once the system transitions to a different phase, it becomes more difficult to revert to the original phase condition.   It can be in the range 1-10.   Default IE(64)=2.  &#x20;

**IE(65)**              Adding small artificial friction at near zero velocity condition to gain numerical stable condition.&#x20;

0:  on.&#x20;

1:   off.&#x20;

**IE(66)**              Two versions of function are implemented in TOUGH4 for calculating the heat loss through wellbore using analytical solution. The function is sensitive to the convergence for some non-isothermal simulations. User may select different version to achieve best performance. &#x20;

0: Using (Ramey, 1962), including short time solution.

1:  Using (Ramey, 1962), not including short time solution.

**IE(67)**              Two versions of function are implemented in TOUGh4 for calculating the acceleration loss in a well. This function is sensitive to the convergence for some simulations.  User may select different version to achieve best performance. &#x20;

0:  Newer version.&#x20;

1:   Older version.&#x20;

**IE(68)**              Naming rules for time-series output files for observation elements or connections by FOFT, COFT and GOFT. &#x20;

0:  The element name or connection will be part of the output file name (default).

1:   The numbering of the observation element or connection will be part of the output file name.

**IE(69)**              In many simulations, model has an initial condition of  pressure distribution with gravity equilibrium and  temperature distribution with given temperature gradients. For such a case, the pressure and temperature at any elements can be estimated from the pressure and temperature at  reference level together with the z coordinate (elevation), fluid density and geothermal  temperature gradients. User can perform the initial pressure and temperature calculation through a Python function at run-time (see _iniCondition_ in TOUGH\_python\_module.py). Other primary variables can also be assigned  values in the Python function. This option can be used to set up initial INCON file (run the simulation for one  time step with tiny time-step size).&#x20;

0: no Python function for initial condition calculation is called.&#x20;

1:  turn on the Python interface to the function for initial condition calculation.&#x20;

**IE(70)**             Selection of volume translated method for improving the accuracy of liquid (oil) density predictions made by cubic equations of state (EoS). &#x20;

0: The Peneloux volume correction (Peneloux, et al., 1982, default).

1:  The Peneloux volume correction (Peneloux, et al., 1982).

2:  Method proposed by Lin and Duan (2005)

3: No correction.

**IE(79)**             Simulation results can be sent to the Python interface. User can access these data through a python function. Three default parameters to be sent are saturations for all phases (parameter1), mass fraction of all components for all phases (parameter3), and pressure for all phases(parameter3). See Python function "_UserDefinedELOutput_" (TOUGH\_python\_module.py) for details. &#x20;

0: Off, no simulation results be sent to Python interface

1: On, turn on the Python interface for the output data.&#x20;

**IE(80)**             User may send different parameter other than the default one  (see **IE(79)**) to Python interface . the first parameter (Parameter1) is:  &#x20;

0: default parameter,  saturations for all phases.

2-8:  2-viscosity for all phases ; 3-density for all phases; 4- enthalpy for all phases; 5-capillary pressures; 6-temperature; 7-mass fraction of all components in all phases; 8-pressure for all phase.&#x20;

**IE(81)**             User may send different parameter other than the default one  (see **IE(79)**) to Python interface . the second parameter (Parameter2) is:  &#x20;

0: default parameter,  mass fraction of all components in all phases.

1-6, 8:  1- saturation for all phases; 2-viscosity for all phases ; 3-density for all phases; 4- enthalpy for all phases; 5-capillary pressures; 6-temperature; 8-pressure for all phase.&#x20;

**IE(82)**             User may send different parameter other than the default one  (see **IE(79)**) to Python interface . the third parameter (Parameter3) is:  &#x20;

0: default parameter,  pressure for all phases.

1-7:  1- saturation for all phases; 2-viscosity for all phases ; 3-density for all phases; 4- enthalpy for all phases; 5-capillary pressures; 6-temperature; 7-mass fraction of all components in all phases.&#x20;

**IE(83)**             Management of options for smart time-stepping.

0: not effect.

1: Turn on all time-stepping options  (i.e. let IE(84)-IE(88)=1).&#x20;

**IE(84)**           If maximum residual increases in three consecutive iterations, cut time-step size.&#x20;

0: Off.

1: On           &#x20;

**IE(85)**           If maximum residual no change in three consecutive iterations, cut time-step size.&#x20;

0: Off.

1: On     &#x20;

**IE(86)**           If residuals large than 1000.0, or  large than FE(86), if FE(86) is not 0, in three consecutive iterations, cut time-step size.&#x20;

0: Off.

1: On     &#x20;

**IE(87)**           If residuals swing in four consecutive iterations, cut time-step size.&#x20;

0: Off.

1: On     &#x20;

**IE(88)**           If maximum residual is large than a given criteria (AMRES, [ **PARAM.3**](../preparation-of-model-input/keywords-and-input-data/param.md)), cut time-step size.&#x20;

0: Off.

1: On     &#x20;

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

**IE(401)**           Selects gas/hydrocarbon viscosity calculation method (for EOS7, EWASG, and ECOF only).

0:  Chung et al. 1988)

1:   Quinones et al. (2001; 2000)

**IE(402)**           Selects air solubility calculation method

0:  solubility is a function of temperature

1:   solubility is independent of temperature (compatible with TOUGH3/EOS7 and TMVOC)

**IE(403)**           Output unit selection for module TMVOC and ECOF

0:  units for output are: density--mole/m<sup>3</sup>; enthalpy--J/mole; component fraction--mole fraction; flux--mole/s (default).

1:   units for output are: density--kg/m<sup>3</sup>; enthalpy--J/kg; component fraction--mass fraction; flux--kg/s.

(For **FE(50)**-**FE(55)**, see [ECO2 process modeling](../process-modeling/eco2.md) for details)

**FE(50)**             lower bound of pressure range (in Pa) for CO2 thermophysical properties. &#x20;

**FE(51)**              upper bound of pressure range (in Pa) for CO2 thermophysical properties.

**FE(52)**             lower bound of temperature range (in $$^oC$$) for CO2 thermophysical properties. &#x20;

**FE(53)**             upper bound of temperature range (in $$^oC$$) for CO2 thermophysical properties.

**FE(54)**             lower bound of the transition zone  temperature range (in $$^oC$$). &#x20;

**FE(55)**             upper bound of the transition zone  temperature range (in $$^oC$$).

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

**FE(86)**            User defined maximum residual criteria used with option of IE(86) for cutting time-step size, see IE(86). &#x20;

**FE(100)**          When Jacobian matrix has zero diagonal term, we need to add tiny digit ( $$\epsilon$$) to it to avoid numerical error in inversion of diagonal submatrix. $$\epsilon$$ may have magic effect on solving the linear equations for some problems.   The default $$\epsilon =10.0^{-200}$$.  The $$\epsilon$$ will be assigned a value $$10.0^{FE(100)}$$, if FE(100)<=-50 and FE(100)>=-300.
