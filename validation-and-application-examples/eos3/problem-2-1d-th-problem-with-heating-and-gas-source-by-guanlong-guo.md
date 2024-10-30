---
description: >-
  This example is contributed by Dr. Guanlong Guo,  Energy Geosciences Division
  , LBNL , using TOUGH4 build No.: 2407301S
---

# Problem 2 - 1D TH Problem with Heating and Gas Source (by Guanlong Guo)

In this section, a 1D coupled TH problem with heating and gas source is simulated using TOUGH4. Figure 10-3 presents the geometry and boundary conditions of the coupled THM problem. The gas pressure, liquid saturation and temperature at the right boundary is 4MPa, 1.0 and 25 °C, respectively. The initial total stress and initial temperature are 8MPa and 25 °C, respectively, in the whole domain. The initial pore gas pressure is 0.1013 MPa and 4MPa for canister and host rock, respectively. The initial liquid saturation is 0.75 and 1.0 for canister and host rock, respectively. A time-dependent heating power is applied in the canister, which is expressed as:

$$
Q\left(t\right)=\left\{\begin{matrix}160-0.16t,\ \ \ t<1000a\\0,\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ t\geq1000a\ \\\end{matrix}\right.
$$

where  is the power per meter (W/m) in the canister.

A time-dependent gas source is applied to the canister, which is expressed as:

$$
Q_g\left(t\right)=\left\{\begin{matrix}0,t<5000a\ or\ t>15000a\\2\times{10}^{-13}\left(t-5000\right),5000a\le t\le10000a\\-2\times{10}^{-13}\left(t-15000\right),10000a<t\le15000a\\\end{matrix}\right.
$$

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption><p>Figure 10-3 1D geometry and boundary conditions</p></figcaption></figure>

Table 10-3 presents the material properties for the 1D coupled TH problem.

&#x20;

_Table 10-3 Material properties for the 1D TH problem_

<table data-header-hidden><thead><tr><th width="369"></th><th></th><th></th></tr></thead><tbody><tr><td> </td><td>Canister</td><td>Host rock</td></tr><tr><td>porosity</td><td>0.37</td><td>0.17</td></tr><tr><td>intrinsic permeability [ <span class="math">m^2</span>]</td><td><span class="math">1.75 \times 10^{-18}</span></td><td><span class="math">1.0 \times 10^{-20}</span></td></tr><tr><td>Residual liquid saturation</td><td>0.03</td><td>0.16</td></tr><tr><td>van Genuchten parameter, <em>m</em></td><td>0.5</td><td>0.28</td></tr><tr><td>Gas entry value, [ <em>MPa</em>]</td><td>0.12</td><td>30</td></tr><tr><td>Pore connectivity, <span class="math">\gamma</span></td><td>0.5</td><td>0.5</td></tr><tr><td>Grain thermal conductivity [ <span class="math">W/\left(m\ast K\right)</span>]</td><td>11.57</td><td>2.3</td></tr><tr><td>Specific heat capacity [ <span class="math">J/\left(kg\ast K\right)</span>]</td><td>830</td><td>900</td></tr><tr><td>Density [ <span class="math">kg/m^3</span> ]</td><td>3450</td><td>2700</td></tr><tr><td>Thermal expansion coefficient [ <span class="math">K^{-1}</span>]</td><td><span class="math">1.77 \times 10^{-5}</span></td><td><span class="math">1.08 \times 10 ^{-6}</span></td></tr></tbody></table>

The monitoring points are located at 0m, 15m, 21m and 30m from the left boundary.

Figure 10-4 presents the comparisons of temperature, gas pressure and degree of saturation obtained from EOS3 of TOUGH3 and TOUGH4. The numerical results from TOUGH4 are in good agreement with those in TOUGH3. As seen from the curve for gas pressure, the curve from TOUGH4 is smoother than that from TOUGH3, which is attributed to a more robust time stepping algorithm used in TOUGH4.

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption><p>Figure 10-4 Comparisons of temperature, gas pressure and saturation obtained from TOUGH4 and TOUGH3</p></figcaption></figure>



[**Input Files**](https://drive.google.com/file/d/1PMZ4dntPuMmwakHGBUPfb2ReJFc8lJJZ/view?usp=sharing)

[**Output Files**](https://drive.google.com/file/d/1j-V2tBnewYqrVebB7i9w3hsalJH\_1Vbj/view?usp=sharing)
