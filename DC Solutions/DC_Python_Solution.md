
```python
#Here we import packages that we will need for this assignment. You can find out about these packages in the Help menu.
# although math is "built in" it needs to be imported so it's functions can be used.
import math
from scipy import constants, interpolate
#see numpy cheat sheet https://www.dataquest.io/blog/images/cheat-sheets/numpy-cheat-sheet.pdf
#The numpy import is needed because it is renamed here as np.
import numpy as np
#Pandas is used to import data from spreadsheets
import pandas as pd
import matplotlib.pyplot as plt
# sys and os give us access to operating system directory paths and to sys paths.
import sys, os
from aide_design import physchem as pc
from aide_design import pipedatabase as pipe
from aide_design.units import unit_registry as u
from aide_design import utility as ut
```
# Design Challenge 1, learning Python, Atom, and some AguaClara Design Functions

### 1)
Calculate the minimum inner diameter of a PVC pipe that can carry a flow of at least 10 L/s for the town of Ojojona. The population is 4000 people. The water source is a dam with a surface elevation of 1500 m. The pipeline connects the reservoir to the discharge into a distribution tank at an elevation of 1440 m. The pipeline length is 2.5 km. The pipeline is made with PVC pipe with an SDR (standard diameter ratio) of 26.

The pipeline inlet at the dam is a square edge with a minor loss coefficient (${K_e}$) of 0.5. The discharge at the top of the distribution tank results in a loss of all of the kinetic energy and thus the exit minor loss coefficient is 1. See the minor loss equation below.

${h_e} = {K_e}\frac{{{V^2}}}{{2g}}$

The water temperature ranges from 10 to 30 Celsius. The roughness of a PVC pipe is approximately 0.1 mm. Use the fluids functions to calculate the minimum inner pipe diameter to carry this flow from the dam to the distribution tank.

Report the following
* critical design temperature (at what temperature will the design fail?)
* kinematic viscosity (maximum viscosity will occur at the lowest temperature)
* the minimum inner pipe diameter (in mm).
Use complete sentences to report the results and use 2 significant digits (use the ut.sig function).


```python
SDR = 26
Q = 10 * u.L/u.s
delta_elevation = 1500 * u.m - 1440 * u.m
L_pipe = 2.5 * u.km
# am using 0 minor losses because pipe diameter function fails if not zero.
K_minor = 1.5
# The maximum viscosity will occur at the lowest temperature.
T_crit = u.Quantity(10,u.degC)
nu = pc.viscosity_kinematic(T_crit)
e = 0.1 * u.mm
pipeline_ID_min = pc.diam_pipe(Q,delta_elevation,L_pipe,nu,e,K_minor)
print('The critical water temperature for this design is '+ str(T_crit)+'.')
print('The kinematic viscosity of water is '+ut.sig(nu,2)+'.')
print('The minimum pipe inner diameter is '+ ut.sig(pipeline_ID_min.to(u.mm),2)+'.')
```

    The critical water temperature for this design is 10 degC.
    The kinematic viscosity of water is 1.3e-6 m²/s.
    The minimum pipe inner diameter is 97 mm.


### 2)
Find the nominal diameter of a PVC pipe that is SDR 26. SDR means standard diameter ratio. The thickness of the pipe wall is 1/SDR of the outside diameter. The pipedatabase file has a useful function that returns nominal diameter given SDR and inner diameter.  


```python
pipeline_ND = pipe.ND_SDR_available(pipeline_ID_min,SDR)
print('The nominal diameter of the pipeline is '+ut.sig(pipeline_ND,2)+' ('+ut.sig(pipeline_ND.to(u.mm),2)+').')
```

    The nominal diameter of the pipeline is 4.0 in (1.0e+2 mm).


### 3)
What is the actual inner diameter of this pipe in mm? Compare this with the [reported inner diameter for SDR-26 pipe](http://www.cresline.com/pdf/cresline-northwest/pvcpressupipeline_Re/CNWPVC-26.pdf) to see if our pipe database is reporting the correct value.


```python
pipeline_ID = pipe.ID_SDR(pipeline_ND,SDR)
cresline_ID = 4.154*u.inch
print('The inner diameter of the pipe is '+ut.sig(pipeline_ID.to(u.mm),3)+'.')
print('Cresline reports the inner diameter is '+ut.sig(cresline_ID.to(u.mm),3)+'.')
```

    The inner diameter of the pipe is 106 mm.
    Cresline reports the inner diameter is 106 mm.


### 4)
What is the maximum flow rate that can be carried by this pipe at the coldest design temperature?
Display the flow rate in L/s using the .to method.


```python
pipeline_Q_max = pc.flow_pipe(pipeline_ID,delta_elevation,L_pipe,nu,e,K_minor)
print('The maximum flow rate at '+ut.sig(T_crit,2)+' is '+ut.sig(pipeline_Q_max.to(u.L/u.s),2)+'.')
```

    The maximum flow rate at 10 celsius is 13 l/s.


### 5)
What is the Reynolds number and friction factor for this maximum flow? Assign these values to variable names so you can plot them later on the Moody diagram.


```python
pipeline_Re = pc.re_pipe(pipeline_Q_max,pipeline_ID,nu)
fPipe = pc.fric(pipeline_Q_max,pipeline_ID,nu,e)
print('The Reynolds number and friction factor for the pipeline flow are '+ut.sig(pipeline_Re,2)+' and '+ut.sig(fPipe,2)+' respectively.')
```

    The Reynolds number and friction factor for the pipeline flow are 1.2e+5 and 0.022 respectively.


### 6)
Check to see if the fluids functions are internally consistent by calculating the head loss given the flow rate that you calculated and comparing that head loss with the elevation difference. Display enough significant digits to see the difference in the two values. Note that the Moody diagram has an accuracy of about ±5% for smooth pipes and ±10% for rough pipes [Moody, 1944](http://user.engineering.uiowa.edu/~me_160/lecture_notes/MoodyLFpaper1944.pdf).


```python
HLCheck = pc.headloss(pipeline_Q_max,pipeline_ID,L_pipe,nu,e,K_minor)
print('The head loss is '+ut.sig(HLCheck,3)+' and that is close to the elevation difference of '+ut.sig(delta_elevation,3)+'.')
```

    The head loss is 60.5 m and that is close to the elevation difference of 60.0 m.


### 7)
How much more water (both volumetric and mass rate) will flow through the pipe at the maximum water temperature of 30 C? Take into account both the change in viscosity (changes the flow rate) and the change in density (changes the mass rate). Report the flow rates in L/s.


```python
Tmax = u.Quantity(30,u.degC)
nuhot = pc.viscosity_kinematic(Tmax)
pipeline_Q_maxhot = pc.flow_pipe(pipeline_ID,delta_elevation,L_pipe,nuhot,e,K_minor)
QDelta = pipeline_Q_maxhot-pipeline_Q_max
MassFlowDelta = (pipeline_Q_maxhot*DensityWater(Tmax)-pipeline_Q_max*DensityWater(T_crit)).to_base_units()
print('The increase in flow rate at '+ut.sig(Tmax,2)+' is '+ut.sig(QDelta.to(u.L/u.s),2)+'.')
print('The increase in mass rate at '+ut.sig(Tmax,2)+' is '+ut.sig(MassFlowDelta,2)+'.')
```

    The increase in flow rate at 30 celsius is 0.24 l/s.
    The increase in mass rate at 30 celsius is 0.19 kg/s.


### 8)
Why is the flow increase due to this temperature change so small given that viscosity actually changed significantly (see the calculation below)?


```python
print('The viscosity ratio for the two temperatures was '+ut.sig(pc.viscosity_kinematic(Tmax)/pc.viscosity_kinematic(T_crit),2)+'.')
```

    The viscosity ratio for the two temperatures was 0.62.


The flow is turbulent and thus viscosity has little influence on the flow rate.

### 9)
Suppose an AguaClara plant is designed to be built up the hill from the distribution tank. The  transmission line will need to be lengthened by 30 m and the elevation of the inlet to the entrance tank will be 1450 m. The rerouting will also require the addition of 3 elbows with a minor loss coefficient of 0.3 each. What is the new maximum flow from the water source?


```python
delta_elevationnew = 1500*u.m - 1450*u.m
L_pipenew = 2.5*u.km + 30*u.m
Knew = 1.5+3*0.3
pipeline_Q_maxnew = pc.flow_pipe(pipeline_ID,delta_elevationnew,L_pipenew,nu,e,Knew)
print('The new maximum flow rate at '+ut.sig(T_crit,2)+' is '+ut.sig(pipeline_Q_maxnew.to(u.L/u.s),4)+'.')

```

    The new maximum flow rate at 10 celsius is 11.95 l/s.





1.2999268625519206e-06 meter<sup>2</sup>/second



### 10)
How much less water will flow through the transmission line after the line is rerouted?


```python
print('The reduction in flow is '+ut.sig((pipeline_Q_max-pipeline_Q_maxnew).to(u.L/u.s),4)+'.')
```

    The reduction in flow is 1.290 l/s.


### 11)
The next big goal is to create the Moody diagram using the friction factor function. As a first step, modify the friction factor function from that takes the Reynolds number and dimensionless roughness (ε/D) as inputs. You should define the friction function with an if, else statement.


```python
#returns the friction factor for pipe flow for both laminar and turbulent flows
def fofRe(Re,roughness):
    if Re >= pc.RE_TRANSITION_PIPE:
        f = 0.25/(math.log10(roughness/(3.7)+5.74/Re**0.9))**2
    else:
        f = 64/Re
    return f
```

### 12)

Create a beautiful Moody diagram. Include axes labels and show a legend that clearly describes each plot. The result should look like the picture of the graph below.![](Moody.png)

Start by creating a numpy array of Reynolds numbers (note that start and stop are the log10 of 3500 and log10 of 10^8.
logspace(start, stop[, num, endpoint, base, ...])

Include a data point for the Reynolds number and friction factor for the pipeline problem that was calculated above.



```python
eGraph = np.array([0,0.0001,0.0003,0.001,0.003,0.01,0.03,0.1])
Gpoint = 50
ReG = np.logspace(math.log10(3500), 8, Gpoint)
ReLam = np.logspace(math.log10(670),math.log10(2100),Gpoint)
fLam = np.zeros(Gpoint)
for i in range(0,Gpoint):
    fLam[i] = fofRe(ReLam[i],0)
fG = np.zeros((len(eGraph),Gpoint))
for j in range(0,len(eGraph)-1):
    for i in range(0, Gpoint):
        fG[j,i]=fofRe(ReG[i],eGraph[j])

mylegend = np.append(eGraph.astype('str'),[('laminar', 'Pipeline')])  
#Set the size of the figure to make it big!
plt.figure('ax',(10,8))
for i in range(len(fG)):
    plt.plot( ReG,fG[i,:], '-', linewidth = 4)

#fig = plt.figure()  
plt.plot(ReLam,fLam,'k-',linewidth=4)
plt.plot(pipeline_Re,fPipe,'ko')
plt.yscale('log')
plt.xscale('log')
plt.grid(b=True, which='major', color='k', linestyle='-', linewidth=0.5)

#Set the grayscale of the minor gridlines. Note that 1 is white and 0 is black.
plt.grid(b=True, which='minor', color='0.5', linestyle='-', linewidth=0.5)

#The next 2 lines of code are used to set the transparency of the legend to 1.
#The default legend setting was transparent and was cluttered.
leg = plt.legend(mylegend, loc='best')
leg.get_frame().set_alpha(1)

plt.xlabel('Reynolds number', fontsize=30)
plt.ylabel('Friction factor', fontsize=30)

plt.show()  
plt.savefig('reynolds_and_friction_factor.png')
```


![png](DC_Python_Tutorial_Solution_files/DC_Python_Tutorial_Solution_94_0.png)


### 13)
Researchers in the AguaClara laboratory collected the following head loss data through a 1/8" diameter tube that was 2 m long using water at 22 C. The data is in a comma separated data file named ['Head_loss_vs_Flow_dosing_tube_data.csv'](https://github.com/AguaClara/CEE4540_DC/blob/master/Head_loss_vs_Flow_dosing_tube_data.csv). Use the pandas read_csv function to read the data file into a pandas data object. Display the data so you can see how it is formatted.


```python

head_loss_data = pd.read_csv('Head_loss_vs_Flow_dosing_tube_data.csv')  
head_loss_data  


```

<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }
    .dataframe thead th {
        text-align: left;
    }
    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Head loss (m)</th>
      <th>Flow rate (mL/min)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.063</td>
      <td>41.833333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.073</td>
      <td>48.666667</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.083</td>
      <td>51.500000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.093</td>
      <td>60.833333</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.103</td>
      <td>67.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.113</td>
      <td>73.333333</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.123</td>
      <td>77.000000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.133</td>
      <td>82.666667</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.143</td>
      <td>86.500000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.153</td>
      <td>94.833333</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.162</td>
      <td>102.000000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.172</td>
      <td>106.833333</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.182</td>
      <td>112.833333</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.192</td>
      <td>115.666667</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0.202</td>
      <td>122.666667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.212</td>
      <td>128.166667</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0.221</td>
      <td>133.833333</td>
    </tr>
    <tr>
      <th>17</th>
      <td>0.231</td>
      <td>135.500000</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0.241</td>
      <td>144.000000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.251</td>
      <td>148.000000</td>
    </tr>
  </tbody>
</table>
</div>



### 14)
Assign the head loss and the flow rate data to separate 1d NumPy arrays. Attach the correct units. NumPy.array can extract the data by simply passing it the text string of the column header. Here is example code to create the first array. `HL_data=np.array(head_loss_data['Head loss (m)'])*u.m`


```python
HL_data=np.array(head_loss_data['Head loss (m)'])*u.m
Q_data=np.array(head_loss_data['Flow rate (mL/min)'])*u.mL/u.min
```

### 15)
Calculate and report the maximum and minimum Reynolds number for this data set.


```python
D_tube=1/8*u.inch
L_tube=2*u.m
T_data=u.Quantity(22,u.degC)
nu_data=pc.viscosity_kinematic(T_data)
Re_data_max=max(pc.re_pipe(Q_data,D_tube,nu_data))
Re_data_min=min(pc.re_pipe(Q_data,D_tube,nu_data))
print('The Reynolds number varied from '+ut.sig(Re_data_min,2)+' to '+ut.sig(Re_data_max,2)+'.')
```

    The Reynolds number varied from 2.9e+2 to 1.0e+3.


### 16)
Plot the data (as data points and NOT AS A CONTINUOUS LINE) and the theoretical value of head loss in a straight tube (as a curve) on a graph. For the theoretical value assume that minor losses were negligible. Make the y axis have units of cm and the x axis have units of mL/s.

A couple of hints.
* You can use the linspace command to create a set of flows to calculate the theoretical head loss for the plot. Linspace doesn't work with units and so you will need to remove the units and then reattach the correct units of flow.
* convert the flow and head loss data to the desired units when passing the data arrays to the plot method.
* The `pc.headloss_fric` function can handle arrays as inputs, so that makes it easy to produce the theoretical head loss array.




```python
Qpoint=50

QGraph= np.linspace((min(Q_data).to(u.mL/u.s)).magnitude, (max(Q_data).to(u.mL/u.s)).magnitude, Qpoint)*u.mL/u.s

plt.plot(Q_data.to(u.mL/u.s),HL_data.to(u.cm),'o')
plt.plot(QGraph.to(u.mL/u.s),pc.headloss_fric(QGraph,D_tube,L_tube,nu_data,0*u.mm).to(u.cm), '-',linewidth=2)

leg=plt.legend(['data','theoretical major losses'], loc='best')
leg.get_frame().set_alpha(1)
plt.xlabel('Flow rate (mL/s)')
plt.ylabel('Headloss (cm)')
plt.title(' Headloss vs Flow rate')
plt.show()
plt.savefig('headloss_vs_flow_rate.png')
```


![png](DC_Python_Tutorial_Solution_files/DC_Python_Tutorial_Solution_102_0.png)


The theoretical model doesn't fit the data very well. We assumed that major losses dominated. But that assumption was wrong. So let's try a more sophisticated approach where we fit minor losses to the data. Below we demonstrate the use of the [scipy curve_fit method](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html#scipy.optimize.curve_fit) to fit the minor loss coefficient given this data set.  


```python
from scipy.optimize import curve_fit

# Define a new function that calculates head loss given the flow rate
# and the parameter that we want to use curve fitting to estimate
# Define the other known values inside the function because we won't be passing those parameters to the function.

def HL_curvefit(FlowRate, KMinor):
    # The tubing is smooth AND pipe roughness isn't significant for laminar flow.
    PipeRough = 0*u.mm
    L_tube=2*u.m
    T_data=u.Quantity(22,u.degC)
    nu_data=pc.viscosity_kinematic(T_data)
    D_tube=1/8*u.inch
    # pass all of the parameters to the head loss function and then strip the units so
    # the curve fitting function can handle the data.
    return (pc.headloss(FlowRate, D_tube, L_tube, nu_data, PipeRough, KMinor)).magnitude

# The curve fit function will need bounds on the unknown parameters to find a real solution.
# The bounds for K minor are 0 and 20.

# The curve fit function returns a list that includes the optimal parameters and the covariance.

popt, pcov = curve_fit(HL_curvefit, Q_data, HL_data, bounds=[[0.],[20]])

K_minor_fit = popt[0]

# Plot the raw data
plt.plot(Q_data.to(u.mL/u.s), HL_data.to(u.cm), 'o', label='data')

# Plot the curve fit equation.
plt.plot(Q_data.to(u.mL/u.s), ((HL_curvefit(Q_data, *popt))*u.m).to(u.cm), 'r-', label='fit')
plt.xlabel('Flow rate (mL/s)')
plt.ylabel('Head loss (cm)')
plt.title('Curve fit of headloss to flow rate')
plt.legend()
plt.show()
plt.savefig('curve_fit_headloss_and_flow_rate.png')

#Calculate the root mean square error to estimate the goodness of fit of the model to the data
RMSE_Kminor = (np.sqrt(np.var(np.subtract((HL_curvefit(Q_data, *popt)),HL_data.magnitude)))*u.m).to(u.cm)
print('The root mean square error for the model fit when adjusting the minor loss coefficient was '+ut.sig(RMSE_Kminor,2))
```


![png](DC_Python_Tutorial_Solution_files/DC_Python_Tutorial_Solution_104_0.png)


    The root mean square error for the model fit when adjusting the minor loss coefficient was 0.39 cm


### 16)
Repeat the analysis from the previous cell, but this time assume that the minor loss coefficient is zero and that diameter is the unknown parameter.

```python
# Define a new function that calculates head loss given the flow rate
# and the parameter that we want to use curve fitting to estimate
# Define the other known values inside the function because we won't be passing those parameters to the function.

def HL_curvefit2(FlowRate, D_tube):
    # The tubing is smooth AND pipe roughness isn't significant for laminar flow.
    PipeRough = 0*u.mm
    L_tube=2*u.m
    T_data=u.Quantity(22,u.degC)
    nu_data=pc.viscosity_kinematic(T_data)
    KMinor=0
    # pass all of the parameters to the head loss function and then strip the units so
    # the curve fitting function can handle the data.
    return (pc.headloss(FlowRate, D_tube, L_tube, nu_data, PipeRough, KMinor)).magnitude

# The curve fit function will need bounds on the two unknown parameters to find a real solution.
# The bounds for the diameter are 1 to 10 mm and must be given in meters.
# The curve fit function returns a list that includes the optimal parameters and the covariance.

popt, pcov = curve_fit(HL_curvefit2, Q_data, HL_data, bounds=[[0.001],[0.01]])

D_tube_fit = popt[0]*u.m

# Plot the raw data
plt.plot(Q_data.to(u.mL/u.s), HL_data.to(u.cm), 'o', label='data')

# Plot the curve fit equation.
plt.plot(Q_data.to(u.mL/u.s), ((HL_curvefit2(Q_data, *popt))*u.m).to(u.cm), 'r-', label='fit')
plt.xlabel('Flow rate (mL/s)')
plt.ylabel('Head loss (cm)')
plt.legend()
plt.show()
plt.savefig('curve_fit_and_covariance_headloss_and_flowrate.png')

#Calculate the root mean square error to estimate the goodness of fit of the model to the data
RMSE_Diameter = (np.sqrt(np.var(np.subtract((HL_curvefit(Q_data, *popt)),HL_data.magnitude)))*u.m).to(u.cm)
print('The root mean square error for the model fit when adjusting the diameter was '+ut.sig(RMSE_Diameter,2))
```


![png](DC_Python_Tutorial_Solution_files/DC_Python_Tutorial_Solution_106_0.png)


    The root mean square error for the model fit when adjusting the diameter was 1.5 cm


### 17
Changes to which of the two parameters, minor loss coefficient or tube diameter, results in a better fit to the data?

The root mean square error was smaller when the minor loss coefficient was varied to fit the data.

### 18
What did you find most difficult about learning to use Python? Create a brief example as an extension to this tutorial to help students learn the topic that you found most difficult.

## Final Pointer
It is good practice to close, reopen, and rerun your file after completing an assignment to make sure that everything in your assignment works correctly and that you haven't deleted an essential line of code!
