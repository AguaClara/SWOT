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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;  
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

### Important Equations   
1.

## 4.1) Introduction to Hydraulic Flocculation
The reason that flocculation is widely used in water treatment is because of sedimentation. Sedimentation is the process that actually removes particles like clay, dirt, organic matter, and bacteria from water. As you learned in the previous chapter on Rapid Mix _**(DOUBLE CHECK THAT THIS IS IN RAPID MIX ONCE RAPID MIX IS WRITTEN)**_, sedimentation is the process of particles 'falling' out of water due to density stratification, and its governing equation is:

$$V_t = \frac{d^2 g}{18 \nu} \frac{\rho_p - \rho_w}{\rho_w}$$  

Such that:  
$V_t$ = terminal velocity, the downwards speed of the particle if it were in quiescent (still) water  
$d$ = particle diameter  
$\rho$ = density. $p$ stands for particle, $w$ stands for water

To increase $V_t$ and make sedimentation more efficient, floccuation aims to increase the diameter $d$ of the particles. This is done by applying a coagulant to the dirty water, helping it to stick evenly to all particles during Rapid Mix _**(DOUBLE CHECK THAT THIS IS IN RAPID MIX ONCE RAPID MIX IS WRITTEN)**_, and allowing the particles to collide, merge, and grow bigger during flocculation.

So our goal in designing a flocculator is to facilitate particle collisions. How can we do this?

### Collision Potential, $G \theta$
**Collision potential** is a term with a very straightforward name. It is a _dimensionless_ parameter which is often used as a performance metric for flocculators; big values are good and small values are bad. AguaClara aims for a collision potential of 37,000. The value for collision potential is obtained by multiplying $G$, a parameter for fluid shear with units of $\frac{1}{[T]}$, and $\theta$, the residence time of water in the flocculator. $\theta$ is easy to measure, calculate, and understand. $G$ is a bit more difficult. First, an intuitive explanation. See the image below, which shows the velocity profile of flowing water.

<img src="https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%204_Flocculation/Images/G_veloctiy_profile.jpg?raw=true" width=500>

$G$ measures the magnitude of shear by comparing the velocity gradient of a fluid, in this case water, to the space it spans, $\frac{\Delta V}{\Delta h}$. This is essentially the same thing as the $\frac{\delta u}{\delta y}$ term you learned about in fluid mechanics. The only difference is that $\frac{\delta u}{\delta y}$ considers flow at a boundary, while $\frac{\Delta V}{\Delta g}$ can apply to water at or away from a boundary. 

$G$ represents the average $\frac{\Delta V}{\Delta h}$ for the entire water volume under consideration. Unfortunately, we can't measure $\frac{\Delta V}{\Delta h}$ for every part of the water we care about and take an average. We need to approximate $G$ using measureable parameters.
