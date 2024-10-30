# FLAC

To run a coupled TOUGH-FLAC simulation, a data block FLAC (or [COUPL](coupl.md)) must be introduced and present in the main input file. The block FLAC introduces material parameters and coupling options. It must be specified after the block ROCKS and contain two records for each rock type in the same order as in the block ROCKS, plus an additional record placed after the line containing the keyword FLAC.

**FLAC**           Introduces material parameters and coupling options for TOUGH-FLAC3D coupling simulation

Record **FLAC.1**

&#x20;                   Free format for 3 parameters, or Format(3I5).

&#x20;                   IE\_THM(I), I=1,3

_IE\_THM(1)_     Select creep mode (not implemented yet).

&#x20;                 0:                 default mode

&#x20;                  1:                  creep mode

_IE\_THM(2)_     Select porosity evolution model.

&#x20;                 0:                 no mechanical induced porosity change.

&#x20;                  1:                 mechanical-induced porosity change.

&#x20;                  2:                 porosity change as a function of volumetric strain.

_IE\_THM(3)_     Select FLAC3D version.

&#x20;                 6:                  call FLAC3D v6 from its default location.

&#x20;                  7:                 call FLAC3D v7 from its default location.

&#x20;                  9:                  call FLAC3D v9 from its default location (default).

Record **FLAC.2**

&#x20;                Free format for 8 parameters, or format (I10, 7E10.4)&#x20;

&#x20;                IHM, HM(I), I = 1, 7

IHM                 Select permeability model.

&#x20;                 0:                 permeability models defined in the Python script flac3d.py.

&#x20;                  1:                 no mechanical induced permeability change.

&#x20;                  2:                 Minkoff et al. (2004).

HM(I)             Parameter values for selected permeability model.

Record **FLAC.3**

&#x20;                Free format for 8 parameters, or format (I10, 7E10.4)&#x20;

&#x20;                ICP, CP\_THM(I), I = 1, 7

ICP                 Select equivalent pore pressure model (Coussy, 2004).

&#x20;                  3:                 Integral term is zero.

CP\_THM(I)     Parameter values for the model.

The input for data block "FLAC" can also through "[COUPL](coupl.md)", a keyword for third-party software coupling input.&#x20;

**Used in**: All EOS modules

**Example**:

FLAC              //An example of block FLAC for an input file with three different rock types

0, 1, 7

1, 0.0\*7

3, 0.0\*7

1, 0.0\*7

3, 0.0\*7

1, 0.0\*7

3, 0.0\*7
