# Deriving the Pipe Diameter of a Drain System for tanks

This document contains the derivation of $D_{Pipe}$, which is the pipe diameter necessary to install in a drain system to entirely drain a tank in time $t_{Drain}$.

First, it is necessary to understand how AguaClara tank drains work and what they look like. Tanks like the flocculator have a hole in their bottoms which are made with [pipe couplings](https://www.mrpoolman.com.au/assets/thumbL/16057.jpg). During normal operation, these couplings have pipes in them, and the pipes are tall enough to go above the water level and not allow water to flow into the drain. When the pipe is removed, the water begins to flow out of the drain, as the image below indicates. The drain pipe consists of pipe and one elbow, as the image indicates. This image is not to scale.  



**Note:** The image below is an example of an AguaClara flocculator drain. A sedimentation tank uses a valve to drain instead of a pipe coupling and piece of pipe. This does not change the derivation at all, the only necessary adjustment is using $D_{Valve}$ instead of $D_{Pipe}$.

![](https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/Pipe%20stub%20drainage.jpg?raw=true)

We will start the derivation from the following equation, which is found in an intermediate step from the [tank-with-a-valve derivation](https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Derivation_flow_through_tank_with_a_valve.md).

$$\sqrt h  = \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{Tank}} \sqrt {\frac{2g}{K_e}}$$

We need to make some adjustments to this equation before proceeding, to make it applicable for this new drain-system scenario.  First, we want to compare the tank before it has started draining to when it finishes draining. Thus, $t = t_{Drain}$ and $h = 0$. Next, we recall that the tank drain is not actually a valve, but just pipe and an elbow, so $A_{Valve} = A_{Pipe}$. With these substitutions,  the equation becomes:

$$\sqrt{h_0}  = t_{Drain} \frac{A_{Pipe}}{2 A_{Tank}} \sqrt {\frac{2g}{K_e}}$$

Now, with the knowledge that $A_{Pipe} = \frac{\pi D_{Pipe}^2}{4}$ and rearranging to solve for $D_{Pipe}$, we obtain the following equation:

$$ D_{Pipe} = \sqrt{ \frac{8 A_{Tank}}{\pi t_{Drain}} \sqrt{ \frac{K_e h_0}{2g} } }$$

To get the equation in terms of easily measureable tank parameters, we substitute $L_{Tank} W_{Tank}$ for $A_{Tank}$. To maintain consistency in variable names, we substitute $H_{Tank}$ for $h_0$.   
**Note:** By saying that $h_0 = H_{Tank}$, we are making the assumption that the pipe drain is at the same elevation as the bottom of the tank. The pipe drain is actually a little lower than the bottom of the tank, but that would only make the tank drain faster than $t_{Drain}$. Therefore, we are designing a slight safety factor when we say that $h_0 = H_{Tank}$

Finally, we arrive at the equation for drain pipe sizing:

$$ D_{Pipe} = \sqrt{ \frac{8 L_{Tank} W_{Tank}}{\pi t_{Drain}}} {\left( \frac{K_{e} H_{Tank}}{2g} \right)^{\frac{1}{4}}}$$

Such that the variables are as the appear in the image below.

![](https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/Pipe%20stub%20drainage%20variables.jpg?raw=true)

Here $K_e$ is the sum of all the minor loss coefficients for the drain system. There is a minor loss as the water enters the drain pipe initially (entrance loss), a minor loss for the elbow, and _maybe_ a minor loss for the exit of the water out of the drain pipe (exit loss), depending on whether or not the drain pipe exits to water or to air.
