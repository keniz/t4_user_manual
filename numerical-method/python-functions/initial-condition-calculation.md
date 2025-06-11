# Initial Condition Calculation

A Python function named "iniCondition" is provided. This function will receive primary variables, x, y, z coordinates, material number  and phase state index for all elements from TOUGH4. Users can manipulate the primary variables for initial conditions, such as setting initial condition for pressure and temperature according to element's z coordinate, gravity equilibrium and temperature gradient, setting initial condition for fluid saturations or mass fractions based on the rock number or coordinates, or any other assignment to the primary variables.  The updated primary variables will be sent back to TOUGH4.   TOUGH4 will write the updated primary variables to a SAVE file which can be used as initial condition for further simulation. User may also change the phase state index which will also be sent back TOUGH4.

In many simulations, model has an initial condition of pressure distribution with gravity equilibrium and temperature distribution with given temperature gradients. For such a case, the pressure and temperature at any elements can be estimated from the pressure and temperature at reference level together with the z coordinate (elevation), fluid density and geothermal temperature gradients. User can perform the initial pressure and temperature calculation through a Python function at run-time (see iniCondition in TOUGH\_python\_module.py). Other primary variables can also be assigned values in the Python function. User may use this function to generate a INCON file by running a simulation for a single time step with tiny time-step size (e.g. 1.0e-6 second). See [IE(69)](https://lbl-2.gitbook.io/tough4-user-manual/appendix/c-additional-program-options) for further details.  &#x20;

In many simulations, model has an initial condition of pressure distribution with gravity equilibrium and temperature distribution with given temperature gradients. For such a case, the pressure and temperature at any elements can be estimated from the pressure and temperature at reference level together with the z coordinate (elevation), fluid density and geothermal temperature gradients. User can perform the initial pressure and temperature calculation through a Python function at run-time (see iniCondition in TOUGH\_python\_module.py). Other primary variables can also be assigned values in the Python function. User may use this function to generate an initial INCON file by running a simulation for a single time step with tiny time-step size (e.g. 1.0e-6 second).   &#x20;

Here is a template for the `iniCondition` function that you can modify to suit your specific initial condition requirements:

```python
def iniCondition(double_array, int_array):
# start getting data section, user does not need change to this section
    nPrv=int_array[4]          #this is the number of primary variables
    numElem=int_array[6]       #number of elements
    HEAT=int_array[7]-1        # the index of temperature in the PV list
    xk= np.zeros((numElem, nPrv), dtype='float64')    # original primary variables 
    xx= np.zeros(numElem*(nPrv+1), dtype='float64')   # final primary variables
    x= np.zeros(numElem, dtype='float64')             # x coordinates   
    y= np.zeros(numElem, dtype='float64')             # y coordinates
    z= np.zeros(numElem, dtype='float64')             # z coordinates
    nMat=np.zeros(numElem, dtype=int)                 # rock index of the elements       
    stateIdx=np.zeros(numElem, dtype=int)             # phase state index 
    for i in range(0,nPrv):
       nE=i*numElem
       for j in range(0,numElem): 
          xk[j,i]=double_array[nE+j]       # get original initial-condition PV variables.
    nE=nPrv*numElem      
    for i in range(0,numElem):
          x[i]= double_array[nE+i]         # get x coordinates
    nE=nE+numElem      
    for i in range(0,numElem):
          y[i]= double_array[nE+i]         # get y coordinates
    nE=nE+numElem      
    for i in range(0,numElem):
          z[i]= double_array[nE+i]         # get z coordinates
    for i in range(0,numElem):
       nMat[i]= int_array[i+10]              # get rock of the elements.
    for i in range(0,numElem):
       stateIdx[i]= int_array[i+10+numElem]  # get initial phase state index
# end getting data section
# users need to define the reference temperature and pressure:
    refZ=0                    
    refT=35.0
    refP=5.0e6
    density=1000.0
    g=9.81
    T_gradient=35.0   # temperature gradient 35C/km           
# perform calculation of xk (PV for initial condition) at following lines: 
# for example, pressure: if gravity equilibrium, xk=P_ref+density*g*h      
#           temperature: geothermal temperature graditent is known: xk(HEAT)=T_ref-h*T_gradient
# User can assign the the primary variables based on knowns: such as: x, y, z, nMat
    for i in range(0,numElem):
       xk[i,0]=refP+(z[i]-refZ)*density*g
#       xk[i,1]=0.000
#       xk[i,2]=0.000
       xk[i,HEAT]=refT+(z[i]-refZ)/1000.0*T_gradient
#       stateIdx[i]=2                      #Users can also change the phase state if necessary
  
#start assembling data section, user does not need change to this section 
    for i in range(0,nPrv):
       nE=i*numElem
       for j in range(0,numElem): 
          xx[nE+j] =xk[j,i]   
    nE=	nPrv*numElem  
    for j in range(0,numElem):
       xx[nE+j] = stateIdx[j]
# assembling data section
    return xx 
```

In this template, the `iniCondition` function takes lists of coordinates, material numbers, and phase states for each element. You can customize the calculations for pressure, temperature, saturation, and mass fractions based on the provided parameters to create initial conditions suited for your simulation.
