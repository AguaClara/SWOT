
# DC Sedimentation


```python
from aide_design.play import*
from aide_design import floc_model as floc
from pytexit import py2tex

#Below are the items that were imported by the code above so that you know what abbreviations to use in your code.

# Third-party imports
#import numpy as np
#import pandas as pd
#import matplotlib.pyplot as plt
#import matplotlib

# AIDE imports
#import aide_design
#import aide_design.pipedatabase as pipe
#from aide_design.units import unit_registry as u
#from aide_design import physchem as pc
#import aide_design.expert_inputs as exp
#import aide_design.materials_database as mat
#import aide_design.utility as ut
#import aide_design.k_value_of_reductions_utility as k
#import aide_design.pipeline_utility as pipeline
#import warnings
```

# Introduction

The AguaClara team would like to understand how to design larger sedimentation tanks. In this design challenge you will learn how some of the sedimentation tank components work together. The design for an entire sedimentation tank is somewhat complex and you are welcome to review the sedimentation tank design file to see the latest AguaClara design team solution.  The sedimentation tank design has evolved rapidly over the past 10 years and our fabrication techniques have evolved as well.  


In AguaClara sedimentation tanks the influent and effluent channels are located above the space occupied by the floc hopper. If you want to see how those geometric constraints are handled you can review the AguaClara sedimentation tank design file. AguaClara is currently working with Agua Para el Pueblo on a 120 L/s plant for Gracias. This plant would have 2 treatment trains and thus we can design for 60 L/s. For this design challenge you may assume the following:

For each step in the solution define a variable with a name that is easily understood so that it can be used later if needed. Consider using the AguaClara naming convention.

Use numpy for ceil, floor, sin, and pi.

<br>
<br>
The following cell has constants defined for you to use in designing your sedimentation tank. Read through and run it so you know what variables have been defined for you.


```python
# We are experimenting with using head loss at the exit of the diffusers as
# a reasonable design constraint for the design of the
# inlet manifold/diffuser system. This head loss in the exit of the diffuser
# will allow higher velocities (and pressure recovery) in the manifold pipe
# and thus will enable use of smaller diameter manifold pipes.
# -----
# We've set a maximum head loss in the sedimentation tank inlet:
headloss_sed_inlet_max = 1 * u.cm

# The manifold and diffuser pipes used in the sedimentation tank have an SDR of 26.
SDR=26

# Pi_jet_plane is used to estimate the maximum energy dissipation rate in a plane jet.
# A plane jet is uniform in one dimension. A plane jet can be formed by a long narrow slot.
Pi_jet_plane = 0.225

# Design temperature will be helpful to calculate viscosity
T_design = 15*u.degC

# Plant Flowrate:
flow_plant = 60 * u.L/u.s

# Upflow velocity at the top of the floc blanket:
V_sed_up = 1 * u.mm/u.s

# The corrugated plastic sheets used to make the plate settlers:
W_sed = 42 * u.inch
thickness_sed_plate = 2 * u.mm

# The plate settlers are angled 60° from the horizontal:
angle_sed_plate = 60 * u.deg

# The plate setters are spaced 2.5cm apart (this is the perpendicular
# distance between plates, not the horizontal distance between plates):
s_sed_plate = 2.5 * u.cm

# Plate settler capture velocity:
V_sed_capture = 0.12 * u.mm/u.s

# The minimum port flow (from the first port) divided by the maximum port
# flow (from the last port) for flow division between sedimentation tanks
# and for flow distribution from the inlet manifold should be at least:
Pi_sed_manifold_flow = 0.8

g = pc.gravity
```

## Diffusers

### 1:

We will start our design of the sedimentation tank by considering the diffusers.

* Calculate the maximum velocity of water leaving the diffuser based on the maximum head loss. Assume that the majority of head loss is the kinetic energy of the flow exiting the diffuser slot (this assumption will be checked later). Assume K=1.


* Calculate the minimum inner width of the diffuser. Assume that the diffuser slot is continuous over the entire length of the sedimentation tank to get an initial estimate (it isn't actually continuous because it is made from many flattened diffuser pipes).

Define your answers as variables and then print those variables.


```python
# minor loss equation with K=1
V_diffuser_max = (np.sqrt((2 * g * headloss_sed_inlet_max))).to(u.m / u.s)
print('The maximum velocity of the sed tank diffusers is',V_diffuser_max)

# mass conservation
W_diffuser_inner_min = ((V_sed_up / V_diffuser_max) * W_sed).to(u.mm)
print('The minimum width of the sed tank diffusers is',W_diffuser_inner_min)
```

    The maximum velocity of the sed tank diffusers is 0.4429 meter / second
    The minimum width of the sed tank diffusers is 2.409 millimeter


### 2:

Diffusers are made by deforming PVC pipe. Softened PVC pipe is forced onto a mold that shapes it into the rectangular shape of the diffuser (see slides from the Sedimentation Lecture).

* What metal plate thickness should be used to make the mold for the diffusers? This value will be the minumum diffuser width. Metal plates are available in 1/16" increments of thickness. The minimum thickness of plate that is strong enough for a mold is 1/16".

Note: you can use the `ceil_nearest` function defined in `utility.py` to do this elegantly. You can create an array of available metal plates using `numpy.arange`.


```python
W_diffuser = ut.ceil_nearest(W_diffuser_inner_min, np.arange(1/16,1/4,1/16)*u.inch)

print('The width of sed tank diffuser is',W_diffuser.to(u.cm))
```

    The width of sed tank diffuser is 0.3175 centimeter


## Py2tex
Show your work for question 3 using pytexit's py2tex. You will need to [install pytextit](https://confluence.cornell.edu/display/cee4540/Installing+Pytexit) if you have not done that yet.  
1. Pytexit is a python package which contains Py2tex and:
    1. Allows you to write LaTeX formulas directly from the Python expression.
    1. Checks Python formulas for correctness: once printed, LaTeX is much more readable than a multiline Python expression.
<br>
<br>
1. **Note:** Py2tex does not handle references from aide_design files well (ex. pc.(), floc.()) but will handle greek letters,numpy (ex. np.pi, np.sin), and user defined variables and functions.
    1. Simply enter your equation to py2tex within ' apostrophes '.
    1. Because py2tex has difficulty with user defined file references, **`py2tex('pc.flow_pipe')` is not okay, but `py2tex('flow_pipe')` is okay**
<br>
<br>
1. Follow the example offered below.


```python
Pi_Error = 0.1
Headloss_DosingTube_Max = 20*(u.cm)
K_Minor = 2

Vel_Tube_Max = (((Pi_Error * 2 * Headloss_DosingTube_Max * g) / K_Minor)**(1/2)).to(u.meter/u.s)
py2tex('Vel_Tube_Max = (((Pi_Error * 2 * Headloss_DosingTube_Max * g) / K_Minor)**(1/2))')
```

$$Vel_{Tube,Max}=\left(\frac{2\,\Pi_{Error}\,Headloss_{DosingTube,Max}\,g}{K_{Minor}}\right)^{\frac{1}{2}}$$


$$Vel_{Tube,Max}=\left(\frac{2\,\Pi_{Error}\,Headloss_{DosingTube,Max}\,g}{K_{Minor}}\right)^{\frac{1}{2}}$$





    '$$Vel_{Tube,Max}=\\left(\\frac{2\\,\\Pi_{Error}\\,Headloss_{DosingTube,Max}\\,g}{K_{Minor}}\\right)^{\\frac{1}{2}}$$'



### 3:

The PVC pipe that forms the diffusers changes in shape and wall thickness during the molding process. The inner width of the rectangle is created by forcing the pipe over a rectangular wedge that is the thickness you calculated above. During the molding process, PVC pipe wall cross-sectional area is conserved. The pipe wall is stretched in total length approximately 20%. Another way to think about this is that the thickness of the wall is reduced by a factor of 1/1.2 because the mass of PVC is conserved and the density is unchanged. Thus, volume and cross-sectional area are conserved.  

* Start by drawing a picture of what is happening to the deformation of the pipe as it is converted from the circular pipe to the rectangular diffuer slot (assume that the slot is a rectangle with perfectly square corners). You do not need to submit your sketches for this design challenge.
    * Draw the initial circular pipe. Label the diagram with the appropriate variables for inner diameter, outer diameter, and wall thickness.
    * Draw the final rectangular diffuser slot. Label the diagram with the appropriate variables for length, width, and wall thickness.


Area is given using the following equation:
$$Area_{PVC}=2\left (B_{diffuser}+W_{diffuser} \right )thickness_{wall}$$

* Use the equation for $Area_{PVC}$ to calculate the following:

    * the outer length of the rectangular diffuser slot, $B_{diffuser}$.
    * the inner length of the rectangular diffuser slot, $W_{diffuser}$.


Answering this question will require using functions from the `pipedatabase` file, imported here as `pipe`.


```python
SDR=26

# Assumed stretch of the PVC pipes as they are heated and molded:
Pi_PVC_stretch = 1.2

# Nominal diameter of the sed tank diffuser
ND_sed_diffuser = 1 * u.inch
```


```python
#The cross-sectional area of the pipe wall is:
area_PVC = (np.pi/4) * ((pipe.OD(ND_sed_diffuser)**2)
                          - (pipe.ID_SDR(ND_sed_diffuser,SDR)**2)
                          )

#The thickness of the wall is reduced by the stretch factor:
thickness_sed_diffuser_wall = ((pipe.OD(ND_sed_diffuser)
                               - pipe.ID_SDR(ND_sed_diffuser,SDR))
                              / (2 * Pi_PVC_stretch)
                              )

# From geometry of the rectangular diffuser opening (assuming perfectly square corners) we have:
B_diffuser = ((area_PVC / (2 * thickness_sed_diffuser_wall))
                            - W_diffuser
                            ).to(u.cm)

print("Sed diffuser outer length:", B_diffuser)

S_diffuser = B_diffuser - (2 * thickness_sed_diffuser_wall)
print("Sed diffuser inner length:", S_diffuser)
```

    Sed diffuser outer length: 5.736 centimeter
    Sed diffuser inner length: 5.522 centimeter


### 4:

Each diffuser serves a certain width and length of the sedimentation tank. Assume that the diffusers are installed so that they touch each other.

* Determine the flow through each diffuser.
* Determine the velocity through each diffuser.



```python
flow_max_diffuser = V_sed_up * W_sed * B_diffuser

V_diffuser = (flow_max_diffuser
                    / (W_diffuser * S_diffuser)).to(u.m / u.s)
print('The flow of water leaving a sed tank diffuser is',flow_max_diffuser.to(u.ml/u.s))
print('The velocity of water leaving the sed tank diffuser is',V_diffuser)
```

    The flow of water leaving a sed tank diffuser is 61.19 milliliter / second
    The velocity of water leaving the sed tank diffuser is 0.349 meter / second


### 5:

What is the Reynolds number of the jet exiting the diffusers?

Note: you will likely need to force Pint to display this as a dimensionless number.


```python
Re_diffuser_jet = ((W_diffuser * V_diffuser) / pc.viscosity_kinematic(T_design)).to(u.dimensionless)
print('The Reynolds number for this jet is',Re_diffuser_jet)
```

    The Reynolds number for this jet is 974.6 dimensionless


### 6:

What is the Reynolds number of the vertical flow up through the top of the floc blanket?


```python
Re_sed = ((W_sed * V_sed_up) / pc.viscosity_kinematic(T_design)).to(u.dimensionless)
print('Reynolds number through floc is',Re_sed)
```

    Reynolds number through floc is 938.2 dimensionless


### 7:

Compare the two values for Reynolds numbers that you found for Problems 5 and 6. What do the Reynolds numbers for these very different flows tell you?

The Reynolds number is almost the same because mass conservation requires V*W to be a constant. The only difference in the Reynolds number is due to the fact that the plane jet isn't quite continuous. It is broken by twice the thickness of the pipe wall between diffusers.

### 8:
Next, we want to determine the energy dissipation rate for the flow leaving the jet reverser. For this process, you can assume that the jet remains laminar. The flow spreads to fill the gaps created by the walls of the diffuser tubes by the time it traverses the jet reverser. Jet velocity and flow rate are conserved as the jet changes direction in the jet reverser.

* Calculate the thickness of the jet after it does the 180 degree bend of the jet reverser.
* Calculate the energy dissipation rate for the flow leaving the jet reverser.

Convert your final answer to milliwatts per kilogram.


```python
#Calculate the thickness of the jet when it leaves the diffuser. B_diff = S_diff

W_jet_reversed = W_sed * V_sed_up / V_diffuser

#Calculate the maximum energy dissipation rate

EDR_inlet_jet = (((Pi_jet_plane * V_diffuser)**3)
                        / W_jet_reversed).to(u.mW / u.kg)


print('The energy dissipation rate for inlet jet is', EDR_inlet_jet)
```

    The energy dissipation rate for inlet jet is 158.5 milliwatt / kilogram


### 9:

In desiging AguaClara plants, it is critical to account for all forms of significant head loss. In the sedimentation tank, effluent launders provide about 4 cm of head loss. We want to calculate the exit head loss for water leaving the diffusers to determine whether it is a significant addition to the total head loss through the sedimentation tank.

Calculate this diffuser exit head loss in two ways.
* First, calculate the head loss making sure to account for the upflow velocity in the sed tank.
* Second, calculate the head loss but assume that the upflow velocity is negligible.

* Is it reasonable to neglect the upflow velocity in the sed tank when calculating this head loss?

$$ h_e = \frac{\left( {{V_{in}} - {V_{out}}} \right)^2}{2g} $$

You will find that the exit head loss for water leaving the diffuser is high enough that we need to account for head loss in the sed tank inlet piping for our designs.


```python
hl_sed_diffuser_exit1 = (((V_diffuser - V_sed_up) ** 2) / (2 *g)).to(u.cm)

hl_sed_diffuser_exit2 = (((V_diffuser) ** 2) / (2 *g)).to(u.cm)

hl_sed_diffuser_error=(hl_sed_diffuser_exit2-hl_sed_diffuser_exit1)/hl_sed_diffuser_exit1

print('The best estimate of the exit head loss for the diffuser is', hl_sed_diffuser_exit1)
print('The 2nd estimate of the exit head loss for the diffuser ignoring the upflow velocity is', hl_sed_diffuser_exit2)
print('It is reasonable to neglect the effect of the upflow velocity. The error is',hl_sed_diffuser_error)
```

    The best estimate of the exit head loss for the diffuser is 0.6176 centimeter
    The 2nd estimate of the exit head loss for the diffuser ignoring the upflow velocity is 0.6211 centimeter
    It is reasonable to neglect the effect of the upflow velocity. The error is 0.005755 dimensionless


## Manifold and Launders

Flow distribution between and within sedimentation tanks is an important design component to ensure good sedimentation performance. We need to distribute flow uniformly between sedimentation tanks and also between diffusers on the inlet manifolds.

The following variable definitions and equations will be useful in answering later questions.
* ${hl}_{ParallelPath}$ is the head loss (flow resistance) in the parallel paths leaving the manifold. The head loss in the parallel path is the total head loss from where the flow leaves the manifold to the point where the parallel flows reunite.
* $\Delta{H}_{Manifold}$ is the variability in piezometric head in the manifold that is driving the flow through the parallel paths.

* The ratio of minimum (first diffuser port) to maximum (last diffuser port) flow is given by:

$$\Pi_{DiffuserFlow} = \sqrt{\frac{{hl}_{ParallelPath} -  \frac{\Delta{H}_{Manifold}}{2}}{{hl}_{ParallelPath} + \frac{\Delta{H}_{Manifold}}{2}}}$$

* The change in piezometric head is given by:
$$\Delta{H}_{Manifold} = \frac{{{Velocity}_{Manifold}}^{2}}{2g}$$

* The maximum allowable velocity in the manifold is given by:

$${\Pi_{DiffuserFlow}}^{2} * \left({hl}_{ParallelPath} + \frac{\Delta{H}_{Manifold}}{2} \right) = {hl}_{ParallelPath} -  \frac{\Delta{H}_{Manifold}}{2}$$

$$\left({\Pi_{DiffuserFlow}}^{2} - 1 \right) {hl}_{ParallelPath} + \left({\Pi_{DiffuserFlow}}^{2} + 1 \right) \frac{\Delta{H}_{Manifold}}{2} = 0$$

$$\left(\frac{1 - {\Pi_{DiffuserFlow}}^{2}}{{\Pi_{DiffuserFlow}}^{2} + 1} \right) {hl}_{ParallelPath} =  \frac{\Delta{H}_{Manifold}}{2}$$

$$\left(\frac{1 - {\Pi_{DiffuserFlow}}^{2}}{{\Pi_{DiffuserFlow}}^{2} + 1} \right) {hl}_{ParallelPath} = \frac{{{Velocity}_{Manifold}}^{2}}{4g}$$

### 10:

Now, we want to find the maximum velocity for an inlet manifold which is dependent on the given flow distribution constraint, $\Pi_{DiffuserFlow}$, and the head loss in the parallel paths, ${hl}_{ParallelPath}$.

* Determine the relationship between diffuser exit velocity and the head loss in the parallel paths.
* Determine an equation for maximum velocity for an inlet manifold in terms of diffuser exit velocity and the flow distribution constraint.
* Write a **function** for maximum velocity for an inlet manifold using the equations you just found.


Exit losses from the diffusers dominate the head loss because the velocity in the diffuser slots is much higher than the velocity at the entrance to the diffuser pipes. Using the insight from the previous problem, it is reasonable to neglect the effect of the upflow velocity when calculating the exit head loss for the manifold diffusers.


```python
#h_jet = V_jet^2/(2*g)

def Vel_sed_manifold_max(Pi_diffuser_flow, V_diffuser):
    return (V_diffuser * np.sqrt(2 * ((1-(Pi_diffuser_flow**2))
                                          / ((Pi_diffuser_flow**2)+1)
                                          )
                                     ))
```

### 11:
Head loss in the sedimentation tank is impacted by multiple forms of head loss, inlcuding head loss through the effluent launder and diffusers. Head loss through the effluent launder is about 4 cm. You found head loss through the diffusers in Problem 9.  
* Which form of head loss (effluent launder or diffuser) is in the parallel path, ${hl}_{ParallelPath}$?

Use the function that you wrote for Problem 10 to calculate the maximum velocity in the inlet manifold of the sedimentation tank.
* Use the value for `Pi_sed_manifold_flow` given above.
* Use the diffuser exit velocity you found in Problem 4.



```python
print("Only the diffuser head loss is in the parallel paths.")

V_sed_manifold_max = Vel_sed_manifold_max(Pi_sed_manifold_flow, V_diffuser)

print('The maximum velocity in the sedimentation tank manifold is',V_sed_manifold_max)
```

    Only the diffuser head loss is in the parallel paths.
    The maximum velocity in the sedimentation tank manifold is 0.2313 meter / second


### 12:
The ratio of manifold pipe cross-sectional area to total diffuser cross-sectional area determines the flow distribution between diffusers.

* Calculate the ratio of manifold pipe cross-sectional area to total diffuser cross-sectional area. You can use the velocities of the manifold and the diffusers to calculate the areas.
* What is the significance of the flow area ratio that you found? What does it tell you about the relative areas?

Note: the flow distribution will be more uniform if the diffuser velocity is higher than the manifold velocity.


```python
print('The flow area ratio of manifold pipe to diffusers is',(V_diffuser / V_sed_manifold_max).to(u.dimensionless))
print("This means that the manifold flow area is larger than the total diffuser area.")
```

    The flow area ratio of manifold pipe to diffusers is 1.509 dimensionless
    This means that the manifold flow area is larger than the total diffuser area.


### 13:

The maximum sed tank flow rate is currently set by the constraint of using a single length of pipe for the manifold and launder. The maximum length of the upflow region of the sedimentation tank is 5.8 m, as given below.
* What is the corresponding sedimentation tank flow rate?


```python
L_sed_upflow_max = 5.8 * u.m
```


```python
flow_sed_max = (L_sed_upflow_max * V_sed_up * W_sed).to(u.L / u.s)
print("The maximum flow rate in one sedimentation tank is",flow_sed_max)
```

    The maximum flow rate in one sedimentation tank is 6.187 liter / second


### 14:
The maximum sed tank flow rate dictates the required pipe diameter for the manifold and launder.  

* What is the minimum inner diameter of the sedimentation tank manifold?
* What is the required nominal pipe diameter given this flow rate? Use the `pipe.ND_SDR_available` function.

SDR is the same as given in Problem 3 (SDR = 26).


```python
D_sed_manifold_min= pc.diam_circle(flow_sed_max / V_sed_manifold_max)

ND_sed_manifold = pipe.ND_SDR_available(D_sed_manifold_min, SDR)

print('The minimum inner diameter of the sedimentation tank manifold is',D_sed_manifold_min.to(u.inch))
print('The nominal diameter of the sedimentation tank manifold is',ND_sed_manifold)
```

    The minimum inner diameter of the sedimentation tank manifold is 7.266 inch
    The nominal diameter of the sedimentation tank manifold is 8 inch


## Sedimentation Tank Bays and Number of Diffusers


### 15:

What is the total required plan area for the sedimentation tanks? Calculate this using the design flow rate and the upflow velocity between the floc blanket and plate settlers.

Give your final answer in square meters.


```python
A_sed_flocblanket_total = (flow_plant / V_sed_up).to(u.m**2)

print('The plant view area of the floc blanket is',A_sed_flocblanket_total)
```

    The plant view area of the floc blanket is 60 meter ** 2


### 16:

What is the total length of the floc blanket zone for all tanks? Calculate this using the total required plan area for the sedimentation tank and the sedimentation tank width.

This total length will enable you to calculate how many sed tanks are required.


```python
L_sed_flocblanket_total = (A_sed_flocblanket_total / W_sed).to(u.m)

print(L_sed_flocblanket_total)
```

    56.24 meter


### 17:

How many sedimentation tanks are required to treat the total plant flow? Calculate this using the the total plant flow rate and the maximum sed tank flow rate. The plant flow rate is the basis of design and the maximum sed tank flow rate is based on the manifold diameter.

Your answer should be an integer value.



```python
N_sed_tanks = int(np.ceil(flow_plant / flow_sed_max))

print('The required number of sedimentation tanks is',N_sed_tanks)
```

    The required number of sedimentation tanks is 10


### 18:

How much water (in L/s) can all of the sedimentation tanks for the plant treat? Assume that all tanks have been built to maximum length.


```python
flow_sed_tanks_total = flow_sed_max * N_sed_tanks

print(flow_sed_tanks_total)
```

    61.87 liter / second


### 19:

How many diffusers are required in each tank? Assume the maximum length of the upflow region of the sedimentation tank is used. Use the `np.floor` function to round down to an integer value.


```python
N_sed_tank_diffusers = int(np.floor(((L_sed_flocblanket_total/N_sed_tanks) / B_diffuser).to(u.dimensionless)))

print('The number of diffuser pipes per sed tank is',N_sed_tank_diffusers)
```

    The number of diffuser pipes per sed tank is 98


## Plate Settlers

You may assume that the active area of the sedimentation tank is equal to the top area of the floc blanket zone. This isn't quite right because of the geometric constraints from the floc hopper, inlet channel, settled water channel, and angled plates. However, it is a good approximation for these long tanks. We will use this approximation to determine the plate settler details.

### 20:

What is the required length of the plate settlers? Do not neglect the thickness of the plate settlers.


```python
L_sed_plate = ((s_sed_plate * ((V_sed_up/V_sed_capture)-1)
                  + thickness_sed_plate * (V_sed_up/V_sed_capture))
                 / (np.sin(angle_sed_plate) * np.cos(angle_sed_plate))
                 ).to(u.m)

print('The minimum length of the plate settlers is',L_sed_plate)
```

    The minimum length of the plate settlers is 0.4619 meter


### 21:

What is the horizontal spacing (center to center) of the plate settlers?


```python
B_sed_plate_horizontal = ((thickness_sed_plate + s_sed_plate)
                                    / np.sin(angle_sed_plate)).to(u.cm)

print('The horizontal center to center spacing of the plate settlers is',B_sed_plate_horizontal)
```

    The horizontal center to center spacing of the plate settlers is 3.118 centimeter


### 22:

Approximately how many plate settlers spaces are needed in each sedimentation tank? Assume the maximum length of the upflow region of the sedimentation tank is used. Neglect the lost space at the end of the sedimentation tank due to the angle of the plate settlers.

Round your answer to the closest integer value.


```python
N_sed_plates_pertank = int(round((((L_sed_flocblanket_total/N_sed_tanks) / B_sed_plate_horizontal)).to(u.dimensionless)))
print('The number of plate settlers per sedimentation tank is',N_sed_plates_pertank)
```

    The number of plate settlers per sedimentation tank is 180


Congratulations on making it this far! Although we haven't designed every component in the sedimentation tank, you have a good idea of the analysis that is required for systematic parametric design. We have not covered the topics of the inlet channel, the launder that removes clean water from the top of the sedimentation tank, the floc weir or floc hopper, or the system of equations used to calculate the final depth of the sedimentation tank. The detailed design required to create a high-performing sedimentation tank is sophisticated, complicated, and if you are successful the resulting sedimentation tank is high-performing and easy to maintain!
