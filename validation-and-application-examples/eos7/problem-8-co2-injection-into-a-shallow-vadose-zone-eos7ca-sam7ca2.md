# Problem 8-CO2 Injection into a Shallow Vadose Zone (EOS7CA/SAM7CA2)

This test problem is originally present in TOUGH3/EOS7CA user manual. It is prototypical of the kinds of injection and migration problems that TOUGH3/EOS7CA was designed to handle. TOUGH4/EOS7 uses completely different gas solubility model which can handle much higher pressure and temperature simulations compared to  TOUGH3/EOS7CA. We use this example to test EOS7 simulation for such problem.&#x20;

The problem consists of a shallow vadose zone with a water table at a depth of approximately 3 m. We assume there is a horizontal injection well at a depth of approximately 2.4 m, and that the well is long enough that the flow domain can be approximated as a two-dimensional (2D) Cartesian slice transverse (perpendicular) to the well. This test problem is designed to model field experiments aimed at studying how CO2 will flow and migrate within the shallow subsurface following its arrival from a deep leaking geologic carbon sequestration site through a leakage pathway such as an abandoned well, fault, or fracture zone (e.g., Oldenburg et al., 2010a). Table 10-7 provides properties of the system.

&#x20;                         Table 10-7 Properties of the homogeneous vadose zone

<figure><img src="../../.gitbook/assets/image (69).png" alt="" width="560"><figcaption></figcaption></figure>

Files containing the inputs and simulation outputs can be downloaded from following html links. Discussion of the modeling results can be found in TOUGH3/EOS7CA user manual. Slight different results may be observed due to the difference in gas solubility model for the two codes. &#x20;

**Input Files:**                 [sam7ca2.zip](https://drive.google.com/file/d/1K-V6wROcfEpdL8lGLuExZ4frGQq7pU5r/view?usp=sharing)&#x20;

**Output Files:**                [output\_sam7ca2.zip](https://drive.google.com/file/d/1nBn5d2Q4Gc\_g0Puizi9J4Pbn7VoeVnPY/view?usp=sharing)
