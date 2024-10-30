# Problem 1 - Brine Density Calculation (dnh)

This problem is from the  sample problem No. 1  in TOUGH3/EWASG user manual.&#x20;

The problem demonstrates the brine correlations. Several element subproblems are simulated, which are entirely independent of each other (no flow connections between subproblems), except that being run together they all must go through the same sequence of time steps. Only a single time step (1E-8 sec) is computed to calculate the brine density at different initial salt mass fraction. The salt content approximately varies from 1 to 6 molar. The initial condition for these elements are presented in Figure 10-10.

<figure><img src="../../.gitbook/assets/image (77).png" alt="" width="563"><figcaption><p>Figure 10-10 Initial conditions representing different salt content for the 6 elements.  </p></figcaption></figure>

Brine properties can be calculated with different approaches through the options specified by IE array. Discussion of these IE options are present in [Section 7/EWASG](../../process-modeling/ewasg.md). Data block OUTPU is used to select the liquid density as a single print-out variable. Two simulation cases are run:&#x20;

(1) IE(4)=6, using Driesner (2007) for brine density calculation.

(2) IE(4)=1 and IE(15)=4, using Andersen et al. (1992) for density calculation, using Lorenz et al. (2000) for brine enthalpy calculation.

Note that if only either the brine density (IE(4)) or enthalpy (IE(15)) is specified to use the Driesner’s correlation, TOUGH4 internally assigns the other brine property uses the Driesner’s correlation as well. Table 10-2 shows the results of calculated brine density for the both cases. The brine densities are slightly overestimated with IE(4) = 1, compared to those by Driesner (2007).

_**Table 10-2 Simulated brine density for case 1 and case 2**_

<table><thead><tr><th width="117">Element</th><th width="168">case 1 (kg/ m^3)</th><th>case 2 (kg/m^3)</th></tr></thead><tbody><tr><td>F   1</td><td>0.85027E+03</td><td>0.86241E+03</td></tr><tr><td>F   2</td><td>0.89252E+03</td><td>0.89902E+03</td></tr><tr><td>F   3</td><td>0.93441E+03</td><td>0.94535E+03</td></tr><tr><td>F   4</td><td>0.97668E+03</td><td>0.99803E+03</td></tr><tr><td>F   5</td><td>0.10198E+04</td><td>0.10571E+04</td></tr><tr><td>F   6</td><td>0.10642E+04</td><td>0.11286E+04</td></tr></tbody></table>

Input Files:   [INFILE\_case1](https://drive.google.com/file/d/1WbzuSKlxHojpJ1zkjPwHiQjI8mCxhrTJ/view?usp=sharing),  [INFILE\_case2](https://drive.google.com/file/d/1OIVToiUVWHTLA43-4szVQzqpeQu3FR1Y/view?usp=sharing)

OutputFiles: [dnh\_results\_case1.zip](https://drive.google.com/file/d/1z2U3xQ2qngNQR61ejcRAkd92TD8DSdvZ/view?usp=sharing),  [dnh\_results\_case2.zip](https://drive.google.com/file/d/19VDV8Q9RxGhUgT3-zUaHDS1UmANxa0Wx/view?usp=sharing)
