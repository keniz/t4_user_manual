# ICP=41 User-Defined capillary pressure function

Users may use a capillary pressure function defined by themselves without touching the TOUGH4 source codes. The input parameters are the same as other functions through variables &#x43;_&#x50;(1)-CP(13)_ of data record [**ROCKS.1.3** and **ROCKS.1.3.1**](../../preparation-of-model-input/keywords-and-input-data/rocks.md)**.** The function must be defined in the PYTHON file: TOUGH\_python\_module.py.  A function named CapiFunction() is already included in the the PYTHON file. Users need to modify this function to their own function.   Following is the template of the function:

_**def CapiFunction(double\_array, int\_array):**_

&#x20;     _**capiP = np.zeros(3, dtype='float64')**_&#x20;

&#x20;     _**CapiParam=np.zeros(13, dtype='float64')**_&#x20;

&#x20;     _**sg=double\_array\[13]                         #gas saturation**_&#x20;

&#x20;      _**sl=double\_array\[14]                         #liquid saturation**_&#x20;

&#x20;      _**nph=int\_array\[6]                              # phase number: 2 phase or 3 phase**_&#x20;

&#x20;      _**nmat=int\_array\[7]                            # rock index defined in tough4 input**_

&#x20;      _**for i in range(0,13):**_&#x20;

&#x20;            _**CapiParam\[i]=double\_array\[i]**_   &#x20;

_**#capillary pressure calculation parameters: CapiParam\[0-12], input through record ROCKS.1.3**_

_**#performcapillary pressure calculations at following lines:**_

_**#results of capillary pressures stored in capiP\[0]:**_**&#x20;:gas/aqu; capiP\[2]:gas/oil**

&#x20;     _**return capiP**_

During runtime, the  PYTHON file must be stored at the same location where TOUGH4 executable is located.
