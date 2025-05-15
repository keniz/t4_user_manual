# Problem 1-Steady-state two-phase flow upward

This problem is from the first example in the user manual of T2Well/ECO2N Version 1.0. It was designed for verifying the wellbore flow solution approach through modeling the steady-state, isothermal, two-phase (CO2 as gas and water as liquid) flow in a vertical wellbore of 1000 m length.&#x20;

The details of the problem are described below:

_Table 10-2 Parameters of the example problem_

<table><thead><tr><th width="191">Parameters</th><th>Value</th><th>Remarks</th></tr></thead><tbody><tr><td>Length</td><td>1000 <em>m</em></td><td>Vertical wellbore</td></tr><tr><td>Diameter</td><td>0.1 <em>m</em></td><td>Circular</td></tr><tr><td>Total mass flux</td><td>50  <span class="math">kg/m^2/s</span></td><td>Gas+Liquid</td></tr><tr><td>Gas mass fraction</td><td>0.5</td><td></td></tr><tr><td>Temperature</td><td>40.0 <em>˚C</em></td><td>Isothermal</td></tr><tr><td>Wellhead pressure</td><td>100000 <em>Pa</em></td><td></td></tr></tbody></table>

The specifications of the one-dimensional model are:

1. 1000 m wellbore with a diameter of 0.1 m.
2. Grid resolution 10 m.
3. Injection mass rate at bottom: CO2: 0.19625 _kg/s_; water: 0.19625 _kg/s_ (Each = 25  with a cross sectional area of 7.8500E-03 $$m^2$$).
4. Isothermal simulation with a uniform temperature of 40 °C throughout the wellbore.
5. Top boundary (outlet) pressure is 10000.0 Pa.
6. Wall roughness $$2.4e^{-5}$$ _m_.
7. Use ECO2 module for the simulation.

The input  file for TOUGH4 simulation is modified from the input of T2well. Figure 10-n shows the main changes in the file, including two new data sections ([MODDE](../../preparation-of-model-input/keywords-and-input-data/modde.md) and [WELLB](../../preparation-of-model-input/keywords-and-input-data/wellb.md)). The option IE(52)=-1 forces using change of the primary variables as convergence criteria  for Newton iteration , which is very helpful in improving model convergence behavior. T2Well reached steady-state requires  4100 steps for this example, but T4Well needs only 174 steps to obtain the same results.    IE(67)=1 is for selecting the same function as in T2Well/ECO2N Version 1.0  for the calculation of the acceleration loss.&#x20;

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Figure 10-n TOUGH4 inputs for wellbore simulation</p></figcaption></figure>

The results from TOUGH4 numerical solution are almost identical to the analytical solutions (Pan et al., 2010) and the results from T2Well. Figure 10-m shows the comparison of simulated pressure, drift velocity, gas velocity and gas saturation along the wellbore at steady-sate by T2well and T4.well.&#x20;

<figure><img src="../../.gitbook/assets/image (81).png" alt="" width="563"><figcaption><p>Figure 10-m Comparison of simulation results. </p></figcaption></figure>

**Input Files:**                 [INFILE](https://drive.google.com/file/d/1YhAEWy_3j9hWuRzFeiJwJfygNYNUOLQV/view?usp=sharing)

**Output Files:**            [output files](https://drive.google.com/file/d/1lG3IOndwdUHPCzC94F1HGic4x2sbWYtp/view?usp=sharing)
