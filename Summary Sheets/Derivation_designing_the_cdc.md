# Deriving the Design Equations for the Linear Dose Controller/Chemical Dose Controller
This document will include the equation derivations required to design a CDC system. The most important restriction in this design process is maintaining linearity between head $h$ and flow $Q$, which is the entire purpose of the CDC. Recall that major losses under laminar flow scale with $Q$ and minor losses always scale with $Q^2$ Since it is impossible to remove minor losses from the system entirely, we will simply try to make minor losses very small compared to major losses. The CDC does this by including 'dosing tube(s),' which are long, straight tubes designed to generate a lot of major losses. There can be one or multiple, depending on the design conditions.

We will use the 'head loss trick' that was introduced in the Fluids Review section. Therefore, the elevation difference between the water level in the constant head tank and the end of the tube connected to the slider, $\Delta h$, is equal to the head loss between the two points, $h_L$. Thus, $\Delta h = h_L = h_e + h_f$.

**Note:** This document contains colored equations. If you are viewing this in Atom, which is recommended, consider using a 'Light' syntax theme instead of a 'Dark' one. To do so, open your settings with `ctrl` + `,`, select 'Themes', and change 'Syntax Theme'

**Note:** There are a lot of equations in this document, and they may quickly get confusing. They are color coded in an attempt to make them easier to follow. There are two final design equations, $\color{purple}{V_{Max}}$ and $\color{purple}{L_{Min}}$, and they will be written in $\color{purple}{\rm{purple \, text \, coloring}}$ to make them noticeable.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/CDC_derivation.jpg?raw=true" width=650>

## CDC Design Equation Derivation
**When designing the CDC, there are a few parameters which are picked and set initially, before applying any equations. These parameters are:**  

$D$ = tube diameter. There are discrete tubing diameters in existence, so an array of available tube diameters is set initially.  
$\sum K_e$ = sum of minor loss coefficients. This is also set initially, it is usually 2.  
$h_{L_{Max}}$ = maximum elevation difference between CHT water level and outlet of solution. This parameter is usually 20 cm.



We begin by defining the head loss through the system $h_L$, which is equivalent to defining the driving head $\Delta h$. Major losses will be coded as red from this point onwards.

$$\color{red}{
  h_{\rm{f}} = \frac{128\nu LQ}{g\pi D^4}
  }$$

Such that:  
$\nu$ = kinematic viscosity _of the solution going through the dosing tube(s)_. This is either coagulant or chlorine  
$Q$ = flow rate through the dosing tube(s)  
$L$ = length of the dosing tube(s)   
$D$ = diameter of the dosing tube(s)  


Minor losses are equal to:

$$ h_e = \frac{8 Q^2}{g \pi^2 D^4} \sum{K_e} $$

Such that:  
$\sum K_e$ = sum of all minor loss coefficients between the CHT and the outlet of the solution

Therefore, the total head loss is a function of flow, and is shown in the following equation. Blue will be used to reference actual head loss from now on.

$$\color{blue}{
  h_L(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q}{g \pi ^2 D^4} \sum{K_e} \right) Q
  }$$

This equation is not linear with respect to flow. We can make it linear by turning the variable $Q$ in the $\frac{8Q}{g \pi ^2 D^4} \sum{K_e}$ term into a constant. To do this, we pick a maximum flow rate of coagulant/chlorine through the dose controller, $Q_{Max}$, and put that into the term. The term becomes $\frac{8Q_{Max}}{g \pi ^2 D^4} \sum{K_e}$, and our linearized model of head loss, coded as green, becomes:

$$\color{green}{
  h_{L_{linear}}(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q_{Max}}{g \pi ^2 D^4} \sum{K_e} \right) Q
  }$$

Here is a plot of the three colored equations above. Our goal is to minimize the minor losses in the system; to bring the red and blue curves as close as possible to the green one.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/CDC_linearity_model.jpg?raw=true" width=650>

**The first step in the design is to find the _maximum_ flow velocity through the dosing tube(s) to ensure that major losses far exceed minor losses.**

But minor losses will never be 0, so how much error in our linearity are we willing to accept? Let's define a new parameter, $\Pi_{Error}$, as the amount of error we are willing to accept. We will accept 10% error or less, so $\Pi_{Error} = 0.1$.

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

The following steps are algebraic rearrangements to solve for $L$:

$$ \left( 1 - \Pi_{Error} \right)  \frac{128 \nu L}{g \pi D^4} + \left( 1 - \Pi_{Error} \right) \frac{8 Q_{Max}}{g \pi ^2 D^4} \sum{K_e}  =  \frac{128 \nu L}{g \pi D^4}$$

$$ - \Pi_{Error} \frac{128 \nu L}{g \pi D^4} + \left( 1 - \Pi_{Error} \right) \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e}  = 0$$

$$L = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{Q_{Max}}{16 \nu \pi} \sum{K_e} $$

This last equation describes the _minimum_ length of dosing tube necessary to meet our error constraint at _maximum_ flow.  Unfortunately, both of these terms are unknowns. We can plug this equation for $L$ back into the head loss equation at $Q_{Max}$, which is $h_L = \left( \frac{128\nu L Q_{Max}}{g \pi D^4} + \frac{8Q_{Max}^2}{g \pi ^2 D^4} \sum{K_e} \right)$ and rearrange for $Q_{Max}$ to get:

$$ Q_{Max} = \frac{\pi D^2}{4} \sqrt{\frac{2 h_L g \Pi_{Error}}{\sum K_e }}$$
**Function in aide_design:** `cdc.max_linear_flow(Diam, HeadlossCDC, Ratio_Error, KMinor)` Returns $Q_{Max}$


From this equation for $Q_{Max}$, we can get to our first design equation, $\color{purple}{V_{Max}}$ by using the continuity equation $V_{Max} = \frac{Q_{Max}}{\frac{\pi D^2}{4}}$

$$\color{purple}{
  V_{Max} = \sqrt{ \frac{2 h_L g \Pi_{Error}}{\sum{K_e} }}
  }$$

The only other equation strictly necessary to design a CDC system is one for thelength of the dosing tube(s), $\color{purple}{L_{Min}}$. This is rather simple. First, consider the head loss at maximum flow that was used to get the equation for $Q_{Max}$:

$$ h_{L_{Max}} = \left( \frac{128 \nu L{Q_{Max}}}{g \pi D^4} + \frac{8 Q_{Max}^2}{g \pi^2 D^4} \sum{K_e} \right)$$

Now that we know all of the parameters in this equation except for $L$, we can solve the equation for $L$. This the _shortest_ tube that meets our linearity error constraint, $\Pi_{Error}$.

$$\color{purple}{
L_{Min} = \left( \frac{g h_{L_{Max}} \pi D^4}{128 \nu Q_{Max}} - \frac{Q_{Max}}{16 \pi \nu} \sum{K_e} \right)
}$$
**Functions in aide_design:**   
`cdc._length_cdc_tube_array(FlowPlant, ConcDoseMax, ConcStock, DiamTubeAvail, HeadlossCDC, temp, en_chem, KMinor)` Returns $L_{Min}$, take in the _plant flow rate_.  
`cdc._len_tube(Flow, Diam, HeadLoss, conc_chem, temp, en_chem, KMinor)` Returns $L_{Min}$, takes in the _max flow rate through the dosing tube(s)_.

If you decrease the flow $Q$, $\color{purple}{L_{Min}}$ becomes smaller. This is good, it means that this equation for $\color{purple}{L_{Min}}$ works at every flow rate that the CDC will experience.

***
### Those are the only two equations you _**need**_ to manually design a CDC.
***

## CDC Dosing Tube(s) Diameter $D_{Min}$ Plots
 Below are equations which also govern the CDC and greatly aid in understanding the physics behind it, but are not strictly necessary in design.

 By rearranging  $Q_{Max} = \frac{\pi D^2}{4} \sqrt{\frac{2 h_L g \Pi_{Error}}{\sum K_e }}$, we can solve for $D$ to get the _minimum_ diameter we can use assuming the shortest tube possible, $\color{purple}{L_{Min}}$. If we use a diameter smaller than $D_{Min}$, we will not be able to reach $Q_{Max}$.

$$\color{red}{
D_{Min, \, Error} = \left[ \frac{8 Q^2 \sum K_e}{\Pi_{Error} h_l g \pi^2} \right]^{\frac{1}{4}}
}$$

This is the minimum diameter needed to make sure we don't exceed our allowable linearity error, $\Pi_{Error}$. We can also find the minimum diameter needed to guarantee laminar flow, which is another critical condition in the CDC design. We can do this by combining the equation for Reynolds number at the maximum $\rm{Re}$ for laminar flow, ${\rm{Re}}_{Max} = 2100$ with the continuity equation at maximum flow:

$${\rm Re}_{Max}  = \frac{V_{Max} D}{\nu}$$

$$V_{Max} = \frac{4 Q_{Max}}{\pi D^2}$$

To get:

$$\color{blue}{
D_{Min, \, Laminar} = \frac{4 Q_{Max}}{\pi \nu {\rm{Re}}_{Max}}
}$$

Combined with the discrete amount of tubing sizes (shown in dark green), we can create a graph of the three diameter constraints:

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/CDC_diameter_model.jpg?raw=true" width=650>


## CDC Dosing Tube(s) Length $L_{Min}$ Plots
