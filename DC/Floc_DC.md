# Velocity gradients and flow geometry


### 1)

Coagulant is injected in the center a long straight pipe. The pipe is 12 inches Nominal Diameter schedule 40 PVC and the flow rate is 120 L/s at $10^{\circ}C$. What distance is required for the flow to be completely mixed? Note that this estimate is based on the time required for an eddy to traverse the diameter of the pipe and that a safety factor of order 3 * pi/2 would be reasonable. Include this safety factor in the calculations. See the (equation for pipe mixing)[https://aguaclara.github.io/Textbook/Rapid_Mix/RM_Derivations.html?highlight=energy%20dissipation#equation-rapid-mix-rm-derivations-42]?
```python

from aguaclara.core.units import unit_registry as u
from aguaclara.core import physchem as pc
from aguaclara.core import pipes as pipes
from aguaclara.core import utility as ut
from aguaclara.core import constants as con
from aguaclara.research import floc_model as fm
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


```

### 2)

What is the residence time in this mixing zone?

```python

```
### 3)

How much head loss from wall shear will have occurred in the pipe in the distance measured in the previous problem? Compare this with the
```python

```

### 4)

What is the Camp Stein velocity gradient in this pipe flow?

```python

```
### 5)

What is the $G\theta$ for this mixing zone and how does it compare with the  $G\theta$ recommended for [mechanical mixing units](https://aguaclara.github.io/Textbook/Rapid_Mix/RM_Intro.html#maximum-velocity-gradients)?

```
Mix_HRT = np.array([0.5,15,25,35,85])*u.s
Mix_G = np.array([4000,1500,950,850,750])/u.s
Mix_Gt = np.multiply(Mix_HRT, Mix_G)
```

```Python


```


### 6)

What is the velocity gradient at the wall of the pipe? This will make it apparent that the velocity gradient is far from constant

```python

```
### 7)

Suppose we insert a flat plate oriented with the flat surface facing the flow inside the pipe. Let the width of the plate be 0.5 cm so it is small enough that it doesn't significantly increase the velocity in the pipe. What is the maximum velocity gradient downstream of the plate? You may neglect the fact that the velocity in the center of the turbulent pipe flow is slightly higher than the average velocity.

```python


```
### 8)
What happens to the velocity gradient if a narrower flat plate is used? Does the maximum velocity gradient increase or decrease? Just look at the equation to answer this!



# Flocculation model

### 1)
How far will two kaolin clay particles (density of 2650 $\frac{kg}{m^3}$) with a diameter of 5 $\mu m$ travel relative to each if they are in a uniform velocity gradient of 100 Hz for 400 s and separated (in the direction of the velocity gradient) by their average separation distance based on a turbidity of 0.5 NTU? (We have defined NTU as a unit based on the concentration of clay in the aguaclara distribution. Note that in a uniform velocity gradient $\bar G = G_{CS}$.

``` Python

```
### 2)

How much volume is "cleared" by these particles divided by the volume occupied by the particles? This ratio is essentially how many times these particles should have collided in the 400 s.

```python

```
The above calculations illustrate why 1 NTU is a practical limit for flocculation. Assuming that we don't want to apply so much coagulant that the clay particles are completely covered with coagulant, then some fraction of the collisions will be ineffective. Thus at 1 NTU a $G \theta$ of 40,000 might only cause one successful collisions

# Flocculator design

Below we design a flocculator using aguaclara.design.floc in the aguaclara distribution version 0.0.20 (minimum). We will use the default settings for this design except change the flow rate to 60 L/s. The available inputs that you can change are:

* Q=20 * u.L/u.s,
* temp=25 * u.degC,
* max_L=6 * u.m,
* Gt=37000,
* HL = 40 * u.cm,
* downstream_H = 2 * u.m,
* ent_tank_L=1.5 * u.m,
* max_W=42 * u.inch,
* drain_t=30 * u.min

You can set any of these parameters by including those keywords in the function call.
```
myF = floc.Flocculator(Q=60 * u.L/u.s,temp = 0 * u.degC)

```
Below is our design
``` python
import aguaclara
import aguaclara.core.physchem as pc
import aguaclara.core.head_loss as minorloss
import aguaclara.core.pipes as pipes
import aguaclara.design.human_access as ha
from aguaclara.core.units import unit_registry as u
import numpy as np
import aguaclara.design.floc as floc
Q=60 * u.L/u.s
myF = floc.Flocculator(Q=Q)

# you can either access individual parameters
print('The number of channels is', myF.channel_n)
print('The channel length is',myF.channel_L)
print('The channel width is',ut.round_sf(myF.channel_W,2))
print('The spacing between baffles is',ut.round_sf(myF.baffle_S,2))
print('The number of obstacles per baffle is', myF.obstacle_n)
print('The velocity gradient is', ut.round_sf(myF.vel_grad_avg,2))
print('The residence time used for design is',ut.round_sf(myF.retention_time,2))
print('The maximum distance between flow expansions is', ut.round_sf(myF.expansion_max_H,2))
print('The drain diameter is', myF.drain_ND)
# or you can see the entire design as a dictionary of values
myF.design
```

## Calculations and analysis

### 1)

How many expansions are there in total? Estimate this based on the spacing and flocculator size. You will have to account for the entrance tank that occupies volume in the first flocculator channel.

```Python

```

### 2)
What is the head loss per expansion? (Calculate this head loss using the minor loss equation) You can use the BAFFLE_K that is defined in the flocculator class.
```python

```

### 3)
What is the total head loss of all of the expansions? Compare this with the target head loss of 40 cm.
```Python

```

### 4)
Change the design temperature over a range that would be applicable in Ithaca (0 to 30 degC) for a flocculator design of your choice. What happens as the temperature increases? Plot residence time, velocity gradient, baffle spacing, and number of channels as functions of temperature. Explain WHY these design changes occur.

```Python


```

The water becomes more viscous as it gets colder. Thus it becomes more difficult to deform. Given that we are limiting the amount of energy that we are willing to use, we have to compensate by deforming the fluid more slowly. Thus if we hold the amount of energy available as a constant, then the velocity gradient decreases as the temperature decreases and the residence time increases. The number of channels increases as the temperature drops because the design ran up against the maximum channel width constraint as the flocculator volume increased.

### 5)
When designing a flocculator how should you select the design temperature?

Use the lowest expected temperature for the design temperature.


### 6)
We have been experimenting with flocculators that have a $G\theta$ of 20,000 and a head loss of 50 cm for use in Honduras where the minimum temperature is about 15 $^\circ C$. Create a design with these inputs and flow rates of 10 L/s and 60 L/s. To simplify the design, set the entrance tank length to zero. Note that our flocculator design algorithm currently requires there to be an even number of channels for the flocculator. The minimum width of the channels is 45 cm and thus when the flocculator volume is small the length of the flocculator is reduced.
Given these designs and given that our sedimentation tanks end up being closer to 7 m long, would you recommend that we change our plant layout to allow a single channel flocculator?
List as many design implications as you can think of for this potential change. Check out the [current cad drawing](https://cad.onshape.com/documents/5a7585ae3248902548b02541/w/349594d2eb30a283f019807e/e/add8912cf760c28f462bd04f) and identify what else would need to change if the flocculator only had one channel.


```Python

```
