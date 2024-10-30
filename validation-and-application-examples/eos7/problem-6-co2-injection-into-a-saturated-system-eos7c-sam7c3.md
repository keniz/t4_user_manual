# Problem 6- CO2 Injection into a Saturated System (EOS7C/SAM7C3)

This problem is from the example SAM7C3 in TOUGH3/EOS7C user manual. It demonstrates the capabilities of EOS7 for modeling CO2 injection into saturated systems such as aquifers. The geometry consists of a one-dimensional radial system 10 m thick with CO2 injection at a rate of 8.4 $$kg/s$$. The outer boundary is held at constant pressure and liquid saturated conditions. TOUGH3 simulation requires that a small amount of CH4 is co-injected with CO2 to improve the numerical behavior for iteratively solving gas solubility.  TOUGH4  improves the numerical approach for solving gas solubility  and no co-injection of  small amount of CH4 is needed. The initial pressure is uniform at 150 bars with temperature set at 65 °C. We can see from the output file, after two days (1400 tonnes of CO2 injected), the CO2 gas plume reaches gridblock A1 7, 26 m from the injection point.

**Input File:**         [INFILE.zip](https://drive.google.com/file/d/1ITmdYmk1Z\_3b9y6Fzp0wcYNzHyVq8uqp/view?usp=sharing)

**Output Files:**   [outputfiles.zip](https://drive.google.com/file/d/1mdvuvOFr\_0yJyIDBOaje74UqyYF3fouK/view?usp=sharing)
