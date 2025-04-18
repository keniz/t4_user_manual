# 9️⃣ OUTPUTS

TOUGH4 produces a variety of printed output, most of which can be controlled by the user. In the initialization phase TOUGH4 writes out the general information for model setup and other related system information to the standard output file (TMsimulation.log). This is followed by documentation on block-by-block permeability modification, on settings of the MOP- and MOP2-parameters for choosing program options, and on the EOS-module. During execution TOUGH4 can optionally generate a brief printout for Newtonian iterations and time steps. The file TMsimulation.log also includes the volume- and mass-balances at each specified printout times or time step. For MPI simulation, additional log files (additional\_TMsimulation1.log, additional\_TMsimulation2.log, ...) may be written by other than the master CPU for additional time-stepping/warning information from the corresponding CPU. &#x20;

TOUGH4 generates output files for pre-defined selection of element, connection, or generation variables based on KDATA in block PARAM (see Table 29) or user specified variables with keyword OUTPU.  Separate files in the selected format (either CSV for positive KDATA or TECPLOT for negative KDATA) will be generated for element-, connection-, and sinks/sources-related outputs at user-specified simulation times in block TIMES or time step frequencies in block PARAM.

Table 29. Standard output based on KDATA

<table data-header-hidden><thead><tr><th width="296"></th><th></th></tr></thead><tbody><tr><td>abs (KDATA) = 1: a selection of element variables</td><td></td></tr><tr><td>Output variable</td><td>Comment</td></tr><tr><td>Pressure</td><td> </td></tr><tr><td>Temperature</td><td>Only in nonisothermal mode</td></tr><tr><td>Saturation</td><td>Saturation of all phases</td></tr><tr><td>Mass fraction</td><td>Mass fraction of all components in all mobile phases</td></tr><tr><td>Relative permeability</td><td>Relative permeability of all mobile phases</td></tr><tr><td>Capillary pressure</td><td>Between mobile phases</td></tr><tr><td>Density</td><td>Density of all mobile phases</td></tr><tr><td>Porosity</td><td> </td></tr><tr><td>Biomass</td><td>Biomass of all microbial populations</td></tr><tr><td>abs (KDATA) = 2: in addition, a selection of connection variables</td><td></td></tr><tr><td>Heat flow</td><td>Only in nonisothermal mode</td></tr><tr><td>Total flow</td><td> </td></tr><tr><td>Phase flow</td><td>Flow of all mobile phases</td></tr><tr><td>Diffusive flow</td><td>Only when "accounting for diffusion" is TRUE, see <a href="preparation-of-model-input/keywords-and-input-data/modde.md">MODDE.3</a></td></tr><tr><td>abs (KDATA) = 3: in addition, a selection of generation variables</td><td></td></tr><tr><td>Generation rate</td><td>Mass (kg/s) or energy (J/s) rate depending on generation type</td></tr><tr><td>Flowing enthalpy</td><td>Only in nonisothermal mode</td></tr><tr><td>Fractional flow</td><td>Only for production</td></tr><tr><td>Wellbore pressure</td><td>Only for production wells operated on deliverability against specified bottomhole pressure</td></tr></tbody></table>

TOUGH4 allows the user to select the output variables to be printed using block OUTPU. The user can choose any number of element-, connection-, and generation-related output variables. A lumped set of primary variables or secondary parameters can be selected, and other information, such as grid-block or connection coordinates, index of elements, connection, or sinks/sources, and element names, can be included as well. The list of the output variables is shown in [Table 18](preparation-of-model-input/keywords-and-input-data/outpu.md). The header and unit of variables/parameters selected for printout will be generated accordingly.

By default, outputs are printed to both the default standard output file (output\_data) and the CSV format files. Users may opt out printing output variables to the standard output file, particularly for large-scale simulations, to avoid creating a very big file. TOUGH4 also offers an option to generate a file in a format suitable for TECPLOT. The output variables written to the standard output file can be extracted for visualization using a reformatting program (such as EXT, a free post-processing program downloadable from the TOUGH website, which parses the standard output file along with spatial information provided in the MESH file and then generates a plot file in a format suitable for visualization, for instance, using TECPLOT). It should be noted that EXT calculates the components of flow vectors at the centers of grid blocks; in the current version of the OUTPU feature, flow rates and velocities are simply printed for each connection.

&#x20;Time series of some parameters for plotting can optionally be written to files in the CSV file format using input keyword FOFT (for elements), COFT (for connections), GOFT (for sinks and sources), and ROFT (for rocks). TOUGH4 will generate separate files for each element, connection, sink/source, and rocks. TOUGH4 provides options for users to select the parameters to be written out. &#x20;

For wellbore simulations (drift-flux model is turn on) , additionally to the regular TOUGH4 outputs, specific wellbore outputs are generated:

* Part of the main TOUGH4 file output (TMsimulation.log):

&#x20;              \--Wellbore simulation parameters.

&#x20;              \-- Wellbore geometry (cells followed by faces).

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
