# IRP=41 User-Defined relative permeability function

Users may use a relative permeability function defined by themselves without touching the TOUGH4 source codes. The input parameters are the same as other functions through variables _RP(1)-RP(10)_ of data record [**ROCKS.1.2** and **ROCKS.1.2.1**](../../preparation-of-model-input/keywords-and-input-data/rocks.md)**.** The function must be defined in the PYTHON file: TOUGH\_python\_module.py.  A function named RelpFunction() is already included in the the PYTHON file. Users need to modify this function to their own function.   Following is the template of the function:

_**def RelpFunction(double\_array, int\_array):**_&#x20;

&#x20;      _**relpm = np.zeros(3, dtype='float64')**_&#x20;

&#x20;      _**RelpParam=np.zeros(10, dtype='float64')**_&#x20;

&#x20;      _**sg=double\_array\[13]                   # gas saturation**_&#x20;

&#x20;      _**sl=double\_array\[14]                    # liquid saturation**_&#x20;

&#x20;      _**nph=int\_array\[6]                         # phase number, 2 phase or 3 phase**_&#x20;

&#x20;      _**nmat=int\_array\[7]                      # rock index defined in tough4 input**_\
&#x20;      _**for i in range(0,10):**_&#x20;

&#x20;            _**RelpParam\[i]=double\_array\[i]**_    &#x20;

_**#perform relative permeability calculations at following lines:**_

_**#results of relative permeabilities stored in relpm\[0]:**_

_**#gas phase; relpm\[1]:aqueous phase; relpm(2): oil phase**_

&#x20;     _**return relpm**_

During runtime, the  PYTHON file must be stored at the same location where TOUGH4 executable is located.
