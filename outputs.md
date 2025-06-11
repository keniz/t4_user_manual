# 9️⃣ OUTPUTS

TOUGH4 produces a variety of printed output, most of which can be controlled by the user. Below is a list of TOUGH4 outputs and keywords to write the output.

The generation of output files and associated file format is managed by a range of input parameters as described below.

#### 1- Standard output file (TMsimulation.log)

The main TOUGH4 output is the standard output file (TMsimulation.log). In the initialization phase TOUGH4 writes out the general information for model setup and other related system information to the standard output file (TMsimulation.log). This is followed by documentation on block-by-block permeability modification, on settings of the MOP- and MOP2-parameters for choosing program options, and on the EOS-module. During execution TOUGH4 can optionally generate a brief printout for Newtonian iterations and time steps. The file TMsimulation.log also includes the volume- and mass-balances at each specified printout times or time step. For MPI simulation, additional log files (additional\_TMsimulation1.log, additional\_TMsimulation2.log, ...) may be written by other than the master CPU for additional time-stepping/warning information from the corresponding CPU. &#x20;

The content of the standard output file can be controlled using the PARAM keyword,

* KDATA parameter,
* MOP(1) allows to generate printout for each Newton-Raphson iteration
* MOP(2) through MOP(6) \[Advanced user recommendation] generate additional printout in various sub-routines, if set unequal 0. This feature should not be needed in normal applications, but it will be convenient when a user suspects a bug and wishes to examine the inner workings of the code.
* MOP(7) if unequal 0, a printout of input data will be provided.

WARNING: only the first 100 elements, connections and source/sinks in master CPU will be written in the log file.

#### 2- Main simulation results

The simulation results can be exported as part of the Standard output file or in separate files.

* IE(58) enables or not to generate single output file or 2 output files (link). If IE(58) =0 (default value if absent), Log information are written in the file ‘TMsimulation.log’ and simulation results are written in the file ’output\_data’. If IE(58) =1 (TOUGH2 and TOUGH3), log information and simulation results are written in the file ‘TMsimulation.log’.

By default, simulation result outputs are printed to both the default standard output file (output\_data) and CSV format files.Users may opt out printing output variables to the standard output file, particularly for large-scale simulations, to avoid creating a very big (output\_data) file. See IE(126)/ MOP2(26) in [Appendix C](appendix/c-additional-program-options.md).

Similarly to TOUGH2 and TOUGH3, the export of simulation results can be controlled by the KDATA parameter (part of PARAM keyword). In this case, TOUGH4 generates output files for pre-defined selection of element, connection, or generation variables based on KDATA in block PARAM (see Table 29) or user specified variables with keyword OUTPU.  Separate files in the selected format (either CSV for positive KDATA or TECPLOT for negative KDATA) will be generated for element-, connection-, and sinks/sources-related outputs at user-specified simulation times in block TIMES or time step frequencies in block PARAM.

Table 29. Standard output based on KDATA

<table data-header-hidden><thead><tr><th valign="bottom"></th><th valign="bottom"></th><th valign="bottom"></th></tr></thead><tbody><tr><td valign="bottom"> </td><td valign="bottom">Output variable</td><td valign="bottom">Comment</td></tr><tr><td valign="bottom">abs (KDATA) = 1: selection of Element variables</td><td valign="bottom">Pressure</td><td valign="bottom"> </td></tr><tr><td valign="bottom"></td><td valign="bottom">Temperature</td><td valign="bottom">Only in nonisothermal mode</td></tr><tr><td valign="bottom"></td><td valign="bottom">Saturation</td><td valign="bottom">Saturation of all phases</td></tr><tr><td valign="bottom"></td><td valign="bottom">Mass fraction</td><td valign="bottom">Mass fraction of all components in all mobile phases</td></tr><tr><td valign="bottom"></td><td valign="bottom">Relative permeability</td><td valign="bottom">Relative permeability of all mobile phases</td></tr><tr><td valign="bottom"></td><td valign="bottom">Capillary pressure</td><td valign="bottom">Between mobile phases</td></tr><tr><td valign="bottom"></td><td valign="bottom">Density</td><td valign="bottom">Density of all mobile phases</td></tr><tr><td valign="bottom"></td><td valign="bottom"> Porosity</td><td valign="bottom"></td></tr><tr><td valign="bottom"></td><td valign="bottom">Biomass</td><td valign="bottom">Biomass of all microbial populations</td></tr><tr><td valign="bottom">abs (KDATA) = 2:  selection of Element  + Connection variables</td><td valign="bottom">Heat flow</td><td valign="bottom">Only in nonisothermal mode</td></tr><tr><td valign="bottom"></td><td valign="bottom"> Total flow</td><td valign="bottom"></td></tr><tr><td valign="bottom"></td><td valign="bottom">Phase flow</td><td valign="bottom">Flow of all mobile phases</td></tr><tr><td valign="bottom"></td><td valign="bottom">Diffusive flow</td><td valign="bottom"><a href="https://lbl-2.gitbook.io/tough4-user-manual/preparation-of-model-input/keywords-and-input-data/modde">Only when "accounting for diffusion" is TRUE, see MODDE.3</a></td></tr><tr><td valign="bottom">abs (KDATA) = 3: selection of Element  + Connection + Generation variables</td><td valign="bottom">Generation rate</td><td valign="bottom">Mass (kg/s) or energy (J/s) rate depending on generation type</td></tr><tr><td valign="bottom"></td><td valign="bottom">Flowing enthalpy</td><td valign="bottom">Only in nonisothermal mode</td></tr><tr><td valign="bottom"></td><td valign="bottom">Fractional flow</td><td valign="bottom">Only for production</td></tr><tr><td valign="bottom"></td><td valign="bottom">Wellbore pressure</td><td valign="bottom">Only for production wells operated on deliverability against specified bottomhole pressure</td></tr></tbody></table>



#### 3- OUTPU keyword

A new feature available in TOUGH4 is the keyword OUTPU. TOUGH4 allows the user to select the output variables to be printed using block OUTPU. The user can choose any number of element-, connection-, and generation-related output variables. A lumped set of primary variables or secondary parameters can be selected, and other information, such as grid-block or connection coordinates, index of elements, connection, or sinks/sources, and element names, can be included as well. The list of the output variables is shown in [Table 18](preparation-of-model-input/keywords-and-input-data/outpu.md). The header and unit of variables/parameters selected for printout will be generated accordingly. Relevant to the OUTPU keyword is the IE(59) parameter.

#### 4- TECPLOT outputs

TOUGH4 also offers an option to generate a file in a format suitable for TECPLOT. The output variables written to the standard output file can be extracted for visualization using a reformatting program (such as EXT, a free post-processing program downloadable from the TOUGH website, which parses the standard output file along with spatial information provided in the MESH file and then generates a plot file in a format suitable for visualization, for instance, using TECPLOT). It should be noted that EXT calculates the components of flow vectors at the centers of grid blocks; in the current version of the OUTPU feature, flow rates and velocities are simply printed for each connection. The IE(126) / MOP2(26) parameter enables to control the printout format for the main simulation result file (traditional output, CSV or TECPLOT).

#### 5- Python generated outputs

Another additional feature of TOUGH4 is the ability to export simulation results to the Python interface (see [Section 5](numerical-method/python-functions/)). This is best managed using IE 79 to 82.

#### 6- Specific simulation results (_&#x58;_&#x4F;FT keywords)

Similarly to TOUGH2 and TOUGH3, the export of specific simulation results can be controlled by the FOFT, COFT, GOFT and the newly implemented ROFT keywords. These keywords are optional.

Time series of some parameters for plotting can optionally be written to files in the CSV file format using input keyword FOFT (for elements), COFT (for connections), GOFT (for sinks and sources), and ROFT (for rocks). TOUGH4 will generate separate files for each element, connection, sink/source, and rocks. TOUGH4 provides options for users to select the parameters to be written out.&#x20;

The format and frequency of the _&#x58;_&#x4F;FT output files can be controlled using the following options:

* PARAM keyword

o   TimeS\_Fq The frequency for writing time series output. Time series output file will be written every TimeS\_Fq time step, Default is 1.

* SELEC keyword

o   IE(117)/MOP2(117) Variables printed on FOFT files (time series)

o   IE(131) Control output of flux time-series using [COFT](https://lbl-2.gitbook.io/tough4-user-manual/preparation-of-model-input/keywords-and-input-data/coft).

o   IE(130) Control output of flux time-series using [ROFT](https://lbl-2.gitbook.io/tough4-user-manual/preparation-of-model-input/keywords-and-input-data/roft).

#### 7- Simulation results ‘SAVE’ file

Similarly to TOUGH2 and TOUGH3, at the end of a simulation, the primary variables and additional key parameters are saved into a SAVE file. The SAVE file can then be used as an INCON file to restart a simulation.

There is some opportunity to configure the frequency and format of the SAVE file using the parameters below:

* SELEC keyword

&#x20; o   IE(110) / MOP2(10) determines when the SAVE file will be written (link to MOMOP)

* PARAM keyword

&#x20;o   SAVE\_Fq provides the frequency for writing out SAVE file. SAVE file will be written every SAVE\_Fq time step.

* MOP(13) determines content of INCON and SAVE files.
* MOP(35) selects format of SAVE file: =0, free format; =1, in TOUGH3 format

#### 8- Simulation results for wellbore models

For wellbore simulations (drift-flux model is turn on) , additionally to the regular TOUGH4 outputs, specific wellbore outputs are generated:

* Part of the main TOUGH4 file output (TMsimulation.log):

&#x20;              \--Wellbore simulation parameters.

&#x20;              \-- Wellbore geometry (cells followed by faces).&#x20;

&#x20;              If the WELLB _ActionWord_ GEOTH or OFFMA are used, a summary will be presented.

* Fstatus0.dat file

&#x20;              \--Wellbore cell output at different times for every wellbore cell for a set of variables.&#x20;

&#x20;                 Default Variables are: WellID, Time, Depth, Sg, Pres, T, Dgas

* Fflow0.dat file

&#x20;              \--Wellbore face output at different times for every wellbore face for a set of variables.

&#x20;                 Default variables are: WellID, Time, Depth, Fliq, Fgas, VLiq, VGas, Umix

* WellHeadConditions0.dat

&#x20;              \--Summary of the wellhead conditions over the simulation

* WellStatus0.dat

&#x20;              \--Wellbore face output at the end of the simulation for every wellbore face for a set of variables.&#x20;
