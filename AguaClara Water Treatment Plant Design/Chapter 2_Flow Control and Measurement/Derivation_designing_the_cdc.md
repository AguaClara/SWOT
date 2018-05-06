# Deriving the Design Equations for the Linear Dose Controller/Chemical Dose Controller
This document will include the equation derivations required to design a CDC system. The most important restriction in this design process is maintaining linearity between head $h$ and flow $Q$, which is the entire purpose of the CDC. Recall that major losses under laminar flow scale with $Q$ and minor losses scale with $Q^2$ Since it is impossible to remove minor losses from the system entirely, we will simply try to make minor losses very small compared to major losses. The CDC does this by including 'dosing tube(s),' which are long, straight tubes designed to generate a lot of major losses. There can be one tube or multiple, depending on the design conditions.

We will use the 'head loss trick' that was introduced in the Fluids Review section. Therefore, the elevation difference between the water level in the constant head tank (CHT) and the end of the tube connected to the slider, $\Delta h$, is equal to the head loss between the two points, $h_L$. Thus, $\Delta h = h_L = h_e + h_f$.

**Note:** This document contains colored equations. If you are viewing this in Atom, which is recommended, consider using a 'Light' syntax theme instead of a 'Dark' one. To do so, open your settings with `ctrl` + `,`, select 'Themes', and change the 'Syntax Theme'

**Note:** There are a lot of equations in this document, and they may quickly get confusing. They are color coded in an attempt to make them easier to follow. There are two final design equations, $\color{purple}{V_{Max}}$ and $\color{purple}{L_{Min}}$, and they will be written in $\color{purple}{\rm{purple \, text \, coloring}}$ to make them noticeable.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/CDC_derivation.jpg?raw=true" width=650>

## CDC Design Equation Derivation
**When designing the CDC, there are a few parameters which are picked and set initially, before applying any equations. These parameters are:**  

1. $D$ = tube diameter. only certain tubing diameters are manufactured (like $\frac{x}{16}$ inch), so an array of available tube diameters is set initially.  
2. $\sum K_e$ = sum of minor loss coefficients for the whole system. This is also set initially, it is usually 2.  
3. $h_{L_{Max}}$ = maximum elevation difference between CHT water level and outlet of solution. This parameter is usually 20 cm.


We begin by defining the head loss through the system $h_L$, which is equivalent to defining the driving head $\Delta h$. Major losses will be coded as red.

$$\color{red}{
  h_{\rm{f}} = \frac{128\nu LQ}{g\pi D^4}
  }$$

Such that:  
$\nu$ = kinematic viscosity _of the solution going through the dosing tube(s)_. This is either coagulant or chlorine  
$Q$ = flow rate through the dosing tube(s)  
$L$ = length of the dosing tube(s)    

**Note:** 'Tube(s)' is used because there may be 1 or more dosing tubes depending on the particular design.  

Minor losses are equal to:

$$ h_e = \frac{8 Q^2}{g \pi^2 D^4} \sum{K_e} $$

Therefore, the total head loss is a function of flow, and is shown in the following equation.

$$ h_L(Q) =
\color{red}{
  \frac{128\nu L Q}{g \pi D^4} \
  }
  + \frac{8Q^2}{g \pi ^2 D^4} \sum{K_e} $$

Blue will be used to reference _actual_ head loss from now on. This is the same equation as above.

$$\color{blue}{
  h_L(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q}{g \pi ^2 D^4} \sum{K_e} \right) Q
  }$$

This equation is not linear with respect to flow. We can make it linear by turning the variable $Q$ in the $\frac{8Q}{g \pi ^2 D^4} \sum{K_e}$ term into a constant. To do this, we pick a maximum flow rate of coagulant/chlorine through the dose controller, $Q_{Max}$, and put that into the term in place of $Q$. The term becomes $\frac{8Q_{Max}}{g \pi ^2 D^4} \sum{K_e}$, and our linearized model of head loss, coded as green, becomes:

$$\color{green}{
  h_{L_{linear}}(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q_{Max}}{g \pi ^2 D^4} \sum{K_e} \right) Q
  }$$

Here is a plot of the three colored equations above. Our goal is to minimize the minor losses in the system; to bring the red and blue curves as close as possible to the green one.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/CDC_linearity_model.jpg?raw=true" width=850>

### Designing for the error constraint, $\Pi_{Error}$

**The first step in the design is to make sure that major losses far exceed minor losses. This will result in an equation for the maximum velocity that can go through the dosing tube(s), $\color{purple}{V_{Max} }$.**

Minor losses will never be 0, so how much error in our linearity are we willing to accept? Let's define a new parameter, $\Pi_{Error}$, as the maximum amount of error we are willing to accept. We are ok with 10% error or less, so $\Pi_{Error} = 0.1$.

$$ \Pi_{Error} = \frac{\color{green}{ h_{Linear} } - \color{blue}{ h_L }}{\color{green}{ h_{Linear} }} = 1 - \frac{\color{blue}{ h_L }}{\color{green}{ h_{Linear} }}$$

$$ 1 - \Pi_{Error} = \frac{\color{blue}{ h_L }}{\color{green}{ h_{Linear} }}$$

If we plug $\color{blue}{ h_L(Q) }$ and $\color{green}{ h_{L_{linear}} }$ back into the equation for $1 - \Pi_{Error}$ and take the limit as $Q \rightarrow 0$, we get the following:

$$1 - \Pi_{Error} =
  \frac{ \color{blue}{
  \left( \frac{128 \nu L}{g \pi D^4} +
  \rlap{\Bigg/ \Bigg/ \Bigg/ \Bigg/} \frac{8Q}{g \pi^2 D^4} \sum{K_e}
  \right)
  }}   
  {\color{green}{
  \left( \frac{128 \nu L}{g \pi D^4} + \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e} \right)
  }}     
  =     \frac{\left( \frac{128 \nu L}{g \pi D^4} \right)}{\left( \frac{128 \nu L}{g \pi D^4} + \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e} \right)}$$

The next steps are algebraic rearrangements to solve for $L$. This $L$ describes the _minimum_ length of dosing tube necessary to meet our error constraint at _maximum_ flow. Thus, we will refer to it as $L_{Min, \, \Pi_{Error}}$.

$$ \left( 1 - \Pi_{Error} \right)  \frac{128 \nu L}{g \pi D^4} + \left( 1 - \Pi_{Error} \right) \frac{8 Q_{Max}}{g \pi ^2 D^4} \sum{K_e}  =  \frac{128 \nu L}{g \pi D^4}$$

$$ - \Pi_{Error} \frac{128 \nu L}{g \pi D^4} + \left( 1 - \Pi_{Error} \right) \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e}  = 0$$

$$L = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{Q_{Max}}{16 \nu \pi} \sum{K_e} $$

$$L_{Min, \, \Pi_{Error}} = L = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{Q_{Max}}{16 \nu \pi} \sum{K_e} $$

Note that this equation is independent of head loss.   
Unfortunately, both $L_{Min, \, \Pi_{Error}}$ and $Q_{Max}$ are unknowns. We can plug this equation for $L_{Min, \, \Pi_{Error}}$ back into the head loss equation at maximum flow, which is $h_{L_{Max}} = \left( \frac{128\nu L Q_{Max}}{g \pi D^4} + \frac{8Q_{Max}^2}{g \pi ^2 D^4} \sum{K_e} \right)$ and rearrange for $Q_{Max}$ to get:

$$ Q_{Max} = \frac{\pi D^2}{4} \sqrt{\frac{2 h_{L_{Max}} g \Pi_{Error}}{\sum K_e }}$$
**Function in aide_design:** `cdc.max_linear_flow(Diam, HeadlossCDC, Ratio_Error, KMinor)` Returns the maximum flow $Q_{Max}$ that can go through a dosing tube will making sure that linearity between head loss and flow is conserved.


From this equation for $Q_{Max}$, we can get to our first design equation, $\color{purple}{V_{Max}}$ by using the continuity equation $V_{Max} = \frac{Q_{Max}}{\frac{\pi D^2}{4}}$

$$\color{purple}{
  V_{Max} = \sqrt{ \frac{2 h_L g \Pi_{Error}}{\sum{K_e} }}
  }$$

### Designing for the proper amount of head loss, $h_{L_{Max}}$

**The second step in the design is to make sure that the maximum head loss corresponds to the maximum flow of chemicals. This will result in an equation for the length of the dosing tube(s), $\color{purple}{L_{Min} }$.**

We previously derived an equation for the minimum length of the dosing tube(s), $L_{Min, \, \Pi_{Error}}$, which was the minimum length needed to ensure that our linearity constraint was met. This equation is shown again below, in red:

$$\color{red}{
  L_{Min, \, \Pi_{Error}} = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{Q_{Max}}{16 \nu \pi} \sum{K_e}
  }$$

This equation does not, however, account for getting to the proper amount of head loss. If we were to use this equation to design the dosing tubes, we might not end up with the proper amount of flow $Q_{Max}$ at the maximum head loss $h_{L{Max}}$. So we need to double check to make sure that we get our desired head loss.

First, consider the head loss at maximum flow that was used to get the equation for $Q_{Max}$:

$$ h_{L_{Max}} = \left( \frac{128 \nu L{Q_{Max}}}{g \pi D^4} + \frac{8 Q_{Max}^2}{g \pi^2 D^4} \sum{K_e} \right)$$

Now that we know all of the parameters in this equation except for $L$, we can solve the equation for $L$. This the _shortest_ tube that generates our required head loss, $h_{L_{Max}}$.

$$\color{green}{
L_{Min, \, head loss} = L = \left( \frac{g h_{L_{Max}} \pi D^4}{128 \nu Q_{Max}} - \frac{Q_{Max}}{16 \pi \nu} \sum{K_e} \right)
}$$
**Functions in aide_design:**   
`cdc._length_cdc_tube_array(FlowPlant, ConcDoseMax, ConcStock, DiamTubeAvail, HeadlossCDC, temp, en_chem, KMinor)` Returns $\color{purple}{L_{Min}}$, takes in the flow rate input of _plant design flow rate_.  
`cdc._len_tube(Flow, Diam, HeadLoss, conc_chem, temp, en_chem, KMinor)` Returns $\color{purple}{L_{Min}}$, takes in the flow rate input of _max flow rate through the dosing tube(s)_.

If you decrease the max flow $Q_{Max}$ and hold $h_{L_{Max}}$ constant, $\color{green}{L_{Min, \, head loss}}$ becomes larger. This means that a CDC system for a plant of 40 $\frac{L}{s}$ must be different than one for a plant of 20 $\frac{L}{s}$. If we want to maintain the same head loss at maximum flow in both plants, then the dosing tube(s) will need to be a lot longer for the 20 $\frac{L}{s}$ plant.

To visualize the distinction between $\color{red}{
  L_{Min, \, \Pi_{Error}}}$ and $\color{green}{
L_{Min, \, head loss}}$, see the following plot. $\color{green}{
L_{Min, \, head loss}}$ is discontinuous because it takes in the smallest allowable tube diameter as an input. As the chemical flow rate through the dosing tube(s) decreases, the dosing tube diameter does as well. Whenever you see a jump in the green points, that means the tubing diameter has changed.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/CDC_length_model.jpg?raw=true" width=800>

As you can see, the head loss constraint is more limiting than the linearity constraint when designing for tube length. Therefore, the design equation for tube length is the one which accounts for head loss. This is the second and final design equation for designing the CDC:

$$\color{purple}{
L_{Min} = L_{Min, \, head loss} = \left( \frac{g h_{L_{Max}} \pi D^4}{128 \nu Q_{Max}} - \frac{Q_{Max}}{16 \pi \nu} \sum{K_e} \right)
}$$


***
### The equations for $\color{purple}{V_{Max}}$ and $\color{purple}{L_{Min}}$ are the only ones you _**need**_ to manually design a CDC.
***

## CDC Dosing Tube(s) Diameter $D_{Min}$ Plots
 Below are equations which also govern the CDC and greatly aid in understanding the physics behind it, but are not strictly necessary in design.

 By rearranging  $Q_{Max} = \frac{\pi D^2}{4} \sqrt{\frac{2 h_L g \Pi_{Error}}{\sum K_e }}$, we can solve for $D$ to get the _minimum_ diameter we can use assuming the shortest tube possible that meets the error constraint, $\color{red}{L_{Min, \, \Pi_{Error}}}$. If we use a diameter smaller than $D_{Min, \, \Pi_{Error}}$, we will not be able to simultaneously reach $Q_{Max}$ and meet the error constraint $\Pi_{Error}$.

$$\color{blue}{
D_{Min, \, \Pi_{Error}} = \left[ \frac{8 Q^2 \sum K_e}{\Pi_{Error} h_l g \pi^2} \right]^{\frac{1}{4}}
}$$

We can also find the minimum diameter needed to guarantee laminar flow, which is another critical condition in the CDC design. We can do this by combining the equation for Reynolds number at the maximum $\rm{Re}$ for laminar flow, ${\rm{Re}}_{Max} = 2100$ with the continuity equation at maximum flow:

$${\rm Re}_{Max}  = \frac{V_{Max} D}{\nu}$$

$$V_{Max} = \frac{4 Q_{Max}}{\pi D^2}$$

To get:

$$\color{red}{
D_{Min, \, Laminar} = \frac{4 Q_{Max}}{\pi \nu {\rm{Re}}_{Max}}
}$$

Combined with the discrete amount of tubing sizes (shown in dark green), we can create a graph of the three diameter constraints:

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/CDC_diameter_model.jpg?raw=true" width=800>
