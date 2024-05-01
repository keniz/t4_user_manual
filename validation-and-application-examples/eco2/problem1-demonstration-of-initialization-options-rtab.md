# Problem1-Demonstration of Initialization Options (\*rtab\*)

ECO2 provides different initialization options. It accepts  initial condition files from TOUGH3/ECO2N, ECO2M, and ECO2N V2.0. This example demonstrates&#x20;



The input file as given in Fig. 10 demonstrates initialization of a TOUGH2/ECO2M run with ECO2N-type primary variables. This type of initialization is enabled by omitting the singleline data block INDEX that is required when initializing with the primary variables internally used in ECO2M (Table 2). The input file is completely identical to the corresponding input file for ECO2N, except for one single change in the third parameter in data block MULTI. This parameter specifies the number of phases treated by the fluid property module, and is NPH=3 for ECO2N, while it is NPH=4 in ECO2M. These NPH specifications are necessary, regardless of how many phases are actually present in a flow problem. The input file performs just a single infinitesimal time step (Δt = 10-9 s) and includes neither flow connections between grid blocks nor sinks or sources. Therefore, there is no flow and no changes in the initially specified thermodynamic conditions. The purpose of this problem is simply to demonstrate different options for initializing thermodynamic conditions. Initialization with standard ECO2N-style primary variables (Table 6) is made for a number of grid blocks in single-phase aqueous conditions (_a 1_, _a 3_, _a 5_), a single CO2- rich phase (_a 10_), and two-phase fluid (_A 14_, _A 15_, _A 19_). Several grid blocks are initialized with single-phase type primary variables, but with a CO2 mass fraction (primary variable #3) that is larger than can be dissolved in the aqueous phase, and smaller than required for single-phase gas conditions (_a 2_, _a 6_, _a 9_, _A 18_). The CO2 mass fractions for these blocks correspond to two-phase (aqueous-liquid or aqueous-gas) fluid conditions (see Fig. 6 and Section 5.1), and are internally converted to the appropriate phase saturations during initialization. Grid block _A 16_ is initialized with primary variable #3 corresponding to internal ECO2N useage, but primary variable #2 is larger than saturated salt mass fraction in the binary system water-salt. This specification corresponds to presence of solid salt, and is internally converted to Ss + 10. In some grid blocks both primary variables #2 and #3 are specified with conventions applicable for single-phase liquid conditions, but with salt mass fraction exceeding the solubility limit, and CO2 mass fraction being in the intermediate range between the liquid and gas phase limits (_a 4_, _a 7_, _a 8_, _a 11_, _A 17_). Salt as well as CO2 mass fractions for these blocks are converted to the appropriate internally used saturation variables. Finally, there are grid blocks (_A 20_, _A 21_) in which primary variable #2 is specified as salt molality (counted by convention as undissociated) in the binary water-salt system, which is internally converted to salt mass fraction. The internally used ECO2M-style primary variables generated from the ECO2N-style INCON data given in Fig. 10 are shown in Fig. 11, where phase indices are printed following the pound sign (#). Fig. 12 shows part of the printed output for this problem, with phase indices appearing in the column following the element index (header I). Results agree closely with ECO2N (Pruess, 2005). We emphasize that the preferred and recommended option is to initialize flow problems by means of the internally used primary variables (Table 2). The options of using ECO2N-style initialization and allowing salt and CO2 mass fractions to go out of range are provided as a convenience to users.