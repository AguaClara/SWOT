# Deriving the Minor Loss Equations

This document contains the derivation of the minor loss equation using the following image as a reference. The derivation begins with a slightly simplified energy equation, in which $h_P$ and $h_T$ have been eliminated.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%201_Fluids%20Review/Images/Minor_loss_pipe.jpg?raw=true" width=600>

$$\frac{p_{in}}{\rho g} + {z_{in}} + \frac{V_{in}^2}{2g} = \frac{p_{out}}{\rho g} + z_{out} + \frac{V_{out}^2}{2g} + h_L$$

Since the elevations of the 'in' and 'out' references are the same, we can eliminate $z_{in}$ and $z_{out}$. As we are considering such a small length of pipe, we will neglect the major loss component of head loss. Thus, $h_L = h_e$. The following three equations are all the same, simply rearranged to solve for $h_e$.

$$\frac{p_{in}}{\rho g} + \frac{V_{in}^2}{2g} = \frac{p_{out}}{\rho g} + \frac{V_{out}^2}{2g} + h_e$$

$$\frac{p_{in} - p_{out}}{\rho g} = \frac{V_{out}^2 - V_{in}^2}{2g} + h_e$$

$$h_e = \frac{p_{in} - p_{out}}{\rho g} + \frac{V_{in}^2 - V_{out}^2}{2g}$$

This last equation to determine $h_e$ has four variables, and we would like it to have just one or two. Thus, we will invoke conservation of momentum in the horizontal direction across our control volume to remove some variables. The difference in momentum from the $in$ point to the $out$ point is result of the pressure difference between each end of the control volume. We will be considering the pressure at the centroid of our control surfaces, and we will neglect shear along the pipe walls. After these assumptions, our momentum equation becomes the following:

$$M_{in, \, x} + M_{out, \, x} = F_{p_{in, \, x}} + F_{p_{out, \, x}}$$

Such that:  
$M_{x}$ = momentum flowing through the control volume in the x-direction, $\frac{[M][L]}{[T]^2}$  
$F_{p_x}$ = force due to pressure acting on the boundaries of the control volume in the x-direction, $\frac{[M][L]}{[T]^2}$


Recall that momentum is mass times velocity, $mV$ with units of $\frac{[M][L]}{[T]}$, for solid bodies. Since we consider water flowing through a pipe, there is not one singular mass. Instead, there is a mass flow rate, or a mass per time indicated by $\rho Q$ ($\frac{[M]}{[T]}$). Applying the continuity equation $Q = V A$ and multiplying $\rho Q$ by $V$ to obtain the correct units, we get to the following equation for the momentum of a fluid flowing through a pipe, $M = \rho V^2 A$. The pressure force is simply the pressure at the centroid of the flow multiplied by the area the pressure is acting upon, $p  A$. To ensure correct sign convention, we will make each side of the equation negative for reasons discussed shortly. Since $V_{in} > V_{out}$, the left hand side becomes $M_{out} - M_{in}$. The reduction in velocity from $in$ to $out$ causes an increase in pressure, therefore $p_{in} - p_{out}$ will be negative. With these substitutions, the conservation of momentum equation becomes as follows:

$$\rho V_{out}^2 A_{out} - \rho V_{in}^2 A_{in} = p_{in} A_{out} - p_{out} A_{out}$$

Note that the area term attached to $p_{in}$ is actually $A_{out}$ instead of $A_{in}$, as one might think. This is because $A_{out} = A_{in}$. We chose our control volume to start a few millimeters into the larger pipe, which means that the cross-sectional area does not change over the course of the control volume.

By dividing both sides of the equation by $A_{out} \rho g$, we obtain the following equation, which contains the very same pressure term as our adjusted energy equation above. This is why we chose a negative sign convention.

$$\frac{p_{in} - p_{out}}{\rho g} = \frac{V_{out}^2 - V_{in}^2 \frac{A_{in}}{A_{out}}}{g}$$

Now, we combine the adjusted energy, momentum, and continuity equations:

$$ {\rm{Energy \, equation:}} \,\,\,  h_e = \frac{p_{in} - p_{out}}{\rho g} + \frac{V_{in}^2 - V_{out}^2}{2g}$$  

$$ {\rm{Momentum \, equation:}} \,\,\, \frac{p_{in} - p_{out}}{\rho g} = \frac{V_{out}^2 - V_{in}^2 \frac{A_{in}}{A_{out}}}{g}$$

$$ {\rm{Continuity \, equation:}} \,\,\, \frac{A_{in}}{A_{out}} = \frac{V_{out}}{V_{in}}$$

To obtain an equation for minor losses with just two variables, $V_{in}$ and $V_{out}$.

$$ h_e = \frac{V_{out}^2 - V_{in}^2\frac{V_{out}}{V_{in}}}{g} + \frac{V_{in}^2 - V_{out}^2}{2g}$$

To combine the two terms, the numerator and denominator of the first term, $\frac{V_{out}^2 - V_{in}^2\frac{V_{out}}{V_{in}}}{g}$ will be multiplied by $2$ to become $\frac{2 V_{out}^2 - 2 V_{in}^2\frac{V_{out}}{V_{in}}}{2 g}$. The equation then looks like:

$$h_e = \frac{V_{out}^2 - 2 V_{in} V_{out} + V_{in}^2}{2g}$$

Factoring the numerator yields to the first 'final' form of the minor loss equation:

$$ {\rm{ \mathbf{First \, form:} }} \,\,\, h_e = \frac{\left( V_{in}  - V_{out} \right)^2}{2g}$$

From here, the two other forms of the minor loss equation can be derived by solving for either $V_{in}$ or $V_{out}$ using the ubiquitous continuity equation $V_{in} A_{in} = V_{out} A_{out}$:

$$ {\rm{ \mathbf{Second \, form:} }} \,\,\, h_e = \frac{V_{in}^2}{2g}{\left( {1 - \frac{A_{in}}{A_{out}}} \right)^2} = \frac{V_{in}^2}{2g} \mathbf{K_e^{'}}$$

$$ {\rm{ \mathbf{Third \, form:} }} \,\,\, h_e = \frac{V_{out}^2}{2g}{\left( {\frac{A_{out}}{A_{in}}} -1 \right)^2} = \frac{V_{out}^2}{2g} \mathbf{K_e}$$

Being familiar with these three forms and how they are used will be of great help throughout the class.
