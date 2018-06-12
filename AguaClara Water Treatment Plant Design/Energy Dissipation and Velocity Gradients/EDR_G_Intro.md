# Energy Dissipation Rate, Velocity Gradient, and Mixing
## Introduction

In addition to the general fluids review in the previous chapter, there are a few extra fluid dynamics concepts that are important to know in order to understand drinking water treatment and AguaClara's approach to it. These concepts are primarily focused on the relationships between:
* Turbulence
* Viscosity
* Shear
* Velocity Gradients ($G$), which serve as a measure of fluid deformation
* Energy Dissipation Rate (EDR, $\varepsilon$)

Knowledge of these concepts and how they interact is critical to understand the following processes, which are key parts of water treatment:

* **[Rapid Mix](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix) and [Disinfection](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Disinfection):** Thorough mixing of chemicals with the water
* **[Flocculation](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Flocculation):**
  - Collisions between dissolved substances, nanoparticles, pathogens, and suspended particles
  - Prevention of floc breakup in high shear zones  
and possibly,
  - Shear that prevents coagulant nanoparticle deposition on reactor walls

The two concepts that were not covered in the previous chapter, [fluids review](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Fluids_Review_Design.md), are velocity gradient $G$ and energy dissipation rate $\varepsilon$. While these will be very thoroughly described over the course of this introduction, a brief and simple explanation is included to help get the ball rolling.

### What do $G$ and $\varepsilon$ mean?

$G$, or velocity gradient, is a measure of fluid deformation. It is defined by how quickly one point of water along one streamline moves in comparison to another point on another streamline ($v_A$ compared to $v_B$, for example), taking into account the distance between the streamlines, $\Delta h$. A visual example of a velocity gradient is shown in the image below:

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/Velocity_gradient_image.jpg" width=700></center>

</br>

**Note on terminology:** "Fluid deformation" is equivalent to "velocity gradient," and the two terms can be used interchangeably. They are different ways of thinking about the same concept. Thus, $G$ is the measure of both terms.

$\varepsilon$, or energy dissipation rate, is the rate that the kinetic energy of the fluid is being converted to heat. EDR is a very useful concept because the last step of converting kinetic energy into heat is accomplished by viscosity ($\nu$). This kinetic energy being dissipated by viscosity is the energy associated with velocity gradients ($G$). Thus, through EDR there is a direct connection between $\nu$ and $G$. This connection will be further covered later on in this introduction.

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/EDR_image.jpg" width=700></center>

### Deriving equations for $\varepsilon$ and $G$

As mentioned above, EDR and velocity gradients play an important role in mixing and in causing suspended particles to collide with each other, both important topics in flocculation. Their use is not limited to flocculation, however, they are also helpful in understanding failure modes of plate settlers ([Sedimentation](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Sedimentation)) and terminal head loss of sand filters ([Filtration](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Filtration)).

We will begin by defining the concept of energy dissipation rate for a control volume. In a control volume that does not include pumps, turbines or other external energy sources or sinks, the mechanical energy lost is indicated by a change in elevation and quantified as $g h_L$. That mechanical energy is lost in the time that the fluid is in the control volume, $\theta$.

$$ \bar\varepsilon \theta = g h_L$$

This equation simply states that the average rate of energy dissipation times the time over which that dissipation occurs is equal to the total lost mechanical energy. The dimensions of $\varepsilon$ are:

$$ \varepsilon = \frac{[m^3]}{[s^3]} = {\rm \frac{W}{kg}} $$

These dimensions can be understood as a velocity squared per time, otherwise known as a rate of kinetic energy loss (recall that kinetic energy is ${\rm Ke} = \frac{v^2}{2g}$, or ${\rm Ke} \propto v^2$), or as power per unit mass, which would be ${\rm \frac{W}{kg}}$.

Velocity gradients are central to flocculation because they cause the deformation of the fluid which results in particle collisions. Consider a real-world example: if everyone on a sidewalk is walking in the same direction at exactly the same velocity, then there will never be any collisions between people. If, however, people at one side of the sidewalk stand still and people walk progressively faster as a function of how far they are away from the zero velocity side of the sidewalk, then there will be many collisions between the pedestrians.  Indeed, the rate of collisions is proportional to the velocity gradient.

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/Pedestrians_on_sidewalk.jpg" width=700></center>

Estimation of velocity gradients for various flow geometries is the basis for the design of rapid mix, flocculators, and plate settlers and thus our goal is to define the velocity gradients consistently across the range of possible flow regimes. There are three approaches to calculating the average velocity gradient within a control volume.
1) Use the Navier Stokes equations and solve for the spatially averaged velocity gradient.
1) Use computation fluid dynamics to solve for the spatially averaged velocity gradient.
1) Use the total mechanical energy loss in the control volume to calculate the energy dissipation rate. Estimate the velocity gradient directly from the energy dissipation rate, $G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}}$, as defined by Camp and Stein in 1943 (Camp, T. R., and Stein, P. C. (1943) ‘‘Velocity Gradients and Hydraulic Work in Fluid Motion,’’ J. Boston Soc. Civil Eng., 30, 203–221.).

The first approach would be ideal but is difficult in practice because Navier Stokes solutions are only available for limited geometries and laminar flow. Computational Fluid Dynamics could be used but is difficult to use as a general engineering design approach given the large number of geometries that are used in drinking water treatment plants. For these reasons we will use the control volume approach to estimate the average velocity gradient. This method incorrectly assumes that the energy dissipation rate is completely uniform in the control volume and hence the velocity gradient is also uniform. This method results in an over estimation of the velocity gradient.

The Camp-Stein estimate of $G_{CS}$ is based on a control volume where the velocity gradient is uniform. Consider a layer of fluid of depth $H$ and apply a velocity, $v$ at the top of the fluid. The velocity gradient, $G$, is thus $\frac{v}{H}$ everywhere in the fluid. The force required to move the top of the fluid at velocity v can be obtained from the required shear, $\tau$. From Newtons Law of Friction we have

$$\tau = \mu \frac{v}{H} = \mu G = \nu\rho G$$

Where $\tau$ is the force required per unit plan view area. The power per unit area required to move the fluid at velocity $v$ is $\tau v$. The mass per unit area is $\rho H$. Thus the energy dissipation rate or the power per mass is

$$\varepsilon = \frac{P}{M} = \frac{\tau v}{\rho H} = \frac{\nu \rho G v}{\rho H} = \nu G^2 $$

This equation has no approximations, but has one very important assumption. We derived this equation for a control volume where the velocity gradient was **uniform**. The reactors and control volumes that we will be using as we design water treatment plants will **not** have uniform velocity gradients. Indeed, several of the water treatment processes will be turbulent and thus the velocity gradients in the fluid will vary in both space and time. Even in laminar flow in a pipe the velocity gradient is far from uniform with high velocity gradients at the wall and zero velocity gradient at the center of the pipe.

We'd like to know if we can apply the previous equation
$$\varepsilon = \nu G^2 $$

to the case where the energy dissipation rate and velocity gradients are nonuniform by simply introducing average values of both quantities.

$$\bar\varepsilon \overset{?}{=} \nu \bar G^2 $$

We will test this option with a simple case. Consider a hypothetical reactor (case 2) that is 4 times as large in plan view area as the uniform velocity gradient case explored above (case 1). In addition, assume that 3/4 of the reactor has a velocity gradient of zero. The average energy dissipation rate for case 1 is

$$\bar \varepsilon_1 = \frac{P_1}{M_1} =  \nu \bar G_1^2 $$

The average energy dissipation rate for case 2 is
$$\bar \varepsilon_2 = \frac{P_1}{4M_1} = \frac{\bar \varepsilon_1}{4} $$
This makes sense because we are putting in the same amount of energy into a control volume that is 4 times bigger.

Now we calculate the velocity gradients. As previously determined,

$$\bar G_1 = \sqrt{\frac{\bar\varepsilon_1}{\nu}}$$

The average velocity gradient in the second control volume is simply the volume weighted average
$$\bar G_2 = \bar G_1\frac{1}{4}+ 0 \frac{3}{4}$$
where 1/4 of the case 2 control volume has the same velocity gradient as the case 1 control volume and 3/4 of the control volume has a velocity gradient of 0. The Camp Stein method would suggest that $\bar G_2$ is equal to

$$\bar G_2 \overset{?}{=} \sqrt{\frac{\bar\varepsilon_2}{\nu}}= \sqrt{\frac{\bar\varepsilon_1}{4\nu}}$$

Now we check to see if the Camp Stein method of estimating the average velocity gradient, $\bar G$, is correct.

$$\bar G_2 = \frac{\bar G_1}{4} \neq \sqrt{\frac{\bar\varepsilon_1}{4\nu}} =  \frac{\bar G_1}{2}$$

Given that the energy dissipation rate is proportional to the square of the velocity gradient the mean of the energy dissipation rate is **not** proportional to the mean of the velocity gradient. Thus the Camp Stein method of calculating the average velocity gradient is not correct except in the case of uniform velocity gradient. The Camp Stein equation is dimensionally correct and could be corrected by adding a dimensionless constant $\Pi_{CS}$ that is a function of the energy dissipation rate distribution within the control volume.

$$\bar G =\Pi_{CS}\sqrt{\frac{\bar\varepsilon}{\nu}}$$

where $\Pi_{CS}$ is 1 for a uniform velocity gradient and is less than one for non uniform velocity gradients. We can think $\Pi_{CS}$ as a measure of the efficiency of using energy to deform the fluid. We can calculate $\Pi_{CS}$ for cases where we have either a Navier Stokes or a computation fluid dynamics estimate of $\bar G$.

The conventional approach to design of flocculators uses the Camp Stein definition of

$$G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}}$$

where $G_{CS}$ is **not** the average velocity gradient, but is larger than the average velocity gradient by a factor of $\Pi_{CS}$. Thus we have

$$G_{CS} = \Pi_{CS}\bar G $$

Use of the Camp Stein velocity gradient in design of mixing units and flocculators results in an error when applying results from one reactor to another. If the energy dissipation rate distribution within the reactors is different, then $\Pi_{CS}$ will be different for the two reactors and the actual average velocity gradient, $\bar G$ will be different for the two reactors.

Given that energy is used more efficiently to produce velocity gradients if the velocity gradients are uniform, our goal is to design mixing and flocculation units that have relatively uniform velocity gradients. If all of our reactors at both research scale and municipal scale have similar values of $\Pi_{CS}$, then we can use the Camp Stein definition of $G_{CS}$ and not introduce any significant errors. It will not be reasonable, however, to expect similar performance based on similar values of $G_{CS}$ if one reactor has relatively uniform energy dissipation rates and the other reactor has zones with very high energy dissipation rates and zones with very low energy dissipation rates.

We will demonstrate later that mechanically mixed reactors typically have a much wider range of energy dissipation rates than do well designed hydraulically mixed reactors. Thus comparisons between mechanically mixed and hydraulically mixed reactors must account for differences in $\Pi_{CS}$.

We will use the Camp Stein definition $G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}}$ as the design parameter of convenience in this textbook.

# Different Geometries
Water treatment plants at research and municipal scales deploy a wide range of flow geometries. The following list includes the flow geometries that are commonly used for mixing processes and example locations.

* Straight pipe (wall shear) - [uncommon, but included for completeness]
* Coiled tube (wall shear and expansions) - [research scale mixing]
* Series of expansions (expansions) - [hydraulic flocculators]
* Mechanical mixing - [mechanical rapid mix and flocculators]
* Between flat plates (wall shear) - [plate settlers]
* Round jet -  (expansion) - [hydraulic rapid mix]
* Plane jet - (expansion) - [inlet into sedimentation tank]
* Behind a flat plate - (expansion) - [mechanical mixers]

The following tables can serve as a convenient reference to the equations describing head loss, energy dissipation rates, and velocity gradients in various flow geometries that are commonly encountered in water treatment plants.

Table of equations for control volume averaged values of head loss, energy dissipation rate, and the Camp-Stein velocity gradient.
| Geometry | $h_L$ |$\bar\varepsilon$ | $G_{CS}(\bar v)$ |  $G_{CS}(Q)$|
| - | :-: | :-: | :-: | :-: |
| Straight pipe | $h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$ |$\bar\varepsilon = \frac{\rm{f}}{2} \frac{\bar v^3}{D}$ |$G_{CS} = \left(\frac{\rm{f}}{2\nu} \frac{\bar v^3}{D} \right)^\frac{1}{2}$ |  $G_{CS} = \left(\frac{\rm{32f}}{ \pi^3\nu} \frac{Q^3}{D^7} \right)^\frac{1}{2}$ |
| Straight pipe laminar|$h_{\rm{f}} = \frac{32\nu L\bar v}{ g D^2}$| $\bar\varepsilon =32\nu \left( \frac{\bar v}{D} \right)^2$ |$G_{CS} =4\sqrt2 \frac{\bar v}{D}$ | $G_{CS} =\frac{16\sqrt2}{\pi} \frac{Q}{D^3}$ |
| Parallel plates laminar | $h_{\rm{f}} = 12\frac{ \nu L \bar v }{gS^2}$ | $\bar\varepsilon = 12 \nu \left(\frac{  \bar v}{S} \right)^2$ | $G_{CS} = 2\sqrt{3}\frac{  \bar v}{S}$ | :-: |
| Coiled tube laminar | $h_{L_{coil}} = \frac{32\nu L\bar v}{ g D^2} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]$ |$\bar\varepsilon = 32\nu \left( \frac{\bar v}{D} \right)^2 \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]$| $G_{CS_{coil}} = 4\sqrt2 \frac{\bar v}{D}\left[ 1 + 0.033\left(log_{10}De\right)^4  \right]^\frac{1}{2}$ | - |
| Expansions | $h_e =  \mathbf{K_e}\frac{\bar v_{out}^2}{2g}$ | $\bar\varepsilon = \mathbf{K_e}\frac{\bar v_{out}^3}{2H}$ | $G_{CS} = \bar v_{out}\sqrt{\frac{\mathbf{K_e}\bar v_{out}}{2H\nu}}$ | - |

The equations used to convert between columns in the table above are:

$$\bar\varepsilon = \frac{gh_{\rm{L}}}{\theta} \qquad\qquad
G_{CS} = \sqrt{\frac{\bar \varepsilon}{\nu}} \qquad\qquad
\bar v=\frac{4Q}{\pi D}$$

Note that the velocity gradient is independent of viscosity (and hence temperature) for laminar flow. This is because the total amount of fluid deformation is simply based on geometry. The no slip condition, the diameter, and the length of the flow passage set the total fluid deformation. Of course, if temperature decreases and viscosity increases the amount of energy required to push the fluid through the flow passage will increase (head loss is proportional to viscosity for laminar flow).

For turbulent flow and for flow expansions the amount of fluid deformation decreases as the viscosity increases and the total energy required to send the flow through the reactor is almost independent of the viscosity. The "almost" is because for wall shear under turbulent conditions there is a small effect of viscosity that is buried inside the friction factor.

Table of equations for maximum (wall) energy dissipation rates and wall velocity gradients.
| Geometry | $\varepsilon_{wall}$ | $G_{wall}$|
| - | :-: |:-: |
| Straight pipe  | $\varepsilon_{wall} = \frac{1}{\nu}\left(\rm{f}  \frac{\bar v^2}{8} \right)^2$ | $G_{wall} =\rm{f}  \frac{\bar v^2}{8\nu}$|
| Straight pipe laminar | $\varepsilon_{wall} = \left(\frac{8\bar v}{D} \right)^2 \nu$ | $G_{wall} =  \frac{8\bar v}{D}$|
| parallel plates | $\varepsilon_{wall} = 36\left( \frac{\bar v}{S}\right)^2 \nu$ | $G_{wall} = \frac{6 \bar v}{S}$|
| Coiled pipe | - | $G_{CS_{wall_{coil}}} =\rm{f} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]  \frac{\bar v^2}{8\nu}$|

Table of equations for maximum energy dissipation rates and velocity gradients for flow expansions.
| Geometry |$\Pi_{Jet}$ | $\varepsilon_{max}$ | $G_{max}$|
| - | :-: |:-: |:-: |
| Round jet |0.08 | $\varepsilon_{Max} = \Pi_{JetRound}\frac{   \bar v_{Jet} ^3}{D_{Jet}}$ | $G_{Max} = \bar v_{Jet} \sqrt{\frac{\Pi_{RoundJet} \bar v_{Jet} }{\nu D_{Jet}}}$ |
| Plane jet |0.0124| $\varepsilon_{Max} = \Pi_{JetPlane} \frac{  \bar v_{Jet} ^3}{S_{Jet}}$ | $G_{Max} = \bar v_{Jet}\sqrt{\frac{\Pi_{JetPlane} \bar v_{Jet}}{\nu S_{Jet}}}$ |
| Behind a flat plate |0.04 | $\varepsilon _{Max} = \Pi_{Plate}\frac{\bar v^3}{W_{Plate}}$ | $G_{Max} = \bar v\sqrt{\frac{\Pi_{Plate} \bar v}{\nu W_{Plate}}}$ |

For mechanical mixing where an impeller or other stirring device is adding shaft work to a control volume we have

$$ \bar\varepsilon = \frac{P}{M} = \frac{P}{\rho \rlap{-}V}$$

where
* $P$ = power input into the control volume
* $M$ = mass of fluid in the control volume
* $\rlap{-}V$ = volume of the control volume
* $\rho$ = density of the fluid

The Camp-Stein velocity gradient in a mechanically mixed reactor is

$$ G_{CS} = \sqrt{\frac{P}{\rho \nu \rlap{-}V}} $$
