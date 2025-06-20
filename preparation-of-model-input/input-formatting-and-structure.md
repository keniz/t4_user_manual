# Input formatting and structure

#### 1- TOUGH 4 input file structure

Similarly, than for TOUGH2 and TOUGH3, the main TOUGH4 input file _INFILE_ (default, or user specified name) provides inputs using data blocks defined by keywords. In the standard TOUGH4 input file data are organized in blocks which are defined by five-character keywords typed in columns 1-5, as in Table 16. Additionally, input can be provided in a flexible manner by means of one or several ASCII data files. Most of the required input data are still the same as TOUGH3. For convenience of users and to make this report self-contained, we repeat the introduction of input data and adopt the texts from TOUGH3 user’s guide directly.

The first record of the input file must be a problem title of up to 80 characters. The last record usually is ENDCY; alternatively, ENDFI may be used if no flow simulation is to be carried out (useful for mesh generation). Data records beyond ENDCY (or ENDFI) will be ignored. Some data blocks, such as those specifying reservoir domains (ROCKS), volume elements (ELEME), connections (CONNE), sinks/sources (GENER), and initial conditions (INDOM and INCON), have a variable number of records, while others have a fixed number of records. The end of variable-length data blocks is indicated by a blank record. The data blocks can be provided in arbitrary order; exceptions are (1) the first line must be the title line, (2) ELEME, if present, must precede CONNE, (3) MODDE must be specified before PARAM, INDOM, INCON.  The blocks ELEME and CONNE must either be both provided through the input file, or must both be absent, in which case alternative means for specifying geometry data will be employed.  Keyword START and MULTI which are used in TOUGH3 become obsolete. MULTI may still require only when NKIN ≠ NK. It must appear before MODDE.  The block INCON can be incomplete, with elements in arbitrary order, or can be absent. Elements for which no initial conditions are specified in INCON will then be assigned domain-specific initial conditions from block INDOM, if present, or will be assigned default initial conditions given in block PARAM, along with default porosities given in ROCKS. In TOUGH4 input, there is several new keywords are introduced including: MODDE, GASES, TRACR, BIODG, ROFT, SPAVA and WELLB.

The inputs for the keywords ELEME, CONNE, GENER, and INCON can also be done through files _MESH_ (or MINC), _GENER_, and _INCON_. The initialization of the arrays for geometry, generation, and initial condition data is always made from these files. Users can either provide these files at execution time, or they can be written from TOUGH4 input data at the initialization phase of the program.

The format of data blocks ELEME, CONNE, GENER, and INCON is basically the same when these data are provided as separate files or as part of the main input file. They are either in free format or remaining in the original TOUGH3 format. Input of these data through the main input file rather than as separate files offers some additional conveniences, which are useful when a new simulation problem is initiated. For example, a sequence of identical items (volume elements, connections, sinks or sources) can be specified through a single data record. Also, indices used internally for cross-referencing elements, connections, and sources will be generated internally by TOUGH4 rather than having them provided by the user. _MESH_, _GENER_, and _INCON_ files written by TOUGH4 can be merged into the main input file without changes, keeping the cross-referencing information.

If no data blocks GENER and INCON are provided in the main input file, and if no separate files _GENER_ and _INCON_ are present, defaults will take effect (no generation; domain-specific initial conditions from block INDOM, or defaults from block PARAM). If a user intends to use these defaults, the user must make sure that at execution time no files INCON or GENER are present from a previous run (or perhaps from a different problem). A safe way to use default GENER and INCON is to specify “dummy” data blocks in the input file, consisting of one record with GENER or INCON, followed by a blank record.

During initialization, two binary files _MESHA_ and _MESHB_ are created from the file _MESH_. If _MESHA_ and _MESHB_ exist in the working folder and the model total element number is larger than 50000, the code will ignore the _MESH_ file and the ELEME and CONNE blocks in the input file, and read geometric information directly from these two files, which will reduce the memory requirement for the master processor and enhance I/O efficiency for large model simulations. In this case, if the mesh is changed, _MESHA_ and _MESHB_ must be deleted from the working folder to make the changes take effect.&#x20;

At the end of each TOUGH4 simulation run, files _SAVE_ and _TABLE_ will be generated. These two files record the status of the flow system and coefficients of semi-analytical linear heat exchange with confining beds, respectively. _SAVE_ can be used as the initial conditions for continuation simulation by simply changing the file name _SAVE_ to _INCON_. If heat exchange with confining beds is considered in the simulation, file _TABLE_ will be read in continuation run for the heat-exchange calculation.

&#x20;**Table 16. TOUGH4 input data blocks**

<table data-header-hidden><thead><tr><th width="188"></th><th></th></tr></thead><tbody><tr><td>Keyword</td><td>Functions</td></tr><tr><td>TITLE</td><td>First record, single line with a title for the simulation problem</td></tr><tr><td>MESHM</td><td>Parameters for internal grid generation through MESHMaker</td></tr><tr><td>ROCKS</td><td>Hydrogeologic parameters for various reservoir domains</td></tr><tr><td>MULTI</td><td>Specifies number of fluid components and balance equations per grid block (obsolete), replaced by MODDE</td></tr><tr><td>SELEC</td><td>Used with certain EOS-modules to supply thermophysical property data</td></tr><tr><td>MODDE</td><td>Model design, specifies module to be run, modeling processes to be included, Length of gridblock name.</td></tr><tr><td>PARAM</td><td>Computational parameters; time stepping and convergence parameters; program options; default initial conditions</td></tr><tr><td>MOMOP</td><td>More program options</td></tr><tr><td>SOLVR</td><td>Parameters for linear equation solver</td></tr><tr><td>DIFFU</td><td>Diffusivities of mass components</td></tr><tr><td>FOFT</td><td>Specifies grid blocks for which time series data are desired</td></tr><tr><td>COFT</td><td>Specifies connections for which time series data are desired</td></tr><tr><td>GOFT</td><td>Specifies sinks/sources for which time series data are desired</td></tr><tr><td>ROFT</td><td>Specifies connected rocks for which time series data are desired</td></tr><tr><td>RPCAP</td><td>Parameters for relative permeability and capillary pressure functions</td></tr><tr><td>HYSTE</td><td>Parameters for hysteretic characteristic curves; required only if non-default values of parameters are used</td></tr><tr><td>TIMES</td><td>Specification of times for generating printout</td></tr><tr><td>*ELEME</td><td>List of grid blocks (volume elements)</td></tr><tr><td>*CONNE</td><td>List of flow connections between grid blocks</td></tr><tr><td>*GENER</td><td>List of mass or heat sinks and sources</td></tr><tr><td>INDOM</td><td>List of initial conditions for specific reservoir domains</td></tr><tr><td>*INCON</td><td>List of initial conditions for specific grid blocks</td></tr><tr><td>TIMBC</td><td>Specifies time-dependent Dirichlet boundary conditions</td></tr><tr><td>OUTPU</td><td>Specifies variables/parameters for printout</td></tr><tr><td>GASES</td><td>Defines gas components included in current simulation</td></tr><tr><td>CHEMP</td><td>Provides parameters for calculating the thermophysical properties of the NAPL/chemical</td></tr><tr><td>TRACR</td><td>Defines tracers included in current simulation</td></tr><tr><td>BIODG</td><td>Defines biodegradation reactions included in current simulation</td></tr><tr><td>WELLB</td><td>Specifies the parameters for wellbore models.</td></tr><tr><td>SPAVA</td><td>Introduce the spatial variable parameters through a data file.</td></tr><tr><td>COUPL</td><td>Options and parameters for TOUGH4 and third-party software coupling simulation</td></tr><tr><td>FLAC</td><td>Introduces material parameters and coupling options for coupling with FLAC3D</td></tr><tr><td>FORCH</td><td>Introduces parameters on non-Darcy flow coefficient model and weighting scheme using Forchheimer equation</td></tr><tr><td>CBMDA</td><td>Input parameters for simulation of gas/tracer absorption (such as coalbed methane) using the  extended Langmuir isotherm</td></tr><tr><td>ENDCY</td><td>Last record to close the TOUGH3 input file and initiate the simulation</td></tr><tr><td>ENDFI</td><td>Alternative to ENDCY for closing a TOUGH3 input file; will cause flow simulation to be skipped; useful if only mesh generation is desired</td></tr></tbody></table>

\* [_These blocks can be provided on separate files, in which case they would be omitted from the INPUT file._](#user-content-fn-1)[^1]

#### 2- Flexible file formatting

TOUGH4 allows flexible formatting for the input files. The input can be in free format or in a file format that is fully backward compatible with the format of TOUGH3. It automatically recognizes the format of TOUGH3 or the new free format.&#x20;

#### 3- Free formatting

TOUGH4 allows the input data in free format with comma or semicolon as a “separator”. For example, inputs using the two formats as shown in Figure 25 are equivalent for TOUGH4.

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption><p>Figure 25. Formats for the input of TOUGH4</p></figcaption></figure>

Users can use the old format or new style for different lines in the same input file. TOUGH4 will automatically identify the text lines with new style input. The TOUGH4 also allows input of the TOUGH3 multiple line inputs for a parameter series in one line (as more as 20 data). The two formats shown in Figure 26 are equivalent for TOUGH4.&#x20;

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption><p>Figure 26. The two formats are equivalent for the TOUGH4</p></figcaption></figure>

#### 4- (New feature) Entering comments in the input file

In the input file, the “//” or “!” can be placed at any locations for indicating the starting of comments. The comments are for information only and neglected by the program.&#x20;

#### 5- (New feature) Multiple identical adjacent entry

Another new feature for TOUGH4 input is _x\*n_ representing repeat input x (must be integer or real/double datum) _n_ times, e.g. the last row of the input in Figure 26 can also be written as:&#x20;

0.1000960052269E+6, 0.0\*3, 0.105E+02, 0.15E+02

#### 6- Units

All TOUGH4 input is in standard metric (SI) units, such as meters, seconds, kilograms, ˚C, and the corresponding derived units, such as Newtons, Joules, and Pascal (= N/m2).

#### 7- Backward compatibility

For most case, the input file of TOUGH3 can be directly used. In some modules the sequence of mass components may not be consistent in both versions, e.g. CO2 is COM3 in TOUGH3/ECO2N, but it is COM2 in TOUGH4/ECO2. The inconsistency requires the modification of input for keyword GENER. &#x20;

#### _8-_ Obsolete keywords

Keyword START and MULTI which are used in TOUGH3 become obsolete. MULTI may still require only when NKIN ≠ NK. It must appear before MODDE.&#x20;

#### _9-_ Compatibility with TOUGH+

In consistent with TOUGH+, some keywords can be replaced with other words, including ROCKS (MEDIA), MESHM (meshm, Meshm), START (RANDO), FOFT (Elem\_, FOFT\_, foft, foft\_), GOFT (SS\_Ti, GOFT\_, goft, goft\_), COFT (conx\_, COFT\_, coft, coft\_), and ROFT (ROFT\_).

[^1]: 
