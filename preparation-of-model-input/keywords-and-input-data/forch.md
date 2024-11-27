# FORCH

FORCH           Invokes flow calculation according to the Forchheimer equation; introduces information on non-Darcy flow coefficient model and weighting scheme.

Record FORC&#x48;**.1**

&#x20;                       Free format for 7 parameters, or FORMAT (2I5, 6E10.4)

&#x20;                       IFORCH, MFORCH, (FORCH(I), I=1,6)

IFORCH         Integer parameter to choose type of non-Darcy flow coefficient model (see Table x, in [Non-Darcy Flow](../../governing-equations/non-darcy-flow.md) section). If a negative number is given, the Forchheimer equation is applied to gas flow only; liquid flow is governed by Darcy’s law.&#x20;

MFORCH      Determines interface weighting scheme for non-Darcy flow coefficient β :  &#x20;

&#x20;                       MFORCH = 0: Upstream weighting (recommended)&#x20;

&#x20;                       MFORCH = 1: Upstream weighting with WUP (see record PARAM.3)&#x20;

&#x20;                       MFORCH = 2: Harmonic weighting&#x20;

&#x20;                       MFORCH = 3: Geometric average&#x20;

&#x20;                       MFORCH = 4: Arithmetic average&#x20;

FORCH(I) I = 1, …, 6;          user-specified parameters for non-Darcy flow coefficient model (see [Table x](../../governing-equations/non-darcy-flow.md); only needed for models IFORCH = 1 and 14).

Record FORC&#x48;**.2**

&#x20;                       Free format or FORMAT (8A10)

&#x20;                         ND\_Rocks1,  ND\_Rocks2, ......                        &#x20;

ND\_Rocks      Input a list of rocks in which the flow will be treated as non-Darcy flow. These rocks must be defined in the [ROCKS](rocks.md) data section. If no rock is specified in this record, the whole flow system will be treated as non-Darcy flow.&#x20;

**Used in**: All EOS modules

**Example**:

FORCH

2, 0             //use the second model for the coefficient calculation; use upstream weighting.

SAND1, SAND2    //flow in rock SAND1 and SAND2 is treated as non-Darcy flow.&#x20;
