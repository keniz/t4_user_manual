# Problem 1-Initialization of Different Phase Conditions (r7c)

This example is the Sample Problem 1 (r7c) in the TMVOC user manual. It demonstrates the initialization of different phase conditions using TMVOC. A single infinitesimal time step of 1.e-9 s is specified, and no flow simulation is carried out.

Users should note that properly initializing multiphase multicomponent systems can be challenging due to several simultaneous thermodynamic constraints. It is envisioned that 2 or 3-phase conditions including a NAPL will rarely be initialized directly. Instead, a flow simulation will typically start from single-phase water (saturated zone) or two-phase water-gas conditions (unsaturated zone) without any VOCs present. VOC distributions and the possible evolution of a NAPL phase would then be computed using appropriate injection specifications to simulate a contamination event.

The model includes two hydrocarbon components (BENZENE and n-DECANE) and one gas component (AIR, by default). Users can refer to the input files for details on the model setup and initial conditions for each element. The main input file (INFILE) was modified from the original input file of r7c by adding the data section "MODDE".

Current model results match the corresponding results by TOUGH3 very well, except for the air mole fraction in the aqueous phase. Differences in calculated air mole fractions are due to the use of different air solubility models. TOUGH4 uses a more accurate model for air solubility calculation in water. Users may specify IE(402)=1 to force the use of the same air solubility model as TOUGH3 and achieve the same simulation results.

**Input Files:**                 [INFILE](https://drive.google.com/file/d/1f6YK5G1OPx--k3wxUjMe2eO-tc7Qkotj/view?usp=sharing)

**Output Files:**            [output files](https://drive.google.com/file/d/1AQQyh-QX3FKH5jLsqUbUIjUkOIp6-b50/view?usp=sharing)
