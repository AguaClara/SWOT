# Flow Control and Measurement Design Challenge


Researchers in the AguaClara laboratory collected the following head
loss data through a 1/8" diameter tube that was 2 m long using water at
22°C. The data is in a comma separated data (.csv) file named
[Head_loss_vs_Flow_dosing_tube_data.csv](https://raw.githubusercontent.com/AguaClara/CEE4520/master/DC%20Solutions/Markdown/Head_loss_vs_Flow_dosing_tube_data.csv)
. Use the pandas read csv function (`pd.read_csv('filename.csv')`) to
read the data file. Display the data so you can see how it is formatted.

``` python
  import pandas as pd
  import numpy as np
  from aguaclara.core.units import unit_registry as u
  url = 'https://raw.githubusercontent.com/AguaClara/CEE4520/master/DC%20Solutions/Markdown/Head_loss_vs_Flow_dosing_tube_data.csv'
  head_loss_data = pd.read_csv(url)
  head_loss_data
```

## 1)


Using the data table above, assign the head loss and flow rate data to
separate 1-D arrays. Attach the correct units. `np.array` can extract
the data by simply inputting the text string of the column header. Here
is example code to create the first array:
``` python
  HL_data=np.array(head_loss_data['Head loss (m)'])*u.m
```

## 2)
Calculate and report the maximum and minimum Reynolds number for this
data set. Use the tube and temperature parameters specified above. Use
the `min` and `max` functions which take arrays as their inputs.

The Reynolds number varied from 2.9e+2 to 1.0e+3.

## 3)
You will now create a graph of head loss vs flow for the tube mentioned
in the previous problems. This graph will have two sets of data: the
real data contained within the csv file and some theoretical data. The
theoretical data is what we would expect the head loss through the tube
to be in an ideal world for any given flow. When calculating the
theoretical head loss, assume that minor losses are negligible. Plot the
data from the csv file as individual data points and the theoretical
head loss as a continuous curve. Make the y-axis have units of cm and
the x-axis have units of mL/s.

A few hints.

-   To find the theoretical head loss, you will first need to create
        an array of different flow values. While you could use the
        values in the csv file that you extracted in Problem 14, we
        would instead like you to create an array of 50 equally-spaced
        flow values. These values shall be between the minimum and
        maximum flows in the csv file.
-   You can use the `np.linspace(input1, input2, input3)` function
        to create this set of equally-spaced flows. Inputs for
        `np.linspace` are the same as they were for `np.logspace`, which
        was used in Problem 12a). Linspace does not work with units; you
        can make the inputs dimensionless and then multiply the array by
        a scaling factor with units.
-   The `pc.headloss_fric` function can handle arrays as inputs, so
        that makes it easy to produce the theoretical head loss array
        once you have finished your equally-spaced flow array.
-   When using plotting, make sure to convert the flow and head loss
        data to the desired units.

## 4)

The theoretical model doesn't fit the data very well. We assumed that
major losses dominated. But that assumption was wrong. So let's try a
more sophisticated approach where we fit minor losses to the data. Below
we demonstrate the use of the [scipy curve_fit
method](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html#scipy.optimize.curve_fit)
to fit the minor loss coefficient given this data set. In this example,
`Q_data` is the flow rate array for the csv file from problem 13. You
should re-name this variable below to whatever you titled this variable.

``` python
  from scipy.optimize import curve_fit

  # Define a new function that calculates head loss given the flow rate
  # and the parameter that we want to use curve fitting to estimate
  # Define the other known values inside the function because we won't be passing those parameters to the function.

  def HL_curvefit(FlowRate, KMinor):
      # The tubing is smooth AND pipe roughness isn't significant for laminar flow.
      PipeRough = 0*u.mm
      L_tube = 2*u.m
      T_data = u.Quantity(22,u.degC)
      nu_data = pc.viscosity_kinematic(T_data)
      D_tube = 1/8*u.inch
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
  plt.legend()
  plt.show()

  #Calculate the root mean square error to estimate the goodness of fit of the model to the data
  RMSE_Kminor = (np.sqrt(np.var(np.subtract((HL_curvefit(Q_data, *popt)),HL_data.magnitude)))*u.m).to(u.cm)
  print('The root mean square error for the model fit when adjusting the minor loss coefficient was',RMSE_Kminor)
```

The root mean square error for the model fit when adjusting the minor
loss coefficient was 0.39 cm

## 5)
Repeat the analysis above, but this time assume that the minor loss
coefficient is zero and that diameter is the unknown parameter. The
bounds specified in the line beginning with `popt, pcov` should be
changed from the previous question (which had bounds from 0 to 20) to
the new bounds of 0.001 to 0.01.

Hint: You only need to change the name of the defined function (perhaps
"`HL_curvefit2`"?) and adjust its inputs/values.

The root mean square error for the model fit when adjusting the diameter
was 0.47 cm

## 6)
Changes to which of the two parameters, minor loss coefficient or tube
diameter, results in a better fit to the data?

## 7)
Create a design for a [chemical dose controller using
aguaclara](https://github.com/AguaClara/aguaclara/blob/master/aguaclara/design/cdc.py)
. Then take that design and calculate the maximum coagulant dose that it
will deliver.

``` python
  import aguaclara
  from aguaclara.core.units import unit_registry as u
  from aguaclara.design import cdc as cdc
  from aguaclara.core import physchem as pc
  import numpy as np
  FlowPlant = 60 * u.L/u.s
  ConcDoseMax = 20 * u.mg/u.L
  ConcStock = 60 * u.g/u.L
  DiamTubeAvail = (np.linspace(1,10,10)) * 1/16 * u.inch
  print(DiamTubeAvail.magnitude)
  HeadlossCDC = 20 * u.cm
  LenCDCTubeMax = 4 * u.m
  temp = 20 * u.degC
  # 1 is for PACl
  en_chem =  1
  KMinor = 2

  L_tube = cdc.len_cdc_tube(FlowPlant, ConcDoseMax, ConcStock, DiamTubeAvail, HeadlossCDC, LenCDCTubeMax, temp, en_chem, KMinor)
  D_tube = cdc.diam_cdc_tube(FlowPlant, ConcDoseMax, ConcStock, DiamTubeAvail, HeadlossCDC, LenCDCTubeMax, temp, en_chem, KMinor).to(u.inch)
  n_tube = cdc.n_cdc_tube(FlowPlant, ConcDoseMax, ConcStock, DiamTubeAvail, HeadlossCDC, LenCDCTubeMax, temp, en_chem, KMinor)

  Nu = cdc.viscosity_kinematic_pacl(ConcStock, temp)
  PipeRough = 0 * u.mm

  C_Plant_Max = n_tube * pc.flow_pipe(D_tube, HeadlossCDC, L_tube, Nu, PipeRough, KMinor) * ConcStock/FlowPlant
  print(C_Plant_Max.to(u.mg/u.L))
```

## 8)
An AguaClara plant will be upgraded from 20 L/s to 30 L/s by adding two
sedimentation tanks, increasing the head loss through the flocculator,
and adding an additional StaRS filter. Give the current design specs for
the CDC. Propose the most cost effective modification to the CDC to
handle the additional flow.

## 9)
Determine if the LFOM diameter will need to be increased for a 20 L/s to
30 L/s plant upgrade.
