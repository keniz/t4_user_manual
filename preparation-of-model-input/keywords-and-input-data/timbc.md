# TIMBC

**TIMBC**            permits the users to specify time-dependent Dirichlet boundary conditions. All values in this data block are read in free format (be careful, this record does not compatible with TOUGH3 input). The inputs either is through a file named "timbc.dat" or through the data section following this keyword. If "timvsp.dat" exists in the working folder, data are directly read from the file and the inputs in the TIMBC section will be neglected.&#x20;

Record **TIMBC.1**

&#x20;                       NTPTAB, T3Comp

_NTPTAB_          number of elements with time-dependent boundary conditions.

T3Comp          This parameter is optional. If  T3Comp="T3", the input format will be compatible with TOUGH3 input ( see TOUGH3 user manual for details), and the following input formatting will not be applied.&#x20;

Record **TIMBC.2**   &#x20;

&#x20;                       BEleName, NBCP, NBCPV&#x20;

_BEleBame_        name of boundary element

_NBCP_               number of times.

_NBCPV_            numbering of primary variable that is time dependent, e.g., 1 for pressure. It can be different for different EOS module and different phase state condition.&#x20;

Record **TIMBC.3**

&#x20;                       TIMBCV, PGBCEL

_TIMBCV_          the time when primary variable _NBCPV_ at boundary element _BCELM_ is specified.

_PGBCEL_          value of primary variable _NBCPV_ at boundary element _BCELM_ at time _TIMBCV._  A special case will be evoked if _PGBCEL<0.0._ Once _PGBCEL<0.0,_ the current element will return to regular element with a volume of abs(_PGBCEL),_ and will not be treated as first type boundary since time _TIMBCV_.  It is also allowed this element changes back to first type boundary again if  _PGBCEL_ become larger than 0.0 at later time.

The default phase state condition will be the current condition of the element. User may specify a new phase condition through a special case for NBCPV =2, by PGBCEL=:

&#x20;                       0-1.0:       default phase condition.

&#x20;                       10.0+sg:  two-phase condition.

&#x20;                       20.0+xg:  single gas phase condition.

&#x20;                      30.0+xg:  single aqueous phase condition.

Repeat TIMBC.3 for _NBCP_ times.&#x20;

Repeat records TIMBC.2, TIMBC.3 for all _NPTTAB_ elements.

**Used in**: All EOS modules

**Example**

_TIMBC_

_2                                            // time-dependent first-type boundary at 2 elements_&#x20;

_ELEM1, 3, 1                         // 1st element name, change at 3 times, time-dependent: 1st PV_&#x20;

_1000.0, 1.0e7                     //time1, the value of 1st primary variable at time1_

_2000.0, 2.0e7                    //time2, the value of 1st primary variable at time2_

_4000.0, 2.5e7                    //time3, the value of 1st primary variable at time3_

_ELEM2, 2, 4                       // 2nd element name, change at 2 times, time-dependent: 4th PV_&#x20;

_2000.0, 40.0                     // time1, the value of 4th primary variable at time1_

_4000.0, 45.0                     // time2, the value of 4th primary variable at time2_
