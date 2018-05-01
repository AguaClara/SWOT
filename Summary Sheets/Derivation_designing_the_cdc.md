# Deriving the Design Equations for the Linear Dose Controller/Chemical Dose Controller
This document will include the equation derivations required to design a CDC system. The most important restriction in this design process is maintaining linearity between head $h$ and flow $Q$, which is the entire purpose of the CDC. Recall that major losses under laminar flow scale with $Q$ and minor losses always scale with $Q^2$ Since it is impossible to remove minor losses from the system entirely, we will simply try to make minor losses very small compared to major losses. The CDC does this by including 'dosing tubes,' which are long, straight tubes designed to generate a lot of major losses.

We will use the 'head loss trick' that was introduced in the Fluids Review section. Therefore, the elevation difference between the water level in the constant head tank and the end of the tube connected to the slider, $\Delta h$, is equal to the head loss between the two points, $h_L$. Thus, $\Delta h = h_L = h_e + h_f$.

**Note:** This document contains colored equations. If you are viewing this in Atom, which is recommended, consider using a 'Light' syntax theme. To do so, open your settings with `ctrl` + `,`, select 'Themes', and change 'Syntax Theme'

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/CDC_derivation.jpg?raw=true" width=650>

We begin by defining the head loss through the system $h_L$, which is equivalent to defining the driving head $\Delta h$. Major losses will be coded as red from this point onwards.

$$\color{red}{ h_{\rm{f}} = \frac{128\mu LQ}{\rho g\pi D^4} }$$

Minor losses are equal to:

$$ h_e = \frac{8 Q^2}{g \pi^2 D^4} \sum{K_e} $$

Therefore, the total head loss is a function of flow, and is shown in the following equation. Blue will be used to reference actual head loss from now on.

$$\color{blue}{ h_L(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q}{g \pi ^2 D^4} \sum{K_e} \right) Q }$$

This equation is not linear with respect to flow. We can make it linear by turning the variable $Q$ in the $\frac{8Q}{g \pi ^2 D^4} \sum{K_e}$ term into a constant. To do this, we pick a maximum flow rate of coagulant/chlorine for the dose controller, $Q_{max}$, and put that into the term. The term becomes $\frac{8Q_{max}}{g \pi ^2 D^4} \sum{K_e}$, and our linearized model of head loss, coded as green, becomes:

$$\color{green}{ h_{L_{linear}}(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q_{max}}{g \pi ^2 D^4} \sum{K_e} \right) Q }$$

Here is a plot of the three colored equations above. Our goal is to minimize the minor losses in the system; to bring the red and blue curves as close as possible to the green one.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/CDC_linearity_model.jpg?raw=true" width=650>

**The first step in the design is to figure out the parameters of the dosing tubes, to ensure that they generate enough major losses to make minor losses insignificant.**

But minor losses will never be 0, so how much error in our linearity are we willing to accept? Let's define a new parameter, $\Pi_{Error}$, as the amount of error we are willing to accept. We will accept 10% error, so $\Pi_{Error} = 0.1$.

$$ \Pi_{Error} = \frac{\color{green}{ h_{Linear} } - \color{blue}{ h_L }}{\color{green}{ h_{Linear} }} = 1 - \frac{\color{blue}{ h_L }}{\color{green}{ h_{Linear} }}$$

If we plug $\color{blue}{ h_L(Q) }$ and $\color{green}{ h_{L_{linear}} }$ back into the $\Pi_{Error}$ equation and take the limit as $Q \rightarrow 0$, we get the following:

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

This last equation describes the _minimum_ length of dosing tube necessary to meet our error constraint at _maximum_ flow.  Unfortunately, both of these terms are unknown. We can plug this equation back into the $\color{green} { h_{L_{linear}} }$ and rearrange for $Q_{max}$ to get:

$$ Q_{Max} = \frac{\pi D^2}{4} \sqrt{\frac{2 h_L g \Pi_{Error}}{\sum{K_e} }} $$

From this equation for $Q_{max}$, we can either get to an equation for $D$ by rearranging algebraically or $V_{max}$ using the continuity equation. 
