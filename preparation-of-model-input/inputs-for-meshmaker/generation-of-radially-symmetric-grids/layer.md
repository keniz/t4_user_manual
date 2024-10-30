# LAYER

**LAYER**            introduces information on horizontal layers, and signals closure of RZ2D input data.

Record **LAYER. l**    &#x20;

&#x20;                       Free format for 1 parameter or Format (I5)

&#x20;                       NLAY

NLAY              number of horizontal grid layers.

Record **LAYER.2**                 &#x20;

&#x20;                       Free format for as more as 20 parameters or Format (8E10.4)

&#x20;                       H(I), I = 1, NLAY

H(I)                   a set of layer thicknesses, from top layer downward. Zero or blank entries for layer thickness will be neglected. Assignment of a zero layer thickness, as needed for inactive layers, can be accomplished by specifying a negative value. If more than 20 layers, input can be in multiple line.

The LAYER data close the RZ2D data block. Note that one blank record must follow to indicate termination of the MESHM data block. Alternatively, keyword MINC can appear to invoke MINC-processing for fractured media (see [below](../minc-processing-for-fractured-media.md)).

**Example:**

_LAYER_

_25_

_1.0\*3, 2.0\*6_

&#x20;_5.0\*15, -1.0_       &#x20;

&#x20;_// total 25 layers, 1.0 m for the first three layer, 2.0 m for the next 6 layers,_&#x20;

_//  5.0 m for layers 10-24,  and 0 m for the last layer._
