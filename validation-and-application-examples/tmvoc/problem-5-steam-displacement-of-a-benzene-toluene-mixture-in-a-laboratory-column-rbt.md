# Problem 5-Steam Displacement of a Benzene-Toluene Mixture in a Laboratory Column (rbt)

This is the sample problem no. 5 in TOUGH3/TMVOC. It is a variation of sample problem no. 4, corresponding to a different experiment of Hunt et al. (1988) in which instead of trichloroethylene a two-component mixture of benzene and toluene was injected over a period of 120 s. The input file is essentially identical to the one for the TCE problem (problem 4), except that (i) CHEMP data were changed to toluene and benzene, (ii) The model includes 4 components (water, air, toluene, benzene), (iii) initial conditions now require 5 parameters, and (iv) injection specifications were modified. In TOUGH4, it is allowed to use the first four characters of component name as source/sink type. The type "tolu" and "benz" in the GENER data represent injection of  toluene and benzene respectively. At prevailing conditions of (T, P) = (22 °C, 1.013e5 Pa) the densities of benzene and toluene are, respectively, 878.94 and 865.06 kg/m3. Injection rates were set in such a way that 9 ml of each would be injected in 120 s. Following Adenekan (1992), we also increased the irreducible gas saturation from a value of .001 used in the TCE problem no. 4 to .01. The results of the VOC injection run are generally similar to what was obtained for the TCE problem.

VOC emplacement is followed again by a waterflood which in this case consists of two parts, a high-rate part in which 9 pore volumes of water are injected at a Darcy velocity of 15 m/day, and a low-rate part in which 1.2 pore volumes are injected at a Darcy velocity of 0.4 m/day. The 15 m/day Darcy velocity corresponds to a volumetric water injection rate of 15\*20.428e-4/86400 = 3.5465e-7 m3/s, which at ambient water density of 997.649 kg/m3 translates into a mass rate of 3.5382e-4 kg/s. This rate is maintained for 18.162e3 seconds, corresponding to injection of 9 pore volumes. Subsequently injection rate is changed to 9.4352e-6 kg/s, corresponding to a Darcy velocity of 0.4 m/day, and injection continues for another 90.809e3 seconds, so that at the final time of 108.971 e3 seconds a total of 10.2 pore volumes have been injected.&#x20;

The SAVE file of the first run segment is used as data block INCON in the input file for waterflooding. Note that we set MOP(12)=2, to rigorously maintain desired total water injection across the step change in water rate after 9 pore volumes, corresponding to t = 18.162e3 s.&#x20;

In the third part of the simulation, the benzene/toluene mixture is mobilized by a steamflood. The final save file from the second run segment is used as the initial condition of  this part of simulation.  During this period, steam with an enthalpy of $$1.562 \times 10^6$$_J/kg_ is injected at a rate of $$3.5341 \times 10^{-5}$$ kg/s for a period of 9000 s.&#x20;

The simulation results of each part match the corresponding results by TOUGH3/TMVOC very well. For discussion of the results, user may refer to TMVOC user manual.&#x20;

**Part 1:**&#x20;

**Input Files:**                 I[NFILE\_rbt1.zip](https://drive.google.com/file/d/1J4bII\_5hgouP35REj\_L6xl0VGDI71Ts7/view?usp=sharing)

**Output Files:**            [output files](https://drive.google.com/file/d/1TjhvlGStVPiesDipyDSQLwX0MFm3Ljsc/view?usp=sharing)

**Part 2:**

**Input Files:**                 [INFILE\_rbt2.zip](https://drive.google.com/file/d/1CW3b4l69drjBqyZ\_vFwDdt7OiOU3Avvp/view?usp=sharing)

**Output Files:**           [ output files](https://drive.google.com/file/d/1iA6kd8YGeP2tSqdqFPmgaUjR3iQrgbw8/view?usp=sharing)

**Part 3:**

**Input Files:**                 [INFILE\_rbt3.zip](https://drive.google.com/file/d/1LY-MtUaw8ePy4XxBgh-fbffLN-wDJhKd/view?usp=sharing)

**Output Files:**            [output files](https://drive.google.com/file/d/1Zhbm39RQ\_\_15LSCt-SNb0sckbBt5NHSS/view?usp=sharing)
