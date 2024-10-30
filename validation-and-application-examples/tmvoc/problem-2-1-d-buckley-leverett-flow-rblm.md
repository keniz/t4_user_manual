# Problem 2-1-D Buckley-Leverett Flow (rblm)

The sample problem no. 2 of TOUGH3/TMVOC  (rblm) was run with TOUGH4.  The 1D model consists of a row of  41 elements with a total length of 304.8 m. The flow system is initialized in two-phase water-NAPL conditions, with a water saturation of 15.9% so that NAPL (chlorobenzene) saturation is 84.1 %.  The model has a first type boundary at one end  and injects water with a constant rate at the another end of the row. Slight modification to the input file of TOUGH3 is needed for TOUGH4 simulation. Modification includes  adding the data section "MODDE" which is used for define the model.&#x20;

An NCGAS data block with a single non-condensible gas (AIR) was included, although this is not required in this case because the choices made in NCGAS are TMVOC defaults. The results agree very closely with those from TOUGH3 simulation.

**Input Files:**                 [INFILE](https://drive.google.com/file/d/1DTD1stA1lhPYH0vAc0hjLntZhz8-vKlW/view?usp=sharing)

**Output Files:**            [output files](https://drive.google.com/file/d/1S3HOpvlfEfW1Fc6C8BoXsV82gXhIsH20/view?usp=sharing)
