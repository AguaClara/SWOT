# Deriving the Pipe Diameter of a Drain System for tanks

This document contains the derivation of $D_{Pipe}$, which is the pipe diameter necessary to install in a drain system to entirely drain a tank in time $t_{Drain}$.

First, it is necessary to understand how AguaClara tank drains work and what they look like. Many tanks, including the flocculator and entrance tank, have a hole in their bottoms which are fitted with [pipe couplings](https://www.mrpoolman.com.au/assets/thumbL/16057.jpg). During normal operation, these couplings have pipe stubs in them, and the pipe stubs are tall enough to go above the water level in the tank and not allow water to flow into the drain. When the pipe stub is removed, the water begins to flow out of the drain, as the image below indicates. The drain pipe consists of pipe and one elbow, shown in the image.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Pipe_stub_drainage.jpg?raw=true" width=550></center>

While AguaClara sedimentation tanks use valves instead of pipe to begin the process of draining, the actual drain piping system is the same, pipe and an elbow. The equation that will soon be derived applies to both pipe stub and valve drains.

We will start the derivation from the following equation, which is found in an intermediate step from the ['tank with a valve derivation'](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Derivation_flow_through_tank_with_a_valve.md). While this system does not have a valve, it has other sources of minor loss and therefore the equation is still valid.

$$\sqrt h  = \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{Tank}} \sqrt {\frac{2g}{K_e}}$$

We need to make some adjustments to this equation before proceeding, to make it applicable for this new drain-system scenario.  First, we want to assume that the tank has fully drained. Thus, $t = t_{Drain}$ and $h = 0$. Next, we recall that the tank drain is not actually a valve, but just pipe and an elbow, so $A_{Valve} = A_{Pipe}$. Additionally, there can be multiple points of minor loss in the drain system: the entrance from the tank into the drain pipe, the elbow, and potentially the exit of the water out of the drain pipe. When considering a sedimentation tank, the open valve required to begin drainage also has a minor loss associated with it. Therefore, it is necessary to substitute $\sum K_e$ for $K_e$ With these substitutions,  the equation becomes:

$$\sqrt{h_0}  = t_{Drain} \frac{A_{Pipe}}{2 A_{Tank}} \sqrt {\frac{2g}{\sum K_e}}$$

Now, with the knowledge that $A_{Pipe} = \frac{\pi D_{Pipe}^2}{4}$ and rearranging to solve for $D_{Pipe}$, we obtain the following equation:

$$ D_{Pipe} = \sqrt{ \frac{8 A_{Tank}}{\pi t_{Drain}} \sqrt{ \frac{h_0 \sum K_e}{2g} } }$$

To get the equation in terms of easily measureable tank parameters, we substitute $L_{Tank} W_{Tank}$ for $A_{Tank}$. To maintain consistency in variable names, we substitute $H_{Tank}$ for $h_0$.   

**Note:** By saying that $h_0 = H_{Tank}$, we are making the assumption that the pipe drain is at the same elevation as the bottom of the tank. The pipe drain is actually a little lower than the bottom of the tank, but that would make the tank drain faster than $t_{Drain}$, which is ok. Therefore, we are designing a slight safety factor when we say that $h_0 = H_{Tank}$.

Finally, we arrive at the equation for drain pipe sizing:

$$ D_{Pipe} = \sqrt{ \frac{8 L_{Tank} W_{Tank}}{\pi t_{Drain}}} {\left( \frac{H_{Tank} \sum K_{e}}{2g} \right)^{\frac{1}{4}}}$$

Such that the variables are as the appear in the image below.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Pipe_stub_drainage_variables.jpg?raw=true" width=400></center>
