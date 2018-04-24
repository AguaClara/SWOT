# Deriving the Pipe Diameter of a Drain System for tanks

This document contains the derivation of $D_{Pipe}$, which is the pipe diameter necessary to install in a drain system to entirely drain a tank in time $t_{Drain}$.

We will start from the following equation, which is found in an intermediate step from the [tank-with-a-valve derivation](https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Derivation_flow_through_tank_with_a_valve.md).

$$\sqrt h  = \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{Tank}} \sqrt {\frac{2g}{K_e}}$$

We need to make some adjustments to this equation before proceeding. First, it is necessary to understand how AguaClara tank drains work and what they look like. Tanks like the flocculator and sed tanks have holes in their bottoms which hold pipe couplings. During normal operation, these couplings have pipes in them, and the pipes are tall enough to go above the water level and not allow water to flow into the drain. When the pipe is removed, the water begins to flow out of the drain.

![](https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/Pipe%20stub%20drainage.jpg?raw=true)

We are looking for how long it will take to completely drain the tank, so to have a water level of $h = 0$ at time $t_{Drain}$. With these assumptions, the knowledge that $A_{Valve} = \frac{\pi D_{Valve}}{4}$, and rearranging to solve for $D_{Valve}$ we obtain the following equation:

$$ D_{Valve} = \sqrt{ \frac{8 A_{Tank}}{\pi t_{Drain}}} {\left( \frac{K_{e} h_{0}}{2g} \right)^{\frac{1}{4}}}$$

To get the equation in terms of easily measureable tank parameters, we substitute $A_{Tank}$ for $L_{Tank} W_{Tank}$ and $h_0$ for $H_{Tank}$.   
**Note:** By saying that $h_0 = H_{Tank}$, we are making the assumption that the valve is at the same elevation as the bottom of the tank.

$$ D_{Valve} = \sqrt{ \frac{8 L_{Tank} W_{Tank}}{\pi t_{Drain}}} {\left( \frac{K_{e} H_{Tank}}{2g} \right)^{\frac{1}{4}}}$$

![](https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/Pipe%20stub%20drainage%20variables.jpg?raw=true)
