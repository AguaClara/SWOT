# Python Design Challenge

### 1)
Calculate the minimum inner diameter of a PVC pipe that can carry a flow of at least 10 L/s for the town of Ojojona. The population is 4000 people. The water source is a dam with a surface elevation of 1500 m. The pipeline connects the reservoir to the discharge into a distribution tank at an elevation of 1440 m. The pipeline length is 2.5 km. The pipeline is made with PVC pipe with an SDR (standard diameter ratio) of 26.

The pipeline inlet at the dam is a square edge with a minor loss coefficient (${K_e}$) of 0.5. The discharge at the top of the distribution tank results in a loss of all of the kinetic energy and thus the exit minor loss coefficient is 1. See the minor loss equation below.

$${h_e} = {K_e}\frac{{{V^2}}}{{2g}}$$

The water temperature ranges from 10 to 30 Celsius. The roughness of a PVC pipe is approximately 0.1 mm. Use the fluids functions to calculate the minimum inner pipe diameter to carry this flow from the dam to the distribution tank.

Report the following

- critical design temperature
- kinematic viscosity (maximum viscosity will occur at the lowest temperature)
- the minimum inner pipe diameter (in mm).

Use complete sentences to report the results.

    The critical water temperature for this design is 10 degC.
    The kinematic viscosity of water is 1.3e-6 m²/s.
    The minimum pipe inner diameter is 97 mm.

### 2)
Find the nominal diameter of a PVC pipe that is SDR 26. SDR means standard diameter ratio. The thickness of the pipe wall is 1/SDR of the outside diameter. The [pipes
file](https://github.com/AguaClara/aguaclara/blob/master/aguaclara/core/pipes.py) has a useful function that returns nominal diameter given SDR and inner diameter.

    The nominal diameter of the pipeline is 4.0 in (1.0e+2 mm).

### 3)
What is the actual inner diameter of this pipe in mm? Compare this with the [reported inner diameter for SDR-26 pipe](http://www.cresline.com/pdf/cresline/pvcpressurepipe&ftgs/pvc761lw.pdf) to see if our pipe database is reporting the correct value.

    The inner diameter of the pipe is 106 mm.
    Cresline reports the inner diameter is 106 mm.

### 4)
What is the maximum flow rate that can be carried by this pipe at the coldest design temperature? Display the flow rate in L/s using the .to method.

    The maximum flow rate at 10 Celsius is 13 l/s.

### 5)
What is the Reynolds number and friction factor for this maximum flow?
Assign these values to variable names so you can plot them later on the Moody diagram.

    The Reynolds number and friction factor for the pipeline flow are 1.2e+5 and 0.022 respectively.

### 6)
Check to see if the fluids functions are internally consistent by calculating the head loss given the flow rate that you calculated and comparing that head loss with the elevation difference. Note that the Moody diagram has an accuracy of about ±5% for smooth pipes and ±10% for rough pipes [Moody, 1944](http://user.engineering.uiowa.edu/~me_160/lecture_notes/MoodyLFpaper1944.pdf).

    The head loss is 60.5 m and that is close to the elevation difference of 60.0 m.

### 7)
How much more water (both volumetric and mass rate) will flow through the pipe at the maximum water temperature of 30 C? Take into account both the change in viscosity (changes the flow rate) and the change in density (changes the mass rate). Report the flow rates in L/s.

    The increase in flow rate at 30 Celsius is 0.24 l/s.
    The increase in mass rate at 30 Celsius is 0.19 kg/s.

### 8)
Why is the flow increase due to this temperature change so small given that viscosity actually changed significantly (see the calculation below)?

    The viscosity ratio for the two temperatures was 0.62.

The flow is turbulent and thus viscosity has little influence on the flow rate.

### 9)
Suppose an AguaClara plant is designed to be built up the hill from the distribution tank. The transmission line will need to be lengthened by 30 m and the elevation of the inlet to the entrance tank will be 1450 m. The rerouting will also require the addition of 3 elbows with a minor loss coefficient of 0.3 each. What is the new maximum flow from the water source?

    The new maximum flow rate at 10 Celsius is 12 l/s.

### 10)
How much less water will flow through the transmission line after the line is rerouted?

    The reduction in flow is 1.3 l/s.

### 11)
There exists a function within physchem called `pc.fric(FlowRate, Diam, Nu, PipeRough)` that returns the friction factor for both laminar and turbulent flow. In this problem, you will be creating a new function which you shall call `fofRe()` that takes the Reynolds number and the dimensionless pipe roughness (ε/D) as inputs.

Recall that the format for defining a function is:

``` python
  def fofRe(input1, input2):
    f = buncha stuff
    return f
```

Since the equation for calculating the friction factor is different for laminar and turbulent flow (with the transition Reynolds number being defined within the physchem file), you will need to use an `if, else` statement for the two conditions.

### 12)
Create a beautiful Moody diagram. Include axes labels and show a legend that clearly describes each plot. The result should look like the figure below.

![Moody diagram describing fluid flow in straight pipes.](https://github.com/AguaClara/CEE4520/blob/master/DC/images/Moody.png)


### 12a)
You will be creating a Moody diagram showing Reynolds number vs friction factor for multiple dimensionless pipe roughnesses. The first step to do this is to define the number of dimensionless pipe roughnesses you want to plot. We will plot 8 curves for the following values: 0, 0.0001, 0.0003, 0.001, 0.003, 0.01, 0.03, 0.1. We will plot an additional curve, which will be a straight line, for laminar flow, since it is not
dependent on the pipe roughness value.

- Create an array for the dimensionless pipe roughness values, using `np.array([])`.
- Specify the amount of data points you want to plot for each curve. We will be using 50 points.

Because the Moody diagram is a log-log plot, we need to ensure that all 50 points on the diagram we are creating are equally spaced in log-space. Use the `np.logspace(input1, input2, input3)` function to create an array for turbulent Reynolds numbers and an array for laminar Reynolds numbers.

- `input1` is the exponent for the lower bound of the range. For example, if you want your lower bound to be 1000, your input should be `math.log10(1000)` which is equal to 3.
- `input2` is the exponent for the upper bound of the range. Format this input as you have formatted `input1`.
- `input3` is the number of data points you are using for each curve. We will be using 50 points.

**12a) Deliverables**

- Array of dimentionless pipe roughnesses. Call this array `eGraph`.
- Variable defining the amount of points on each pipe roughness curve
- Two arrays created using `np.logspace` for turbulent and laminar Reynolds numbers, which will be the x-axis values for the Moody diagram

Note: The bounds for the laminar Reynolds numbers array should span between 670 and the predefined transition number used in Problem 11. The bounds for the turbulent Reynolds numbers array should span between 3,500 and 100,000,000. These ranges are chosen to make the curves fit well within the graph and to intentionally omit data in the transition range between laminar and turbulent flows.

### 12b)
Now you will create the y-axis values for turbulent flow (based on dimensionless pipe roughness) and laminar flow (not based on dimensionless pipe roughness). To do this, you will use the `fofRe()` function you wrote in Problem 11 to find the friction factors.

Begin by creating an empty 2-dimensional array that will be populated by the turbulent-flow friction factors for each dimensionless pipe roughness. Use `np.zeros(number of rows, number of columns)`. The number of rows should be the number of dimensionless pipe roughness values (`len(eGraph)`), while the number of columns should be the number of data points per curve as defined above. Populating this array with friction factor values may require two `for` loops, one to iterate through rows and one to iterate through columns.

You will repeat this process to find the friction factors for laminar flow. The only difference between the turbulent and laminar friction flow arrays will be that the laminar array will only have one dimension since it does not affected by the dimensionless pipe roughness. Start by creating an empty 1-dimensional array and then use a single `for` loop.

**12b) Deliverables**

- One 1-D array containing friction factor values for laminar flow.
- One 2-D array containing friction factor values for each dimensionless pipe roughness for turbulent flow.

### 12c)
Now, we are ready to start making the Moody diagram! The plot formatting is included for you in the cell below. You will add to this cell the code that will actually plot the arrays you brought into existence in 12a) and 12b) with a legend. For the sake of your own sanity, please only add code where specified.

- First, plot your arrays. See the plots in the tutorial above for the syntax. Recall that each dimensionless pipe roughness is a separate row within the 2-D array you created. To plot these roughnesses as separate curves, use a `for` loop to iterate through the rows of your array. To plot all columns in a particular row, use the `[1,:]` call on an array, where 1 is the row you are calling.
- Plotting the laminar flow curve does not require a `for` loop because it is a 1-D array.
- Use a linewidth of 4 for all curves.
- Now plot the data point you calculated for the pipeline problem. Use the Reynolds number and friction factor obtained in Problem 5. Because this is a single point, it should be plotted as a circle instead of a line.
- You will need to make a legend for the graph using `ax.legend(stringarray, loc = 'best')` The first input, `stringarray`, must be an array composed of strings instead of numbers. The array you created which contains the dimensionless pipe roughness values (`eGraph`) can be converted into a string array for your legend (`eGraph.astype('str'))`. You will need to add 'Laminar' and 'Pipeline' as strings to the new `eGraph` string array. Perhaps you will find `np.append(basestring, [('string1','string2')])` to be useful.

### 13)
What did you find most difficult about learning to use Python? Create a brief example as an extension to this tutorial to help students learn
the topic that you found most difficult.

## Final Pointer
Before submitting a file for others to use, you need to verify that all of the dependencies are defined and that you didn't accidently delete a definition that is required. You can do this by placing your cursor in a python code section and then clicking on the python 3|idle in the toolbar at the bottom of the Atom window. Select restart Python 3 kernel. Then execute all of the python code in your document from top to bottom and make sure that all of the code performs as expected.
