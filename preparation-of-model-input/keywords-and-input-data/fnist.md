# FNIST

Running a simulation with EOS6 requires thermophysical properties (density, viscosity, enthalpy, ...... ) of the gas component which are stored in a file named "gas\_properties.dat".  User may create this file manually through downloading the thermophysical property data for a requested gas (see [Section 7-EOS6-subsection 3](../../process-modeling/eos6.md) for details).  If a simulation is run with an executable which includes Python interface, TOUGH4 can automatically fetch these data  from  [NIST Chemistry WebBook](https://webbook.nist.gov/chemistry/fluid/) and create the file "gas\_properties.dat".  FNIST is used to specify the parameters required for fetching data from the NIST web site.&#x20;

FNIST was originally designed for EOS6 simulation. User may also use it to get fluid property data for model validation of other EOS modules.&#x20;

**FNIST**           Introduces parameters for fetching thermophysical property data of a specific gas from  NIST Chemistry WebBook. The property data are fetched for given pressure and temperature conditions in user specified pressure and temperature range.&#x20;

Record **FNIST.1**

&#x20;                       Free format for 7 parameters, or FORMAT (I5, 6E10.4)

&#x20;                       GasIndex, P\_Begin, P\_end, dP, T\_Begin, T\_ene, dT

GasIndex       Index of the gas. User may find it from the list at the bottom of this page. &#x20;

&#x20;P\_Begin         Beginning of the  pressure range , in MPa.&#x20;

&#x20;P\_end             ending of the  pressure range, P\_end  must be large than P\_Begin, in MPa.&#x20;

&#x20;dP                   The pressure increment, in MPa.

&#x20;T\_Begin         Beginning of the  temperature range , in <sup>o</sup>C.&#x20;

&#x20;T\_end             ending of the  temperature range, T\_end  must be large than T\_Begin, in <sup>o</sup>C.&#x20;

&#x20;dT                    The temperature increment, in <sup>o</sup>C.

Fetching data from NIST website could be slow. User may only request the pressure and temperature range that can fully cover the pressure and temperature of current simulation. The pressure and temperature  increment must be reasonable. It is suggested to limit the dimension of table less than 1000, (P\_end-P\_begin)/dP<1000 and (T\_end-T\_begin)/dT<1000.&#x20;

The data fetching will be performed at first run only. If "gas\_properties.dat" is already exist in the working directory, the fetching process will be skipped.&#x20;

To use this functionality, a TOUGH4 executable with Python interface  must be run. Two Python files (fetchWebBookData.py and TOUGH\_python\_module.py) in the TOUGH4 distribution package must be copied to the location where the TOUGH4 executable is located.&#x20;

Followings are the index of gases/fluids  that are included in  [NIST Chemistry WebBook](https://webbook.nist.gov/chemistry/fluid/):

1, Water\
2, Nitrogen\
3, Hydrogen\
4, Parahydrogen\
5, Orthohydrogen\
6, Deuterium\
7, Oxygen\
8, Fluorine\
9, Carbon monoxide\
10, Carbon dioxide\
11, Dinitrogen monoxide\
12, Deuterium oxide\
13, Methanol\
14, Methane\
15, Ethane\
16, Ethene\
17, Propane\
18, Propene\
19, Propyne\
20, Cyclopropane\
21, Butane\
22, Isobutane\
23, Pentane\
24, 2-Methylbutane\
25, 2,2-Dimethylpropane\
26, Hexane\
27, 2-Methylpentane\
28, Cyclohexane\
29, Heptane\
30, Octane\
31, Nonane\
32, Decane\
33, Dodecane\
34, Helium\
35, Neon\
36, Argon\
37, Krypton\
38, Xenon\
39, Ammonia\
40, Nitrogen trifluoride\
41, Trichlorofluoromethane\
42, Dichlorodifluoromethane (R12)\
43, Chlorotrifluoromethane (R13)\
44, Tetrafluoromethane (R14)\
45, Dichlorofluoromethane (R21)\
46, Methane, chlorodifluoro- (R22)\
47, Trifluoromethane (R23)\
48, Methane, difluoro- (R32)\
49, Fluoromethane (R41)\
50, 1,1,2-Trichloro-1,2,2-trifluoroethane (R113)\
51, 1,2-Dichloro-1,1,2,2-tetrafluoroethane (R114)\
52, Chloropentafluoroethane (R115)\
53, Hexafluoroethane (R116)\
54, Ethane, 2,2-dichloro-1,1,1-trifluoro- (R123)\
55, Ethane, 1-chloro-1,2,2,2-tetrafluoro- (R124)\
56, Ethane, pentafluoro- (R125)\
57, Ethane, 1,1,1,2-tetrafluoro- (R134a)\
58, 1,1-Dichloro-1-fluoroethane (R141b)\
59, 1-Chloro-1,1-difluoroethane (R142b)\
60, Ethane, 1,1,1-trifluoro- (R143a)\
61, Ethane, 1,1-difluoro- (R152a)\
62, Octafluoropropane (R218)\
63, 1,1,1,2,3,3,3-Heptafluoropropane (R227ea)\
64, 1,1,1,2,3,3-Hexafluoropropane (R236ea)\
65, 1,1,1,3,3,3-Hexafluoropropane (R236fa)\
66, 1,1,2,2,3-Pentafluoropropane (R245ca)\
67, 1,1,1,3,3-Pentafluoropropane (R245fa)\
68, Octafluorocyclobutane (RC318)\
69, Benzene\
70, Toluene\
71, Decafluorobutane\
72, Dodecafluoropentane\
73, Sulfur dioxide\
74, Hydrogen sulfide\
75, Sulfur hexafluoride\
76, Carbonyl sulfide

**Used in**:  EOS6 module, can also be used for model validation for all other EOS modules.

**Example**:

_FNIST_

_36, 0.1,  80., 0.5, 30.,  50., 5.0_           &#x20;

&#x20;_//obtained Argon thermophysical property data for pressure range 0.1-80Mpa, temperature range 30-50&#x20;_<sup>_o_</sup>_C with increment 0.5Mpa and 5.0 &#x20;_<sup>_o_</sup>_C, respectively._
