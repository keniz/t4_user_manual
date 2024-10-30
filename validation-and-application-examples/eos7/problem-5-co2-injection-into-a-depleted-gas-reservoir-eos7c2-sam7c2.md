# Problem 5-CO2 Injection into a Depleted Gas Reservoir (EOS7C2/SAM7C2)

The sample problem SAM7C2 in TOUGH3/EOS7C user manual was tested with TOUGH4/EOS7 to demonstrate the use of EOS7 for the injection of CO2 into a simplified two-dimensional depleted natural gas (CH4) reservoir. This problem is modeled after the case shown in Oldenburg et al. (2001). In the problem, a two-dimensional depleted natural gas reservoir lies above a water table in a cross-sectional tilted system. The upper right-hand corner gridblock is held at constant pressure while CO2 is injected in the middle-left of the reservoir. As CO2 is injected, the pressure increases and injected CO2 displaces CH4 toward the upper right-hand corner. The initial conditions are provided in the INCON file.

Simulation results  match the corresponding results by TOUGH3/EOS7C very well, Discussion of the  results can be found in TOUGH3/EOS7C user manual.

An alternative simulation was run for this problem using the free format input of TOUGH4. Brine and tracer do not exist in the reservoir for current model, but these two components must be included in the simulation with TOUGH3/EOS7C due to software limitation. In the alternative simulation,  two less equations are solved for each element, because brine and tracer are optional and do not need to be included in the simulation, which significantly improve the simulation efficiency.&#x20;

In the alternative simulation, definition of  gas components through keyword "GASES" for the CH4 and CO2 is required. The initial condition INCON file is from the normal simulation for 1.0e-8 second, which has two more components and two more primary variables.   In the MODDE data block, the InitCType is given a value  "FM1L1236" (FM-indicates special transformation input, 1L-primary variables will be inputted in 1 line for each gridblock, 1236-represent primary variables for current model will read from data number 1,2,3,6 of each gridblock in the INCON file. Details for special transformation input can be found in [Input for Initial Conditions](../../preparation-of-model-input/inputs-for-initial-conditions/).&#x20;

**Input Files:**       [sam7c2.zip ](https://drive.google.com/file/d/1mc6xYzdC2-y-ViU8sMhcM5p\_5WPMp42Z/view?usp=sharing)&#x20;

**Output Files:**     [output\_sam7c2.zip](https://drive.google.com/file/d/1CgyCuVN\_CvDjIAmPHureQyKuK0pSv-2x/view?usp=sharing)

I**nput/output files for alternative simulation:**  [sam7c2\_freeFormat\_inputOutput.zip](https://drive.google.com/file/d/195XNmuccE\_QafooOajK3Z322uHbh\_5Rx/view?usp=sharing)
