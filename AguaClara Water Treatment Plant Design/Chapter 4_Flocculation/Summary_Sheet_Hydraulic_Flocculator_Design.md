# Hydraulic Flocculator Design Summary Sheet
Welcome to the **fourth** summary sheet of CEE 4540! These documents will be guides and references for you throughout the semester. Since Professor Monroe's class time is limited, so too is the amount of material he can fit on the slides while ensuring that they remain understandable. Thus, these summary sheets will supplement the powerpoints by going into further detail on the course concepts introduced in the slides.

Equations, universal constants, and other helpful goodies can be found in the [aide_design repository on GitHub](https://github.com/AguaClara/aide_design/tree/master/aide_design "aide_design"). Most equations and constants you find in these summary sheets will already have been coded into aide_design, and will be shown here in the following format:  

Variable: `pc.gravity`  
Function: `pc.area_circle(DiamCircle)`.

The letters before the `.`, in this case `pc`, indicate the file within aide_design where the variable or function can be found. In the examples above, `pc.gravity` and `pc.area_circle(DiamCircle)` show that the variable `gravity` and function `area_circle(DiamCicle)` are located inside the [physchem.py](https://github.com/AguaClara/aide_design/blob/master/aide_design/physchem.py) (`pc`) file. You are strongly recommended to look up any aide_design equations you plan to use within in their aide_design file before using them, even if they are given here in this summary sheet. This is because each equation has comments in its original file describing what the specific conditions are to using it.

For the most part, [hyperlinks in these documents will contain supplementary information](http://likethis.com/ "This link does not go anywhere"). The information contained in the linked external sites is there in case you don't feel completely comfortable with a concept, but is not necessary to learn thoroughly and will not be tested.


<br>
<br>


---


<br>
<br>

## Table of Contents
Please use this table to control/command find the sections you are looking for.
#### **Section 4: Hydraulic Flocculators, the AguaClara Approach**    
**4.1)** Introduction to Hydraulic Flocculation   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Collision Potential, $G \theta$  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Generating Head Loss with Baffles  
**4.2)**   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;

<br>
<br>


---


<br>
<br>

## Section 4: Hydraulic Flocculators, the AguaClara Approach
### Important Terms
1.  Collision potential  
2. Energy dissipation rate

### Important Equations   
1.

## 4.1) Introduction to Hydraulic Flocculation
The reason that flocculation is widely used in water treatment is because of sedimentation. Sedimentation is the process that actually removes particles like clay, dirt, organic matter, and bacteria from water. As you learned in the previous chapter on Rapid Mix _**(DOUBLE CHECK THAT THIS IS IN RAPID MIX ONCE RAPID MIX IS WRITTEN)**_, sedimentation is the process of particles 'falling' out of water due to density stratification, and its governing equation is:

$$V_t = \frac{d^2 g}{18 \nu} \frac{\rho_p - \rho_w}{\rho_w}$$  

Such that:  
$V_t$ = terminal velocity of a particle, its downwards speed if it were in quiescent (still) water  
$d$ = particle diameter  
$\rho$ = density. $p$ stands for particle, $w$ stands for water

To increase $V_t$ and make sedimentation more efficient, floccuation aims to increase the diameter $d$ of the particles. This is done by applying a coagulant to the dirty water and helping the coagulant to stick evenly to all particles during Rapid Mix _**(DOUBLE CHECK THAT THIS IS IN RAPID MIX ONCE RAPID MIX IS WRITTEN)**_. Being covered in coagulant allows the particles to collide, merge, and grow bigger during flocculation.

So our goal in designing a flocculator is to facilitate particle collisions. How can we do this?

### Collision Potential, $G \theta$, and Energy Dissipation Rate, $\varepsilon$
**Collision potential** is a term with a very straightforward name. It represents the magnitude of potential particle collisions in a fluid. It is a _dimensionless_ parameter which is often used as a performance metric for flocculators; big $G \theta$ values indicate lots of collisions (good) while small values indicate fewer collisions (not so good). AguaClara flocculators usually aim for a collision potential of 37,000. _**WHY DO WE SHOOT FOR 37,000?**_ The value for collision potential is obtained by multiplying $G$, a parameter for fluid shear with units of $\frac{1}{[T]}$, and $\theta$, the residence time of water in the flocculator, with units of $[T]$. $\theta$ is intuitive to measure, calculate, and understand. $G$ is a bit more difficult. First, an intuitive explanation. See the image below, which shows the velocity profile of flowing water.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/Juan_summary_sheets/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%204_Flocculation/Images/G_velocity_profile.jpg?raw=true" width=500>


$G$ measures the magnitude of shear by using the velocity gradient of a fluid in space, $\frac{\Delta V}{\Delta h}$. This is essentially the same as the $\frac{\delta u}{\delta y}$ term in fluid mechanics, which is found in the ubiquitous [fluid-shear problem](http://polymerdatabase.com/polymer%20physics/images/Visc.png "sourced from http://polymerdatabase.com/polymer%20physics/Viscosity.html").

$\bar G$ represents the average $\frac{\Delta V}{\Delta h}$ for the entire water volume under consideration, and is the parameter we will be using from now on. Unfortunately, it is unrealistic to measure $\frac{\Delta V}{\Delta h}$ for every parcel of the water in our flocculator and take an average. We need to approximate $\bar G$ using measureable parameters.

The parameter that serves as the basis for obtaining $\bar G$ is $\varepsilon$, which represents the **energy dissipation** rate of a fluid _normalized by its mass_. The units of $\varepsilon$ are Watts per kilogram:

$$\varepsilon = \left[ \frac{W}{Kg} \right]
= \left[ \frac{J}{s \cdot Kg} \right]
= \left[ \frac{N \cdot m}{s \cdot Kg} \right]
= \left[ \frac{kg \cdot m \cdot m}{s^2 \cdot s \cdot Kg} \right]
= \left[ \frac{m^2}{s^3} \right]
= \left[ \frac{[L]^2}{[T]^3} \right]$$

There are at least two ways to think about $\varepsilon$. One is through $G$. Imagine that a fluid has _no viscosity_; there is no internal friction caused by fluid flow. No matter how high $G$ becomes, no energy is dissipated. Now image a honey, which has a very high viscosity. Making honey flow fast requires a lot of energy over a short period of time, which means a high energy dissipation rate. This explanation allows us to understand the equation for $\varepsilon$ in terms of $G$ and $\nu$:

$$\varepsilon = \nu G^2$$

Which means we can solve for $G$:

$$G = \sqrt{\frac{\varepsilon}{\nu}}$$

Energy dissipation rate is, fortunately, easier to determine than collision potential. This is due to the second way to think about $\varepsilon$, which is using head loss. In any reactor, a flocculator in this case, the total energy dissipated is simply the head loss, $h_L$. The amount of time required to dissipate that energy is the residence time of the water in the reactor, $\theta$. Accounting for the fact that 'head' energy is due to gravity $g$, we have all the parameters needed to determine another equation for energy dissipation rate:

$$ \bar \varepsilon = \frac{g h_L}{\theta} $$

Note that the equation above is for $\bar \varepsilon$, not $\varepsilon$. Since the head loss term we are using, $h_L$, occurs over the entire reactor, it can only be used to find an average energy dissipation rate for the entire reactor. Combining the equations above, $G = \sqrt{\frac{\varepsilon}{\nu}}$ and $\bar \varepsilon = \frac{g h_L}{\theta}$, we can get an equation for $\bar G$ in terms of easily measureable parameters:

$$\bar G = \sqrt{\frac{g h_L}{\nu \theta}}$$

We can use this to obtain a final equation for collision potential of a reactor:

$$\bar G \theta = \sqrt{\frac{g h_L \theta}{\nu}}$$


### Generating Head Loss with Baffles
Now that we know how to measure collision potential with head loss, we need a way to actually generate head loss. While both major or minor losses can be the design basis, it generally makes more sense to use major losses for low-flow flocculation and minor losses for higher flows, as flocculation with minor losses tends to be more space-efficient.

To generate minor losses, we need to cause flow expansions. AguaClara does this with baffles, which are simply obstructions in the channel of a flocculator to make the flow switch directions by 180°.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/Juan_summary_sheets/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%204_Flocculation/Images/AC_flocculator.jpg?raw=true" width=500>
