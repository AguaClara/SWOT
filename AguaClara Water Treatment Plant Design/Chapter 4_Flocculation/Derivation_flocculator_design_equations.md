# Deriving the Design Equations for the Flocculator
This document will include the equation derivations required to design an AguaClara hydraulic, vertical flow flocculator.

Derivations will begin with the flocculator's physical dimensions, followed by the design of the baffle and obstacle parameters.

We will assume that the critical design criteria are already defined:

- $h_{L_{floc}} = 40 \, {\rm cm}$  
      - head loss through the flocculator

- $\bar G \theta = 37,000$   
      - total collision potential in the flocculator

- $H = 2 \, {\rm m}$  
      - height of water at the end of the flocculator

- $L_{Max, \, sed} = 6 \, {\rm m}$  
      - maximum length of flocculator, based on sedimentation tank length
- $W_{Min, \, human} = 45 \, {\rm cm}$
      - minimum width based on the width of the average human hip (someone's got to go down there...)

- $\bar G = \frac{g h_{L_{floc}}}{\nu (\bar G \theta)}$  
      - velocity gradient

- $\theta = \frac{\bar G \theta}{\bar G}$  
      - retention time of flocculator

- $\rlap{-} V_{floc} = \frac{\theta}{Q}$  
      - volume of flocculator

## Physical Dimensions
### Max Length (not the actual length!)
Finding the maximum length is necessary to find the _actual_ width of the flocculator.

### Width
We begin by finding the allowable width of a single flocculator channel. Our two restrictions are:
- Ensuring that we maintain the $\bar G$ we get based on our input parameters
- Ensuring that $3 < \frac{H_e}{S} < 6$

First, we begin by setting the two equations for energy dissipation rate, $\bar \varepsilon  = \nu \bar G^2$ and $\bar \varepsilon = \frac{g h_{L_{floc}}}{\theta}$ equal to each other to bring $\bar G$ into the equation.

$$\nu \bar G^2 = \frac{g h_{L_{floc}}}{\theta}$$

**Very Important Note:** For the following steps, we will consider the flow through _**a single flow expansion, $H_e$**_. This could be from baffle to obstacle, obstacle to baffle, obstacle to obstacle if there is more than one obstacle per baffle space, or baffle to baffle if there are no obstacles. This means that we are briefly redefining $\theta$ to be the time it takes for the flow to fully expand after a flow contraction. $\theta$ no longer represents the time it takes for the flow to go through the entire flocculator.

 From here we make three subsequent substitutions: first $h_{L_{floc}} = K_e \frac{\bar V^2}{2g}$, then $\theta = \frac{H_e}{\bar V}$, and finally $\bar V = \frac{Q}{WS}$

$$\nu \bar G^2 = K_e \frac{\bar V^2}{2 \theta}$$

$$\nu \bar G^2 = K_e \frac{\bar V^3}{2 H_e}$$

$$\nu \bar G^2 = \frac{K_e}{2 H_e} \left( \frac{Q}{WS} \right)^3$$

Now we can solve this equation for channel width, $W$.

$$W = \frac{Q}{S}\left( \frac{K_e}{2 H_e \nu \bar G^2} \right)^\frac{1}{3}$$

From here, we can define $\Pi_{HS} = \frac{H_e}{S}$ and substitute $S = \frac{H_e}{\Pi_{HS}}$ into the previous equation for $W$ to get $W_{Min}$:

$$\color{purple}{
W_{Min} = \frac{\Pi_{HS}Q}{H_e}\left( \frac{K_e}{2 H_e \nu \bar G^2} \right)^\frac{1}{3}
}$$
This equation represents the absolute smallest width of a flocculator channel if we consider the lowest value of $\Pi_{HS}$ and the highest possible value of $H_e$:  
$H_e = H$, this implies that there are no obstacles between baffles  
$\Pi_{HS} = 3$

### Maximum Length
