# Problem 5 - Five-Spot Geothermal Production/Injection under extremely high temperature

The problem was originally  presented in iTOUGH2-EOS1sc user's guide (Magnúsdóttir and Finsterle, 2015). It is a modified version of the [geothermal five-spot problem (problem 3)](problem-3-five-spot-geothermal-production-injection-rfp.md) . The five-spot well pattern is shown in Figure 10-2. The reservoir parameters are the same as summarized in Table 10-1, except in this example the initial temperature is 1200°C, initial pressure is 50 MPa, and injection enthalpy is 3000kJ/kg. The model setup is identical to the problem 3. &#x20;

This model can be run using different water property formulations. For the first simulation, IE(111) is set as 1 so that only the IAPWS-IF97 formulation is used. The cooling of the reservoir is simulated for 55 years of production.  The temperature near the production has decreased to 531.5°C after 55 years. The temperatures and pressures are always within the operational limit of the IAPWS-IF97 formulation; an extrapolation of the formulation is not required. Next, IE(111) is set as 2 so that a combination of the IAPWS-IF97 and IAPWS-95 formulations is used. For this option, IAPWS-95 is used for temperature above or equal to 800°C, and IAPWS-IF97 is used to increase computational speed once the temperature drops below 800°C. In this case, the initial temperature of 1200°C is above the operational temperature limit of 1000°C for IAPWS-95. However, the temperature and pressure results match well with the results when only IAPWS-IF97 is used. Hence, this extrapolation of the IAPWS-95 formulation above its operational limit gives accurate results. The main disadvantage of using IAPWS-95 is the relatively slow computational speed. The IAPWS-IF97 formulation is based on IAPWS-95, and it is significantly faster, as discussed by Magnusdottir and Finsterle \[2015].&#x20;

**Input files**

[INFILE.zip](https://drive.google.com/file/d/1q8sdD7\_ekwM1-28OGSBQrjRnOjc-dAz7/view?usp=sharing)

**Output Files**

[output\_files.zip](https://drive.google.com/file/d/1kCfuBZmJOySmzTA5BYrvpMkz12ed5mKh/view?usp=sharing)
