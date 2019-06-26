# Sedimentation/Filtration Design Challenge
The aguaclara code does not yet design a sedimentation tank. Here we will do design a few of the elements of the sedimentation tank and you will need to code some of these functions. Then we will explore the design of the diffuser system.

```python
import aguaclara
import aguaclara.core.physchem as pc
import aguaclara.core.head_loss as minorloss
import aguaclara.core.pipes as pipes
import aguaclara.design.human_access as ha
import aguaclara.core.constants as con
from aguaclara.core.units import unit_registry as u
import aguaclara.core.utility as ut
import numpy as np
import matplotlib.pyplot as plt


```



## Assumptions.

```python
# We've set a maximum head loss in the sedimentation tank inlet: The total head loss through a filter includes about 4 cm through the effluent launder orifices. The inlet head loss is kept smaller because there is no need for much energy to keep the floc blanket in suspension.
Inlet_max_HL = 1 * u.cm
# Design temperature will be helpful to calculate viscosity
Design_T = 15*u.degC
# Plant Flowrate:
Plant_Q = 60 * u.L/u.s
# Upflow velocity at the top of the floc blanket:
Up_V = 1 * u.mm/u.s
# The corrugated plastic sheets used to make the plate settlers:
Bay_W = 42 * u.inch
# Thickness of the plate settler material
Plate_thickness = 2 * u.mm
# The plate settlers are angled 60° from the horizontal:
Plate_angle = 60 * u.deg
# The plate setters are spaced 2.5cm apart (this is the perpendicular
# distance between plates, not the horizontal distance between plates):
Plate_S = 2.5 * u.cm
# Plate settler capture velocity:
Capture_V = 0.12 * u.mm/u.s
# Maximum length of the floc blanket in a sed tank
Manifold_ND = 8 * u.inch
```

### 1)
If all of the head loss of the inlet manifold (Inlet_max_HL) is in the exit velocity of the diffusers, then what is the maximum velocity of the diffuser jet? Note that there isn't a _vena contracta_ here!


### 2)
The plane (or line) jet created by the diffusers runs the entire length of the sedimentation tank. The sedimentation tank is Bay_W wide. Use mass conservation to calculate the required width of the plane jet (the width of the diffuser nozzle). For this analysis we will neglect the fact that the jet is split up by the wall thickness of the diffusers. You can see a diffuser (Figure 1) and a sed tank (Figure 2) showing how the diffusers are installed to form a line jet. The hyperlinks take you to Onshape where you can play with the objects.

[![diffuser](https://github.com/AguaClara/CEE4520/raw/master/DC/images/Diffuser.PNG)](https://cad.onshape.com/documents/1da857cd8d2957d4ee1de2d5/w/39291033c8827a7062da5d6c/e/898bb56ee9901be34c446a7e?configuration=Diffuser_Length%3D0.15%2Bmeter%3BDiffuser_OD%3D0.025400000000000002%2Bmeter%3BDiffuser_OuterOpeningLength%3D0.05736%2Bmeter%3BDiffuser_SDR%3D26.0%3BDiffuser_WidthOpening%3D0.00317%2Bmeter)

Figure 1.  [Diffuser](https://cad.onshape.com/documents/1da857cd8d2957d4ee1de2d5/w/39291033c8827a7062da5d6c/e/898bb56ee9901be34c446a7e?configuration=Diffuser_Length%3D0.15%2Bmeter%3BDiffuser_OD%3D0.025400000000000002%2Bmeter%3BDiffuser_OuterOpeningLength%3D0.05736%2Bmeter%3BDiffuser_SDR%3D26.0%3BDiffuser_WidthOpening%3D0.00317%2Bmeter) showing the transition for 1" PVC pipe to rectangular geometry that is used to create a line jet.


[![diffuser](https://github.com/AguaClara/CEE4520/raw/master/DC/images/Sed.PNG)](https://cad.onshape.com/documents/1da857cd8d2957d4ee1de2d5/w/39291033c8827a7062da5d6c/e/c07b390baeda1b509a449bb4?configuration=default)

Figure 2.  [Sed tank showing the continuous row of diffusers.](https://cad.onshape.com/documents/1da857cd8d2957d4ee1de2d5/w/39291033c8827a7062da5d6c/e/c07b390baeda1b509a449bb4?configuration=default)


What is the minimum required width (small dimension) of the diffuser slot? Note that this width sets the maximum size of particles that the sedimentation tank can handle. Larger particles must be captured by the screen in the entrance tank.


### 3)
We will neglect the small triangle at the end of the plate settlers and thus assume that the vertical velocity in the plate settlers is equal to the vertical velocity in the flow blanket. How long must be the plate settlers be to achieve the target capture velocity of 0.12 mm/s? Write a function that calculates the length of the plate settler using the equation below. Then create a graph showing the length of the plate settlers and the height of the plate settlers as a function of the spacing over a range of 5 mm to 5 cm.

$$L = \frac{
  S\left( \frac{V_{Active \uparrow}}{V_c} - 1 \right) +    T \frac{V_{Active \uparrow}}{V_c}
  } {\sin \alpha \cos \alpha}$$


We don't yet have any rational basis to choose the capture velocity. Lower capture velocity means fewer particles in the sed tank effluent, but we don't know what that performance curve looks like. We also somewhat randomly selected 2.5 cm spacing based on the goal of reducing the amount of sed tank depth dedicated to plate settlers. Now that we have preliminary evidence that deeper floc blankets would improve performance it would be beneficial to reduce the plate settler height. Should we try 1 cm plate spacing in the PF300 that is at the Cornell water filtration plant?  This is a potential new project for an AguaClara team!

## Design thinking
Both the diffuser and the plate settler designs are somewhat arbitrary. The diameter of the diffusers has been set to 1" nominal diameter. The spacing of the plate settlers has also been set to 1". You should be very skeptical about whether those are actually optimal designs!

The next questions are designed to get you thinking about what the constraints are that limit the range of viable designs for the diffusers and to see if there might be a better design.

### 4)
Analyze what happens as you vary the diameter of the diffuser by a factor of 20 in both directions. This factor of 20 is arbitrary. I simply want to get you thinking about extreme designs! Remember the key functions and the constraints of the diffuser.
 1) straighten the flow so it has no mean velocity in the horizontal direction. This requires that the L/D ratio for the diffuser by greater than about 6. This is similar to the H/S ratio for flocculators!
 2) Create a high velocity line jet that runs the entire length of the sedimentation tank that will resuspend all settled flocs.
 3) Does not exceed the allotted head loss.
 4) It must be possible to fabricate the resulting design!


Identify failures or fabrication challenges that occur if the diameter of the diffuser is too large or too small and derive and solve an equation that sets the limit for maximum and minimum diameters. Make reasonable assumptions and set constraints that you think would be important. For example, you can assume that the distance between the jet reverser and the bottom of the plate settler support system is 1 m. You can also assume that the wall thickness of the diffuser pipes is about 1 mm.

After you identify the constraints for the smallest and largest diameter diffuser pipes, then assess those two options for viability. Which option uses the least material to fabricate? How might we fabricate the option that you are proposing?

# Filtration Design Challenge


### 1)

A rapid sand filter treats settled water for 3 days before it is backwashed. The average settled water turbidity 1 NTU. The average filtered water turbidity is 0.03 NTU. The filtration velocity is 1.8 mm/s and the backwash velocity is 11 mm/s. The backwash duration is 15 minutes. Calculate the average turbidity of the backwash water.

### 2)

Explain why particles are captured at flow constrictions inside sand filters.

### 3)

Explain the role of coagulant nanoparticles in the capture of particles by flow constrictions in sand filters.

### 4)

Explain why a flow constriction in a filter has a limited capacity to collect particles.
