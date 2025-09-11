# CHEMP

**CHEMP**         provides data for calculating the thermophysical properties of the NAPL/chemical. The units of many of these constants are not standard metric units, and care must be taken to ensure that the appropriate units are used. Most of the data used in this block can be taken from Appendix A of Reid et al. (1987), where the same units are used as here.

Record **CHEMP.1**

&#x20;                       Free format, or Format(I5)

&#x20;                       NumHyC

_NumHyC_          number of organic chemicals/hydrocarbons for which data are to be entered. _NumHyC_ must be <19.

Record **CHEMP.2**

&#x20;                       Free format, or Format(A20, 8I5)

&#x20;                       HcNames, RecordID(8)

_HcNames_       name of the organic chemical.

_RecordID_       a list of the data record IDs. Only the records listed  here will be read. As many as 8 IDs can be listed.  The ID must be in the range of  3-10 corresponding to the following data records, No additional data record will be read if it is neglected. Most data records are not required or have been provided internally for the ECOF module.  (For ECOF module only)

Record **CHEMP.3**

&#x20;                       Free format for 5 parameters, or Format (5E10.4)

&#x20;                       TCRITM, PCRITM, ZCRITM, OMEGAM, DIPOLMM

_TCRITM_          chemical critical temperature, K.

&#x20;_PCRITM_ chemical critical pressure, bar (1 bar = $$10^5$$ Pa).

&#x20;_ZCRITM_        chemical critical compressibility.

&#x20;_OMEGAM_     Pitzer's acentric factor for the chemical.

&#x20;_DIPOLMM_     chemical dipole moment, debyes.

Record **CHEMP.4**

&#x20;                       Free format for 5 parameters, or Format (5E10.4)

&#x20;                       TBOILM, VPAM, VPBM, VPCM, VPDM

_TBOILM_          chemical normal boiling point, K.

_VPAM_               chemical vapor pressure constant from Reid et al. (1987). If VPAM ≠ 0 use Wagner correlation (Reid et al., 1987), for VPAM = 0 use Antoine Correlation.

_VPBM_               chemical vapor pressure constant from Reid et al. (1987).

_VPCM_               chemical vapor pressure constant from Reid et al. (1987).

_VPDM_               chemical vapor pressure constant from Reid et al. (1987).

Record **CHEMP.5**

&#x20;                       Free format for 5 parameters, or Format (5E10.4)

&#x20;                       AMWTM, CPAM, CPBM, CPCM, CPDDM

_AMWTM_          chemical molecular weight, g/mole.

_CPAM_               chemical ideal gas heat capacity constant from Reid et al. (1987).

_CPBM_               chemical ideal gas heat capacity constant from Reid et al. (1987)

_CPCM_               chemical ideal gas heat capacity constant from Reid et al. (1987)

_CPDDM_            chemical ideal gas heat capacity constant from Reid et al. (1987)

Record **CHEMP.6**

&#x20;                       Free format for 5 parameters, or Format (5E10.4)

&#x20;                       RHOREFM, TDENREF, DIFV0M, TDIFREF, TEXPOM

_RHOREFM_       reference NAPL (liquid) density, kg/m3.

_TDENREF_         reference temperature for NAPL density, K.

_DIFV0M_            reference binary diffusivity of VOC in air, m2/s.

_TDIFREF_           reference temperature for gas diffusivity, K.

_TEXPOM_          exponent for calculation of chemical diffusivity.

Record **CHEMP.7**

&#x20;                       Free format for 5 parameters, or Format (5E10.4)

&#x20;                       VLOAM, VLOBM, VLOCM, VLODM, VOLCRITM

Two options are available for calculating the NAPL liquid viscosity. The liquid viscosity constants VLOAM - VLODM for the desired NAPL may be assigned data given in Table 9-8 of Reid et al. (1987), and the viscosity will be calculated using a polynomial fit to actual viscosity data (Eq. 4.3.11 in[ TMVOC user manual](https://tough.lbl.gov/assets/files/Tough3/TMVOC_Users_Guide.pdf)). Alternatively, VLOAM and VLOBM may be set equal to 0, and VLOCM and VLODM are assigned equal to a reference viscosity and a reference temperature, respectively. In this case, the viscosity is calculated from a more general (and less accurate) empirical correlation (Van Velzen et al., 1972).

_VLOAM_            liquid NAPL viscosity constant from Reid et al. (1987).

_VLOBM_            liquid NAPI viscosity constant from Reid et al. (1987).

_VLOCM_            liquid NAPL viscosity constant from Reid et al. (1987). If VLOAM and VLOBM = 0, VLOCM is reference NAPL viscosity in units of cP (1 cP = 10-3 Pa-s).

_VLODM_            liquid NAPL viscosity constant from Reid et al. (1987). If VLOAM and VLOBM = 0, VLODM is reference temperature for NAPL viscosity in units of Kelvin.

_VOLCRITM_     chemical critical volume, cm3/mole.

Record **CHEMP.8**

&#x20;                       Free format for 4 parameters, or Format (4E10.4)

&#x20;                       SOLAM, SOLBM, SOLCM, SOLDM

The chemical solubility is calculated from the polynomial SOLUBILITY = SOLAM + SOLBM\*_T_ + SOLCM\* $$T^2$$+ SOLDM\* $$T^3$$. If data for the solubility as a function of temperature are available, then SOLAM, SOLBM, SOLCM, and SOLDM should be calculated from a polynomial fit of the data. If such data are not available (the usual case), the solubility will be assumed to be constant, and SOLAM should be set equal to the known solubility, with SOLBM, SOLCM, and SOLDM set equal to 0.

_SOLAM_            constant for chemical solubility in water, mole fraction.

_SOLBM_            constant for chemical solubility in water, mole fraction/$$K$$.

_SOLCM_            constant for chemical solubility in water, mole fraction/$$K^2$$.

_SOLDM_            constant for chemical solubility in water, mole fraction/$$K^3$$.

Record **CHEMP.9**

&#x20;                       Free format for 3 parameters, or Format (3E10.4)

&#x20;                       OCKM, FOXM, ALAMM

_OCKM_               chemical organic carbon partition coefficient Koc (see Eq. 4.4.2 in [TMVOC user manual](https://tough.lbl.gov/assets/files/Tough3/TMVOC_Users_Guide.pdf)), m3/kg.

_FOCM_               default value for fraction of organic carbon in soil, used for all domains for which no specific value is provided in record ROCKS.1.1.

_ALAMM_            decay constant for biodegradation of VOC, s-1. Biodegradation is assumed to take place only in the aqueous phase, and to follow a first order decay law, MVOC(t) = MVOC,0 \* exp (-λ t). The decay constant λ = ALAMM is expressed in terms of the half life T1/2 of the VOC as follows: λ = (ln 2) / T1/2. Default is ALAMM = 0.

Record **CHEMP.10** (for ECOF module only)&#x20;

&#x20;                       Free format for 20 parameters, or Format (20E10.4)

&#x20;                       bij(20)

_bij_                   a list of user-specified binary interaction coefficients for current component, the number of the inputted coefficients must be equal to the total hydrocarbon component number NumHyC+1 and in the order consistent with the components defined under this keyword (**CHEMP**) with additional coefficient at the end for water.&#x20;



Repeat records CHEMP.2 through CHEMP.10 for a total of _NumHyC_ (up to eighteen) different organic chemicals.

**Used in**: TMVOC, ECOF

**EXAMPLE 1**:

_CHEMP_

_2_                                                              //Number of organic chemicals

_BENZENE_                                             // Name of the first chemical

_562.2, 48.2, 0.271, 0.212, 0.0_           //CHEMP.3 for   BENZENE&#x20;

_353.2, -6.98273, 1.33213, -2.62863, -3.33399_                            //CHEMP.4 for BENZENE

_78.114, -.3392E+02, 0.4739E+00, -.3017E-03, 0.7130E-07_    //CHEMP.5 for BENZENE

_885., 289.00, 0.770E-05, 273.10, 1.52_                                       //CHEMP.6 for BENZENE

_0.4612E+01, 0.1489E+03, -.2544E-01, 0.2222E-04, 259.0_    //CHEMP.7 for BENZENE

_0.411E-03, 0.000E+00, 0.000E+00, 0.000E+00_                 //CHEMP.8 for BENZENE

_0.891E-01, 0.001, 0.0_                                                                   //CHEMP.9 for BENZENE

_n-DECANE_                                                                                    // Name of the second chemical

_617.700, 21.200, 0.249, 0.489, 0.00_                                         //CHEMP.4 for n-DECANE

_447.300, -8.56523, 1.97756, -5.81971, -0.29982_                   //CHEMP.4 for n-DECANE

&#x20;_142.286, -7.913E+0, 9.609E-1, -5.288E-4, 1.131E-7_               //CHEMP.5 for n-DECANE

&#x20;_730.000, 293.000, 1.000E-5, 293.000, 1.600_                    //CHEMP.6 for n-DECANE

_0.0, 0.0, 0.5900, 293.000, 603.000_                                    //CHEMP.7 for n-DECANE

_3.799e-7_                //CHEMP.8 for n-DECANE, constant solubility

_0.000_                     //CHEMP.9 for n-DECANE. The first parameter is 0.0, others set to default values.

**EXAMPLE 2 (for ECOF)**:

_CHEMP_

3                                                              //Number of hydrocarbon components

CO2, 10                                                  // Name of the first component, will read data record 10 (bij) only.

0.0, 0.086292, 0.097866<sup>\*</sup>                 // bij between CO2 and  CO2, C4H10, C10H22 , respectively.&#x20;

C4H10,10        &#x20;

8.6292E-02, 0.0, 3.3693E-08         // bij between C4H10 and  CO2, C4H10, C10H22 , respectively

C10H22,10

9.7866E-02, 3.3693E-08, 0.0          // bij between C10H22 and  CO2, C4H10, C10H22 , respectively

\*The coefficients between water and and these components (the 4th slot) do not present in the input. The default values will be used.   &#x20;
