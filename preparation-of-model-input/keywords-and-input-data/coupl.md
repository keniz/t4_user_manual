# COUPL

**COUPL**           Introduces options and parameters for TOUGH4 and third-party software coupling simulation.

Record **COUPL.1**

&#x20;                   Free format for 2 string parameters, or Format(1A10,1A99).

&#x20;                   NameCouplingApp, run\_cmd

_NameCouplingApp_     The name of the third-party software.&#x20;

_run\_cmd_                        The path and name of the software executable.

if NameCouplingApp="FLAC3D", the additional input parameters and formats are identical to the "[FLAC](flac.md)" data block and the following inputs are neglected.&#x20;

Record **COUPL.2**

&#x20;                  Free format for 20 integer parameters, or Format(20I5).

&#x20;                  int\_coupling(i), i=1,20&#x20;

int\_coupling(i)     20 integer parameters as coupling option or parameters.

Record **COUPL.3**

&#x20;                  Free format for 20 real parameters, or Format(20E10).

&#x20;                  real\_coupling(i), i=1,20&#x20;

real\_coupling(i)     20 real parameters as coupling option or parameters.

&#x20;**Used in**: All EOS modules

**Example**:                &#x20;
