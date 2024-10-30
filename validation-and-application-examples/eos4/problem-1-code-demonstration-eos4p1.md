# Problem 1 - Code Demonstration （eos4p1)

This problem demonstrates various initialization options and phase transitions using EOS4. A number of one- and two-element subproblems are simulated which are entirely independent of each other (no flow connections between subproblems), except that being run together they all must go through the same sequence of time steps. The input file for running with the EOS4 fluid properties module is provided for download. Parameter MOP(19) in the first record of data block PARAM was set equal to 1, to permit initialization of the EOS4 module with the primary variables of (Pg, Sg, T) for two-phase. Data block OUTPU is used to select variables to print out.&#x20;

This problem can also be run using EOS3. The only different of the input file using EOS3 requires turning on vapor pressure lowering simulation (set IE(24)=1). Simulation of vapor pressure lowering effect is default in EOS4, but not in EOS3. It is interesting to note that simulation results from  both module match quite well, but their convergence behavior is significantly different.  &#x20;

Input files:  [INFILE\_eos4](https://drive.google.com/file/d/1fnFTkaCCarltE6l56oEy1Ic4-\_NvKIpT/view?usp=sharing) (alternative run using EOS3:  [INFILE\_eos3](https://drive.google.com/file/d/12ckDNGsEkha1TktJ0\_vUzzb6NiKlWvRt/view?usp=sharing))

Output Files: [eos4p1\_output.zip](https://drive.google.com/file/d/1rFMxUiKNWk5SwSO97hehVVIgPnheDShI/view?usp=sharing)
