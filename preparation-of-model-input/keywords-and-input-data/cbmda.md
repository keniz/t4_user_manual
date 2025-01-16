# CBMDA

**CBMDA**       This keyword provides inputs for evoking simulation of gas/tracer absorption (such as coalbed methane or shale gas) using the  extended Langmuir isotherm. The extended Langmuir isotherm is only applied to specified materials, or rock types. The average in-situ moisture content, wwe, and average in-situ ash content, _wa_, are input as are the Langmuir parameters _pL_ and _GsL_ for each component.  The absorbed gas density is also input to model rock (coal) swelling and shrinkage.

Record **CBMDA.1**

&#x20;                       Free format for 5 parameters, or Format(A5,2E10.4, 2I5)&#x20;

&#x20;                       rockName, wa, wwe, islcbm, CompNum

_rockName_     Name of the rock that absorbed gas for this input, must be one of the rock defined in the "[ROCKS](rocks.md)" data section.

&#x20;_wa_          ash weight fraction.

_wwe_                equilibrium moisture weight fraction

&#x20;_islcbm_            flag for gas saturation dependent extended Langmuir isotherm&#x20;

&#x20;              \= 0 - independent of gas saturation (default).&#x20;

&#x20;              ≠ 0 – gas storage capacity related to gas saturation.       &#x20;

_CompNum_     number of mass components being absorbed by this rock.    &#x20;

Record **CBMDA.2**

&#x20;                        Free format for 4 parameters, or Format(A16,3E10.4)&#x20;

&#x20;                        CompName, GsL, PL, rhosrb

_CompName_   The mass component name (the name of gas, tracer or other components) that has been defined in the model.&#x20;

_GsL_                  dry, ash-free Langmuir storage capacity (sm3/kg-rock) for the component in this rock.&#x20;

_PL_                     Langmuir pressure (Pa)&#x20;

_rhosrb_              Sorbed Gas Density (kg/m3)

Repeat record **CBMDA.2** CompNum times for all the components absorbed to this rock. Maximum 5 components are allowed for each rock (CompNum<=5).

Additional sets for different rocks can be added by repeating records of CBMDA.1 and CMBDA.2.&#x20;

**Used in**: All EOS modules

**Example**:

_CBMDA_

_COAL, 0.156, 0.0672, , 2                           // rock coal absorb 2 gases_

_CH4, 0.0310, 1903.e3, 1180.e10             // neglecting_ swelling and shrinkage effect with a large density.&#x20;

_CO2, 0.0152, 4688.5e3, 421.e10_
