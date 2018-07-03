# Flow Control and Measurement Solution

```python
from aide_design.play import*
```
## Vertical orifice equation


### 1)
The simple orifice equation $Q = {\Pi _{vc}}{A_{or}}\sqrt {2g\Delta h}$ that we normally use is not applicable for vertically oriented orifices that are partially or barely submerged. The [USGS published a great solution](https://il.water.usgs.gov/proj/feq/fequtl98.i2h/4_7aupdate.html) for flow through partially submerged vertically oriented orifices. AguaClara uses a general solution for a vertically oriented orifice, which is available in the physchem file as `pc.flow_orifice_vert`. That function handles vertically oriented orifices even if they are only partially submerged.

The vertical orifice equation is based on the concept that the velocity through the orifice at any point is equal to $\sqrt{2gh}$, where h is the local depth of submergence. The total flow can be obtained by integration of that velocity over the submerged area of the orifice.

For this question, you will create a well formatted graph with two curves to display flow rate through a 5 cm diameter orifice oriented **vertically and horizontally**.

We want to be able to describe the height of the water in the orifice as relative to the orifice diameter size. The relationship between velocity and orifice diameter is true for orifices of any size, so it is valuable to create a non-dimensional model that can be understood for all diameters. The flow rate that you will use for this question is as a function of the normalized depth of water from 1 diameter below the center of the orifice to 2 diameters above the center of the orifice.

The steps for making the graph are as follows:

  - Use `np.linspace` to generate an array of 100 dimensionless water surface elevations ranging from -1 to 2.
  - Create a second array for water elevation (with units) by multiplying the normalized water elevation array by the orifice diameter.
  - Create two arrays of flow rates through the orifice: one for the horizontal orifice orientation and one for the vertical orifice orientation. Use the two orifice equations `pc.flow_orifice` and `pc.flow_orifice_vert` in the physchem file, with orifice diameter and the dimensional water elevation array you created as inputs.  
  - Plot the curves for vertical and horizontal orifice flow in L/s as a function of the normalized height of water.
  - Label the graph with flow rate in L/s as the y-axis and with normalized water elevation above the center of the orifice as the x-axis.
  - Include a legend for the two curves.
  - The vena contracta value can be found in expert_inputs


```python
WaterElevationNormalized = np.linspace(-1,2,100)

DiamOrifice = 5*u.cm
WaterElevation = WaterElevationNormalized*DiamOrifice

HorizontalOrificeFlows = (pc.flow_orifice(DiamOrifice, WaterElevation, exp.RATIO_VC_ORIFICE)).to(u.L/u.s)
VerticalOrificeFlows = pc.flow_orifice_vert(DiamOrifice, WaterElevation, exp.RATIO_VC_ORIFICE).to(u.L/u.s)

plt.figure(0)
plt.plot(WaterElevationNormalized, HorizontalOrificeFlows, 'r-', WaterElevationNormalized, VerticalOrificeFlows, 'b-')

plt.xlabel('Normalized height of water above center of the orifice')
plt.ylabel('Flow rate through the orifice (L/s)')
plt.title('Horizontal vs. Vertical Orifice Orientation')
plt.legend(['Horizontal Orientation', 'Vertical orientation'], loc='best')
plt.grid(True)
#plt.savefig('plots/vertical_horizontal_orifice.png') this isn;t working for me..path issue?
plt.savefig('test_plot.png')
plt.show()

```
<img src="/test_plot.png" alt = "this should be an image and this is the alt text">




## Linear Flow Orifice Meter (LFOM)
A linear flow orifice meter is used in AguaClara plants to measure the plant flow rate and to provide  a linear relationship between flow rate and the depth of water in the entrance tank. Below, we use the LFOM code to obtain a design for a linear flow orifice meter. Your task will be to test this design using the orifice equations to see if it is correct.


```python
#target flow rate that the LFOM should deliver at maximum water height
Flow = 31*u.L/u.s

#height range for the LFOM measured from the bottom of the first row of orifices.
HeadlossLfom = 20*u.cm

#Safety factor that insures that the LFOM pipe doesn't completely fill with water at the bottom row of orifices.
#This factor is the ratio of the pipe area to the area required to contain all of the falling water.
RatioLfomSafety = 1.2

#We will use a pipe with a relatively low SDR so that it has a thick wall to handle the many perforations.
SdrLfom = 26

#The DrillBits array is an array with the available drill bits (or hole saws) that can be used to create the orifices.
#Here we assume that we only have a very limited set of drill bits.
DrillBits = np.arange(5, 25, 5)*u.mm

#Here we use the LFOM functions to get the key parameters that define an LFOM.
NdLfom = lfom.nom_diam_lfom_pipe(Flow, HeadlossLfom, RatioLfomSafety, SdrLfom)
OrificeDiam = lfom.orifice_diameter(Flow, HeadlossLfom, DrillBits)
LfomOrificeArray = lfom.n_lfom_orifices(Flow, HeadlossLfom, DrillBits, SdrLfom)
HeightLfomOrifices = lfom.height_lfom_orifices(Flow, HeadlossLfom, DrillBits)

print('The nominal diameter of the LFOM is ' + ut.sig(NdLfom,1)+'.')
print('The orifice diameter is ' + ut.sig(OrificeDiam,2)+'.')
print('The number of orifices in each row is')
print(LfomOrificeArray)
print('The height of the center of the orifices measured from the LFOM datum, the bottom of the bottom row of orifices, is')
print(HeightLfomOrifices.to(u.cm))

```

    The nominal diameter of the LFOM is 10 in.
    The orifice diameter is 15 mm.
    The number of orifices in each row is
    [ 43.  43.  14.  15.  13.  12.  11.  11.   9.  10.]
    The height of the center of the orifices measured from the LFOM datum, the bottom of the bottom row of orifices, is
    [  0.75   2.75   4.75   6.75   8.75  10.75  12.75  14.75  16.75  18.75] centimeter


### 4)
**Create a function** that calculates the flow rate through the LFOM as a function of only water elevation using the vertical orifice function. Use the arrays for LFOM key parameters, given above as `NdLfom`, `OrificeDiam`, `LfomOrificeArray`, and `HeightLfomOrifices`.

- Create an array for depth of submergence for each row of orifices at a given a height of water in the LFOM. This array is dependent on the water elevation (which should be your function input) and the height of the LFOM orifices (which is from the LFOM key parameters). Use this submergence depth array as the "height" input to your vertical orifice function. The array should be created within your function.

- To calculate the flow rate through the LFOM, multiply the calculated flow for each row of orifices by the number of orifices in that row (`LfomOrificeArray`) to get an array of flows through each row of orifices. Note: the vertical orifice function will report zero flow for any orifices that aren't submerged, so you can send the whole array of depth of submergence for each row of orifices.

- At the end of your function, sum flows from each row of the LFOM and return that value with the correct units.

- Add a comment under the function definition to explain what the function does (see any of the aide design files for examples of descriptive comments).


```python
def flow_lfom_vert(height):
    "Returns the flow through the LFOM as a function of height"
    Flow = pc.flow_orifice_vert(OrificeDiam, height - HeightLfomOrifices, exp.RATIO_VC_ORIFICE)*LfomOrificeArray
    return (sum(Flow)).to(u.L/u.s)

print(flow_lfom_vert(5*u.cm))
```

    7.839628413633346 liter / second


### 5)
Calculate the total flow through the LFOM using the vertical orifice equation for the case when the water level is at the maximum water level for the LFOM, `HeadlossLfom`. You are checking to make sure that the LFOM produces the correct target flow (given as `Flow`) at the maximum height. Does it?


```python
FlowMaxVert = flow_lfom_vert(HeadlossLfom)
print('The flow at a depth of '+ut.sig(HeadlossLfom,2)+' is '+ut.sig(FlowMaxVert,4))
print('This flow is slightly larger than the target flow of '+ut.sig(Flow,2)+'.')
```

    The flow at a depth of 20 cm is 31.49 l/s
    This flow is slightly larger than the target flow of 31 l/s.


### 6)
We want to compare the actual flow rate through the LFOM to the expected flow rate through the elevation as a function of water depth. Create a graph of the normalized actual and expected flow rates, using the following steps:

- Create an 100-unit long array of water depths using `np.linspace`. Note: the expected flow rate at elevation zero is zero, which makes the normalized flow rate undefined for zero elevation. An undefined normalized flow will not run and Python will report an error. You can solve this by beginning your water depth array at a very small (nonzero) elevation. You can end your water depth array at the maximum water depth. Recall that an array of elevations should have units of length.
- Create an array of normalized actual flow rates at each water depth; use the function you created in Problem 4 and a `for` loop (the function you created in Problem 4 probably can't handle an array of depths as input, so you need the `for` loop to cycle through each depth value to make your array of flows).     
    - Start by creating an empty array for actual flow rates that is the same shape as the 100-unit water depth array you just created.
    - In your `for` loop, normalize the actual flow rates by using the following relationship: normalized actual flow rate = (actual flow rate)/[(water depth * target flow rate)/maximum water level]

- Plot a straight horizontal line at y = 1, which is your normalized expected flow value if the LFOM were perfect.


```python
#Create an array of water depths
HeightGraph = np.linspace(0.001, HeadlossLfom.to(u.cm),100) * u.cm

#Create an array that is empty
FlowGraph = np.empty_like(HeightGraph)
# or FlowGraph = []
for i in range(len(HeightGraph)):
    FlowGraph[i] = (flow_lfom_vert((HeightGraph[i]))/((HeightGraph[i]) / HeadlossLfom * Flow)).magnitude

plt.plot(HeightGraph, FlowGraph, 'r-', HeightGraph, np.ones(100), 'c-')
plt.xlabel('Water Depth (cm)')
plt.ylabel('Normalized flow rate')
plt.title('Normalized Flow Rate vs. Water Depth')
plt.legend(['Vertical Orifice', 'Target'], loc='best')
plt.grid(True)
plt.show()
plt.savefig('normalized_flow_vs_water_depth.png')


```
<img src="/normalized_flow_vs_water_depth.png" alt="this should be a plot, this is alt text">


## Laminar Flow Based Flow Controller

You will design (by completing the following questions) a laminar flow controller for chlorine feed for a plant design flow rate of 50 L/s.

For the following steps do NOT use the aide_design.cdc code. Instead, create the functions that you need to solve this problem. At the end, we will compare your solution to the aide_design.cdc solution.

You may assume that the chlorine stock solution kinematic viscosity is approximately the same as water. The dose controller is to have a maximum head loss of 20 cm through the dosing tubes. We will start with commercially available liquid bleach (equivalent to 51.4 gm/L of chlorine gas), which we will use in our chemical stock tanks without dilution. Our goal is to provide a constant chlorine dose of 2 mg/L to the water entering the storage tank. We will be following the guidelines given below.

- Calculate the maximum flow rate through each available dosing tube diameter that keeps error due to minor losses below 10%.

- Calculate the total chemical flow rate that would be required by the treatment system for the maximum chemical dose and the maximum allowable stock concentration.

- Calculate the number of dosing tubes required if the tubes flow at maximum capacity (round up).

- Calculate the length of the dosing tubes that correspond to each available tube diameter.

- Select the longest dosing tube that is shorter than the maximum tube length allowable based on geometric constraints.

- Select the dosing tube diameter, flow rate, and stock concentration corresponding to the selected tube length.


```python
FlowPlant = 50*u.L/u.s
T = u.Quantity(20,u.degC)
NuBleach = pc.viscosity_kinematic(T)
HeadlossDosingTubeMax = 20*(u.cm)
StockCl2 = 51.4*(u.gram/u.L)
DoseCl2 = 2*(u.mg/u.L)
RatioError = 0.1
KMinor = 2
```

### 11)
At the given water treatment plant design flow rate, what is the required flow of bleach (the chlorine stock solution) in mL/s? How many liters of bleach are needed per day?


```python
FlowStockClMax = (FlowPlant * DoseCl2 / StockCl2).to(u.mL/u.s)
print('The required flow of bleach is', ut.sig(FlowStockClMax,3))
print('The daily required flow of bleach is',ut.sig(FlowStockClMax.to(u.L/u.day),5))
```

    The required flow of bleach is 1.95 ml/s
    The daily required flow of bleach is 168.09 l/day


### 13)
Our next big goal is to choose a tubing size for the dosing tube (or tubes). This requires multiple steps. Begin by first creating a numpy array of tubing sizes between 1/16"  and 5/16" with a 1/16" interval. Your list should contain 5 elements. Does `np.linspace` work here? What about `np.arange`?


```python
DiamTubeArray = np.array(np.arange(1/16,6/16,1/16)) * u.inch
print(DiamTubeArray)
```

    [ 0.0625  0.125   0.1875  0.25    0.3125] inch


### 14)
What is the maximum average velocity in a dosing tube based on the constraint that minor losses must be small? This means that the minor losses account for `RatioError` fraction of the total losses (10% when `RatioError` is 0.1). Note that this velocity is independent of the tube diameter.


```python
VelTubeMax = (((RatioError * 2 * HeadlossDosingTubeMax * pc.gravity) / KMinor)**(1/2)).to(u.meter/u.s)
print('The maximum average velocity in a dosing tube is', ut.sig(VelTubeMax,3))
```

    The maximum average velocity in a dosing tube is 0.443 m/s


### 15)
What is the head loss due to minor losses in the tube when the tube is flowing at maximum capacity? Solve for this value algebraically by substituting your equation for the velocity in the tube into the minor loss equation and then calculate the value.


```python
HeadlossMinorMax = RatioError * HeadlossDosingTubeMax
print('The head loss due to minor losses when the tube is at maximum capacity is', ut.sig(HeadlossMinorMax,2))
```

    The head loss due to minor losses when the tube is at maximum capacity is 2.0 cm


### 16)
Create an array of the maximum flow rates corresponding to the array of tubing diameters. The flow rates must meet the error constraint.
$$Q_{Max} = \frac{\pi D^2}{4}\sqrt{\frac{2h_{L}g \Pi_{error}}{\sum K_{e}}}$$

* First, create a function that uses diameter and velocity as inputs to return flow rate. Note that `pc.area_circle(diam)` returns a circle's area given its diameter, and you have already calculated the maximum average velocity in Problem 14.
* Create the array of maximum flow rates using the array of tubing diameters and the maximum headloss through the dosing tubes.


```python
def flow_cdc_max(diam, VelTubeMax):
    Flow = pc.area_circle(diam) * (VelTubeMax)
    return Flow

FlowMaxArray = flow_cdc_max(DiamTubeArray, VelTubeMax).to(u.mL/u.s)
print(FlowMaxArray)
```

    [  0.87658228   3.5063291    7.88924048  14.02531641  21.91455688] milliliter / second


### 17)
Find the minimum number of tubes for each of the available tube diameters that would be required to deliver the maximum flow of bleach.


```python
NDosingTubes = np.ceil(FlowStockClMax / FlowMaxArray)
print('The number of tubes of each diameter is', NDosingTubes)
```

    The number of tubes of each diameter is [ 3.  1.  1.  1.  1.] dimensionless


### 18)
Create an array of the maximum flow rate per tube for each of the available tubing diameters, given the number of tubes that would be used. This will be the flow through each dosing tube at the maximum flow of bleach.


```python
FlowDosingTubeArray = FlowStockClMax / NDosingTubes
print('The flow rate per tube is', FlowDosingTubeArray)
print(FlowStockClMax)
```

    The flow rate per tube is [ 0.64850843  1.94552529  1.94552529  1.94552529  1.94552529] milliliter / second
    1.9455252918287937 milliliter / second


### 19)
We now know the target flow in the dosing tubes, the diameter of the tubes, and the target head loss through the tubes. Thus, we can solve for the length of the tube that will deliver that target flow.
Write a function to find the length of each tube that could handle the entire flow. Your function should use the following equation:
$$L = \frac{g h_{L}\pi D^4}{128 \nu Q_{Max}}-\frac{Q_{Max}}{16 \pi \nu}\sum K_{e}$$

Call your function to return the length of tubing required for each tube size.


```python
def length_tube(flow_max, diam, headloss_max, nu, k_minor):
    "Returns the length of tube necessary to handle the maximum flow."
    L = (((pc.gravity * headloss_max * np.pi * diam**4)/
                           (128 * nu * flow_max))-
                    ((k_minor * flow_max)/
                             (16 * np.pi * nu)))
    return L

LengthDosingTube = length_tube(FlowDosingTubeArray, DiamTubeArray, HeadlossDosingTubeMax, NuBleach, KMinor).to(u.m)

print('The length of each dosing tube would be', LengthDosingTube)

```

    The length of each dosing tube would be [  0.44406171   2.42832361  12.60675229  40.01021413  97.79237081] meter


| 0                | 1          | 2          | 3           | 4           | 5           |
| ---------------- | ---------- | ---------- | ----------- | ----------- | ----------- |
| Max flow (ml/s)  | 0.87658228 | 3.5063291  | 7.88924048  | 14.02531641 | 21.91455688 |
| # tubes          | 3          | 1          | 1           | 1           | 1           |
| Diameters (in)   | 0.0625     | 0.125      | 0.1875      | 0.25        | 0.3125      |
| flow rate (ml/s) | 0.64850843 | 1.94552529 | 1.94552529  | 1.94552529  | 1.94552529  |
| length      (m)  | 0.44406171 | 2.42832361 | 12.60675229 | 40.01021413 | 97.79237081 |     
