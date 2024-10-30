# Inputs for Initial Conditions&#x20;

Input of initial conditions are through keywords “INCON”, “INDOM” or “PARAM” at record PARAM.4. Users can also provide initial conditions through the file “INCON”. TOUGH4 may allow different parameters as the initial conditions. No matter which set of parameters are used as the initial conditions, they must be consistent for the inputs with different keywords or the input file. Default initial conditions are always the primary variables.&#x20;

User may specify initial condition input formatting  through defining initCType in input data record MODDE.1 or command line _–i \<parameter>._ Each module may have its specific value for initCType. Several initCType values are shared by all the EOS modules:&#x20;

&#x20;initCType =

&#x20;                 “1LINE”              initial condition input for each element is in 1 line.

&#x20;                 “2LINES”           initial condition input for each element is in 2 lines.

&#x20;                 “3LINES”           initial condition input for each element is in 3 lines.

&#x20;                 “4LINES”           initial condition input for each element is in 4 lines.

&#x20;                 “FM_n_L_abcd_...”  initial condition input through a special transformation. &#x20;

In  “FM_n_L_abcd_...”, where "FM" is the indicator of the special transformation input; _n_L specifies the lines to be read for each element, can be 1L, 2L, 3L, or 4L; _abcd....._ represents primary variable 1,2,3 ,4 are located in the INCON file data number a, b, c, d, ......, for each element respectively. For example:

A INCON has following format:

_**A00001**_

_**Pg, Sg/Xg1,  Xg2, Xg3, Xbr, xtr1, xtr2, Temperature**_

In current simulation,  brine and tracer 2 are excluded from the model.   The input of initial condition for element A00001 must be:

_**A00001**_

_**Pg,  Sg/Xg1, Xg2, Xg3, xtr1, Temperature**_

If the INCON file is used for current simulation,  initCType must have a value "FM1L123468".

If current simulation will include a new gas (gas 4)  and its mass fractions are all initialized as 0.0 (primary variables: _**Pg, Sg/Xg1,  Xg2,  Xg3,  Xg4,  xtr1, Temperature)**_ , the initCType must have a value "FM1234068"&#x20;

The initial conditions of different EOS modules are summarized below. The maximum number of tracers or salts is 5. The following discussion covers a smaller number of tracers or salts, but it applies to any number of them.
