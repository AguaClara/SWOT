# Flow Control and Measurement Design Challenge


Researchers in the AguaClara laboratory collected the following head loss data through a 1/8" diameter tube that was 2 m long using water at
22°C. The data is in a comma separated data (.csv) file named [Head_loss_vs_Flow_dosing_tube_data.csv](https://raw.githubusercontent.com/AguaClara/CEE4520/master/DC/data/Head_loss_vs_Flow_dosing_tube_data.csv). Use the pandas read csv function (`pd.read_csv('filename.csv')`) to read the data file. Display the data so you can see how it is formatted.

``` python
import pandas as pd
import numpy as np
from aguaclara.core.units import unit_registry as u
from aguaclara.core import physchem as pc
from aguaclara.core import utility as ut
import matplotlib.pyplot as plt

url = 'https://raw.githubusercontent.com/AguaClara/CEE4520/master/DC/data/Head_loss_vs_Flow_dosing_tube_data.csv'
head_loss_data = pd.read_csv(url)
head_loss_data


```

### 1)
Using the data table above, assign the head loss and flow rate data to separate 1-D arrays. Attach the correct units. `np.array` can extract the data by simply inputting the text string of the column header. Name the array of flow rates `Q_data`. Here is example code to create the first array:

``` python
HL_data=np.array(head_loss_data['Head loss (m)'])*u.m
print('There are',HL_data.size,'elements in this array.')

```



### 2)
Calculate and report the maximum and minimum Reynolds number for this data set. Use the tube and temperature parameters specified above. Use the numpy `min` and `max` functions which take arrays as their inputs.

```python
PipeRough = 0*u.mm
L_tube = 2*u.m
T_data = 22 * u.degC
Nu_data = pc.viscosity_kinematic(T_data)
D_tube = 1/8*u.inch



```

The minimum Reynolds number was 292.0
The maximum Reynolds number was 1030.0


### 3)
You will now create a graph of head loss vs flow for the tube mentioned in the previous problems. This graph will have two sets of data: the real data contained within the csv file and a hydraulic model. The hydraulic model is what we would expect the head loss through the tube to be in an ideal world for any given flow. When calculating the hydraulic model head loss, assume that minor losses are negligible. Plot the data from the csv file as individual data points and the hydraulic model head loss as a continuous curve. Make the y-axis have units of cm and the x-axis have units of mL/s.

A few hints.

- To find the theoretical head loss, you will first need to create an array of different flow values. While you could use the values in the csv file, we would instead like you to create an array of 50 equally-spaced flow values. These values shall be between the minimum and maximum flows in the csv file.
- You can use the `np.linspace(start, stop, num)` function to create this set of equally-spaced flows. Linspace does not work with units; you can make the inputs dimensionless and then multiply the array by a scaling factor with units. `np.linspace(start/stop, 1, num) * stop`
- The `pc.headloss_fric` function currently can not handle arrays as inputs. You can use a for loop. Create an array of zeroes with the correct units using the following code or something similar. `HL = np.zeros(Graph_points) *pc.headloss_fric(Q_array[0], D_tube, L_tube, Nu_data, PipeRough).units` Then you can fill the array with the values in the for loop. I learned that creating the array with the correct units initially eliminates the numpy error of assigning units to each element.
- When using plotting, make sure to convert the flow and head loss data to the desired units that are defined in the axis labels.


### Use the data to estimate the minor losses
The theoretical model doesn't fit the data very well. We assumed that major losses dominated. But that assumption was wrong. So let's try a more sophisticated approach where we fit minor losses to the data. Below we demonstrate the use of the [scipy curve_fit method](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html#scipy.optimize.curve_fit) to fit the minor loss coefficient given this data set. In this example, `Q_data` is the flow rate array for the csv file from problem 13. You should re-name this variable below to whatever you titled this variable.

``` python
from scipy.optimize import curve_fit

# Define a new function that calculates head loss given the flow rate
# and the parameter that we want to use curve fitting to estimate
# Define the other known values inside the function because we won't be passing those parameters to the function.

def HL_curvefit(FlowRate, KMinor):

  # pass all of the parameters to the head loss function and then strip the units so
  # the curve fitting function can handle the data.
  HL_curvefit = np.zeros(FlowRate.size) *pc.headloss_fric(FlowRate[0], D_tube, L_tube, Nu_data, PipeRough).units
  for i in range(FlowRate.size):
      HL_curvefit[i] = pc.headloss(FlowRate[i], D_tube, L_tube, Nu_data, PipeRough, KMinor)
  return HL_curvefit.magnitude


# The curve fit function will need bounds on the unknown parameters to find a real solution.
# The bounds for K minor are 0 and 20.

# The curve fit function returns a list that includes the optimal parameters and the covariance.

popt, pcov = curve_fit(HL_curvefit, Q_data, HL_data, bounds=[[0.],[20]])

K_minor_fit = popt[0]
print('The best fit minor loss coefficient is',ut.round_sf(K_minor_fit,2))


# Plot the raw data
plt.plot(Q_data.to(u.mL/u.s), HL_data.to(u.cm), 'o', label='data')

# Plot the curve fit equation.
plt.plot(Q_data.to(u.mL/u.s), ((HL_curvefit(Q_data, *popt))*u.m).to(u.cm), 'r-', label='fit')
plt.xlabel('Flow rate (mL/s)')
plt.ylabel('Head loss (cm)')
plt.legend()
plt.show()

#Calculate the root mean square error to estimate the goodness of fit of the model to the data
RMSE_Kminor = (np.sqrt(np.var(np.subtract((HL_curvefit(Q_data, *popt)),HL_data.magnitude)))*u.m).to(u.cm)
print('The root mean square error for the model fit when adjusting the minor loss coefficient was',ut.round_sf(RMSE_Kminor,2))
```

The root mean square error for the model fit when adjusting the minor loss coefficient was 0.39 cm

### 4)
Repeat the analysis above, but this time assume that the minor loss coefficient is zero and that diameter is the unknown parameter. The bounds specified in the line beginning with `popt, pcov` should be changed from the previous question (which had bounds from 0 to 20) to the new bounds of 0.001 to 0.01.

Hint: You only need to change the name of the defined function (perhaps "`HL_curvefit2`"?) and adjust its inputs/values.

The root mean square error for the model fit when adjusting the diameter was 0.47 cm

### 5)
Changes to which of the two parameters, minor loss coefficient or tube diameter, results in a better fit to the data?

### 6)
Create a design for a [chemical dose controller using aguaclara](https://github.com/AguaClara/aguaclara/blob/master/aguaclara/design/cdc.py).  Use the AguaClara cdc functions to obtain the diameter, length, and number of dosing tubes that are required. Then take that design and use the physchem functions for flow in a pipe to calculate the maximum coagulant dose that it will deliver. This design and check is a powerful tool to ensure that you don't make mistakes because the design and the check are done using different code.

I've included the code necessary to get the length of the dosing tubes. Note that we are currently specifying the diameter of the dosing tubes to be 1/8".

``` python
from aguaclara.core.units import unit_registry as u
from aguaclara.design import cdc as cdc
from aguaclara.core import physchem as pc
import numpy as np
FlowPlant = 60 * u.L/u.s
ConcDoseMax = 20 * u.mg/u.L
ConcStock = 60 * u.g/u.L
DiamTubeAvail = np.array([1/8]) * u.inch
HeadlossCDC = 20 * u.cm
LenCDCTubeMax = 6* u.m
temp = 20 * u.degC
# 1 is for PACl
en_chem =  1
KMinor = 2

L_tube = cdc.len_cdc_tube(FlowPlant, ConcDoseMax, ConcStock, DiamTubeAvail, HeadlossCDC, LenCDCTubeMax, temp, en_chem, KMinor)
print('The length of the dosing tube is', ut.round_sf(L_tube,2))

```

### 7)
An AguaClara plant will be upgraded from 20 L/s to 30 L/s by adding two sedimentation tanks, increasing the head loss through the flocculator, and adding an additional StaRS filter. Give the current design specs for the CDC. Propose a simple modification to the CDC to handle the additional flow.

### 8)
The LFOM for the 20 L/s plant was designed to have a safety factor of 1.2 and the entrance tank water level changes by 20 cm as the flow goes from zero to 20 L/s. The LFOM for this design is an 8 inch SDR 26 pipe.
Determine if the LFOM diameter will need to be increased to handle a flow of 30 L/s.
```python
import aguaclara.design.lfom as lfom
mylfom = lfom.LFOM(safety_factor=1.2)
mylfom = lfom.LFOM(20 * u.L/u.s,safety_factor=1.2)
mylfom.nom_diam_pipe

```
The LFOM for the 20 L/s plant has a diameter of 8 inches.


### 9)
Could you use the original LFOM diameter by increasing the depth of the entrance tank by 10 or 20 cm? The new LFOM depth range would then be either 30 or 40 cm.
