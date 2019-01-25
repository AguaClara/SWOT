

```python
from aide_design.play import*
from aide_design import floc_model as floc

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

# DC Hydraulic Flocculation

In this design challenge you will design a vertical flow hydraulic flocculator. You will use the flow rate of `flow_plant = 20 L/s` as your default design value.

Although we don't require that you use the nomenclature from the AguaClara variable naming guide, it provides a reasonable basis for organizing your variable names. We use the convention that the first part of the variable name describes the type of variable and always has a unique dimension. The subsequent parts of the variable name start from the big picture and slowly add more and more detail to arrive at the precise component that you are describing. Thus space_floc_baffle is the spacing between baffles in the flocculator and n_floc_channel_baffle should be the number of baffles in a flocculator channel. width_floc_channel_port should be the width of the port connecting two flocculator channels.

<span style="color:blue">**In this design challenge we will use functions to calculate each step of the design. Whenever we need to access a previously calculated result we will use the function call to access that value. Using this method of nested function calls will make the entire design be only a function of a few input parameters. **</span> This makes it possible to have flexible design code and ease the creation of new plant designs.

The minimum input parameters to define a flocculator are (flow_plant, headloss_floc_BOD, Gt_BOD, T_BOD). We could have included a longer list of input parameters (height_floc_end, width_PC_sheet, K_e, etc.) to make our functions even more general. But to keep our code more concise we will focus on only 4 of the input parameters. This will make it possible to easily change the input parameters to obtain new designs. We will use this capability to plot the results of varying the design flow rate.

## Hydraulic Vertical Flow Flocculator Design

This challenge is design a hydraulic flocculator using the core concepts of the AguaClara design methodology.

Below are the inputs for the design. BOD stands for Basis Of Design.


```python
# head loss through the flocculator
headloss_floc_BOD = 40 * u.cm

# collision potential based on recent designs for AguaClara Plants
Gt_BOD = 37000

# water depth at the end of flocculator where it flows into the inlet channel of the sedimentation tank
height_floc_end = 2 * u.m

flow_plant = 20 * u.L/u.s

# This is the estimate for larger plants where the flocculator is as long as the sedimentation tanks.
# For lower flow plants we will need to reduce this length because of the constraint that the channels must
# be wide enough to construct.
length_channel_max = 6 * u.m

# minimum and maximum ratios of distance between expansions to baffle spacing
Pi_HS_min = 3
Pi_HS_max = 6

Pi_vc = pc.RATIO_VC_ORIFICE
Pi_vc_baffle = Pi_vc**2

# width of the polycarbonate sheets used to make baffles
width_PC_sheet = 1.067*u.m

# this is a reasonable constraint to keep the channel constructable by humans
width_floc_min_BOD = width_PC_sheet / 2
width_floc_max_BOD = width_PC_sheet

# expansion minor loss coefficient for 180 degree bend
K_e = (1 / Pi_vc_baffle - 1)**2

# this is the minimum temperature of the raw water
T_BOD = 15* u.degC
```

### Design Algorithm Steps
1. Calculate the total volume of flocculator given head loss and collision potential
2. Calculate the number of channels by taking the total width and dividing by the maximum channel width
3. Calculate the channel width (total width over number of channels)
4. Calculate the minimum number of obstacles and spacing between obstacles by assuming a maximum H/S ratio
5. Use the actual H/S ratio based on obstacle spacing to calculate the spacing between baffles
6. Calculate the obstacle width to obtain the same jet expansion conditions as produced by the 180 degree bend.

This algorithm does not yet handle the integer number of baffles in a channel or the thickness of the baffles

For this assignment **create functions for each question** and then use those function calls whenever that calculation result is required in a subsequent step. Include flow_plant, headloss_floc_BOD, Gt_BOD and T_BOD as the inputs that can be varied for each function.

__Whenever you reference a previously calculated value in a function, use the function call for that value so that dependency is not broken.__

That way you will be able to easily vary any of the three main input parameters (flow, Gt, head loss) to see their effect on the design.

### 1) 

Estimate the average velocity gradient of a flocculator given head loss and collision potential. I'm going to solve this problem for you so you see how to use function calls.


```python
def G_avg(hl, Gt, T):
    G = (pc.gravity * hl) / (Gt * pc.viscosity_kinematic(T_BOD))
    return G.to(1/u.s)

print ('The average velocity gradient of flocculator is', G_avg(headloss_floc_BOD, Gt_BOD, T_BOD))
```

    The average velocity gradient of flocculator is 93.24 / second
    

### 2)
Estimate the residence time of flocculator given the target head loss and collision potential. (Note that this ignores the decrease in water depth caused by head loss. We hope to improve this design process further in the near future.)

### 3)
Plot $G\theta$ as a function of the operating temperature given the head loss and residence time for this design. In this step you are assuming that you have built this hydraulic flocculator and you want to see how the collision potential, $G\theta$, varies with temperature of operation.  Vary the temperature from 0°C to 30°C. The following equation makes it clear that the velocity gradient originates from head loss creates fluid deformation that is limited by viscosity.

$\bar G\theta  = \sqrt {\frac{{g{h_e}\theta }}{\nu }} $
$\theta$

### 4)
The following floc model equation creates the link between $\bar Gt$ and flocculator performance.

$pC^* = \frac{3}{2}\log \left( {\frac{2}{3}\pi k\frac{{d_{Clay}^2}}{{\Lambda _0^2}}\bar Gt\alpha  + 1} \right) $

What does the floc model and the graph tell you about flocculator performance and flocculator design? Explain why performance varies with temperature. 

### Your Answer/Explanation Here:

### 5)
Calculate the volume of flocculator. Note that this volume does not take into account the extra volume that flocculator will have due to the changing water level caused by the head loss. Simply estimate the volume based on the residence time and the flow rate.

### 6)
Calculate the actual length of the flocculator channels. This must meet two constraints. First, it must be less than or equal to the maximum channel length. Second, the channel length is limited by the flocculator volume, height, minimum number of channels, and minimum width of the channels. This second constraint is important for low flow rates so that the flocculator has the correct target volume. Make sure to use this floc channel length in subsequent calculations.

### 7)
Calculate the combined total width of the flocculator channels (not including walls) based on the given length and depth.

### 8)
Calculate the minimum channel width required to achieve H/S>3. The channel can be wider than this, but this is the absolute minimum width for a channel. The minimum width occurs when there is only one expansion per baffle and thus the distance between expansions is the same as the depth of water at the end of the flocculator.

${W_{Min}} = \frac{{\Pi _{HS}}Q}{H_e}{\left( {\frac{K_e}{2{H_e}\nu {\bar G}^2}} \right)^{\frac{1}{3}}}$

### 9)
What is the minimum channel width given the additional constraint that it be constructable? Use the max function to find the true minimum channel width given both constraints.

### 10)
Calculate the number of channels by taking the total flocculator width (see step 7) and dividing by the minimum channel width (round down). Include the requirement that the number of channels must be even (Use the numpy floor function - look it up!). To make this function robust, make sure that it can't ever return zero channels (the max function might be useful here)! You can convert the float to an integer with the int() function.

### 11)
Calculate the actual channel width based on the number of channels the total flocculator width.

### 12)
Calculate the *maximum* distance between expansions. This occurs for the largest allowable H/S ratio. Note that this isn't accounting for the integer requirement for the number of baffle spaces per channel yet.

${H_{{e_{Max}}}} = {\left[ {\frac{{{K_e}}}{{2\nu {{\bar G}^2}}}{{\left( {\frac{{Q{\Pi _{H{S_{Max}}}}}}{W}} \right)}^3}} \right]^{\frac{1}{4}}}$

### 13)
Calculate the minimum number of expansions per baffle space.

### 14)
Calculate the actual distance between expansions given the integer requirement for the number of expansions per flocculator depth.

### 15)
Calculate the spacing between baffles based on the target velocity gradient.


$ {S} = {\left( {\frac{{{K_e}}}{{2\nu {{\bar G}^2}}{H_{{e}}}}} \right)^{\frac{1}{3}}}     \frac{Q}{W}$

### 16)
How many baffle spaces would fit in the channel(s) given the length of the flocculator and the baffle spacing? Round to the nearest integer.

### 17)
How many baffle spaces are needed to create the required collision potential? Note that this isn't necessarily the same number as found in Problem 16. Calculating the collision potential per baffle space is the advised first step.

### 18)
Do the two estimates of the number of baffle spaces agree?

### 19)
 Calculate the average velocity of the water in the flocculator. This is the velocity after the flow has expanded through each baffle/obstacle.

### 20)
Calculate the depth of water at the beginning of the flocculator based on the design head loss.

### 21)
Estimate the residence time in the hydraulic flocculator taking head loss into account. It is okay if your estimate doesn't capture all of the details of the flocculator. You don't need to account for the volume of the baffles. Simply account for the added water due to head loss. You can approximate the extra depth as a triangle.

### 22)
Create plots showing number of channels, number of expansions per water depth, total number of baffles, and channel width for a flow range from 10-100 L/s. Note that the functions that we created in this design challenge are not able to handle arrays as inputs. Use `for` loops to create the numpy arrays of y data needed for these graphs. 
Use 100 points to define each plot. Remember to initialize the numpy arrays before 

### 23)
Read from the graphs to determine

1. At what flow rate is it no longer necessary to add extra obstacles in the flocculator?
1. At what flow rate does the flocculator switch from 2 channels to 4 channels?
1. **Why** did the flocculator switch from 2 to 4 channels?

**Your responses here:**

1. 
1. 
1. 

### 24)
Change Gt_BOD to 20,000 and run the code again. Identify at least 3 changes in the design.

**Your responses here:**

1. 
1. 
1. 

