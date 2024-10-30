# Problem 9-Non-Isothermal Compressed Air Energy Storage in Reservoir (by Julien Mouli-Castillo)

This example is contributed by **Dr. Julien Mouli-Castillo,**  Ph.D.- MSCA Fellow Affiliated to LBNL , using TOUGH4 build No.: 2405141S.

## Conceptual Model

The conceptual model is based on a compressed air energy storage (CAES) system within a porous media reservoir. The simulation setup is inspired by the study conducted by Curtis M. Oldenburg and Lehua Pan, detailed in their publication "Porous Media Compressed-Air Energy Storage (PM-CAES): Theory and Simulation of the Coupled Wellbore–Reservoir System" (March 2013, Transport in Porous Media, DOI: 10.1007/s11242-012-0118-6).\
\
The model geometry is represented by a dome with radial symmetry along the well axis. The attached screenshot illustrates the geometry with a horizontal scaling compression factor of 5 (Figure 10-2).

## Geometry and Properties

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Figure 10-2: Geometry of the system, boundary conditions and initial gas saturation. The well screen is indicated by the blue rectangle. The zoom-in provides details of the well elements. The well elements are 1m thick and 0.26 m wide.</p></figcaption></figure>

The model simulates a reservoir with specific properties outlined in Table 10-2.

&#x20;         _Table 10-2 Reservoir properties_

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## Initial Conditions

The initial state of the reservoir features a gas cap positioned above a water leg in gravity–capillary equilibrium. This configuration was chosen to avoid the complexities of simulating the formation of the initial gas bubble during the start-up phase of a CAES project and to differentiate the long-term steady-state behavior of the PM-CAES system from transient bubble formation dynamics.

The pressure at the top of the dome is 7.2 × 10⁶ Pa, with gas-static conditions in the gas cap and hydrostatic conditions in the water leg. The initial temperature, based on a geothermal gradient of 33°C/km, is 32.66°C at a depth of 720 m. The initial saturation levels reflect a gravity–capillary equilibrium, with the gas–water contact at a depth of -60 m.

&#x20;          _Table 10-3 Initial Conditions_

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

## Well Properties

The well is 720 m long with a diameter of 0.52 m, with a well screen length of 30 m in the top of the dome down to 20 m from the base of the reservoir. Only the screened portion of the well is modelled. It is represented by elements 1 m thick and 0.26 m wide. The permeability of the well elements is $$1.0 \times 10^{-11}$$ (an order of magnitude more permeable than the reservoir to minimize the pressure effects from these elements).

## Operational Cycle

The energy storage process is modeled by specifying a mass and enthalpy source term for a 12-hour storage period at each well element. The total mass rates provided in Table 10-4 are divided by the number of well elements (i.e. 30) the resulting weighted mass rates are applied (note: all well elements have the same volume). During CAES operation, a mixture of pseudocomponent air and water vapor, corresponding to humid air at 50°C, is injected. Energy recovery is simulated through a 3-hour daily production phase, with mass produced at the well elements. The 4.5-hour shut-in periods are modeled by setting the injection and production rates at the well elements to zero.

&#x20;         _Table 10-4 Operation Cycle of the Prototypical PM-CAES System_

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## Boundary Conditions

The top and bottom boundaries of the reservoir are closed to heat and mass flow. The down-dip right-hand side is set to a constant hydrostatic pressure, assuming a water density of 1000 kg/m³, and a temperature corresponding to the geothermal gradient specified in the initial conditions. The open boundary is simulated by setting the volume and specific heat capacity of the boundary elements to large values: $$1\times10^{50}$$m³ and $$2 \times 10^4$$J/(kg·K), respectively.

## Simulation Results

The simulation covers three cycles of the operational process, capturing the dynamic behavior of the CAES system within the porous media reservoir.

The results show that the first cycle differs significantly from the subsequent ones. This can be attributed to the first production phase producing directly from the initial conditions which represent an equilibrium between the gas phase and water in the reservoir, whilst also being at reservoir temperatures, which is unlikely to be present as the cushion gas would have been injected over days or weeks prior to the start of the cycling.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Figure 10-2 Simulated pressure and temperature changes with time at different locations</p></figcaption></figure>

_<mark style="color:green;">**Note**</mark><mark style="color:green;">: ChatGPT-4o  was used to generate the figure using the data.csv provided. The output was verified by the author. Use was also made to improve the legibility of the text and the formatting of the document.</mark>_

**Input Files:**          [inputFiles.zip](https://drive.google.com/file/d/10\_UAH30Fs6XMkCju6Kp-cCKgW6kw87j3/view?usp=sharing)

**Output Files:**      [outputFiles.zip](https://drive.google.com/file/d/1bJDwgRx8Q-6SzAeW2L511URj3qHGmW0z/view?usp=sharing)
