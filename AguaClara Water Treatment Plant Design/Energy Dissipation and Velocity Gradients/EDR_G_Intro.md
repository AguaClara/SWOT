# Energy dissipation rate, velocity gradients, and mixing
## Introduction

Drinking water treatment requires
* mixing chemicals with the water
* collisions between dissolved substances, nanoparticles, pathogens, suspended particles
* prevention of floc breakup in high shear zones
* and possibly, shear that prevents coagulant nanoparticle deposition on reactor walls

Each of these processes requires an understanding of fluid dynamics and specifically the relationships between turbulence, fluid deformation, energy dissipation, velocity gradients, and shear.

The energy dissipation rate is the rate that mechanical energy is being converted to heat. In a control volume that does not include pumps or turbines the mechanical energy lost is $g h_L$. That energy is lost in the time that the fluid is in the control volume, $\theta$.

$$ \bar\varepsilon \theta = g h_L$$

This equation simply states that the average rate of energy dissipation times the time over which that dissipation occurs is equal to the total lost mechanical energy. The dimensions of $\varepsilon$ are

$$ \varepsilon = \frac{[m^3]}{[s^3]} = \frac{W}{kg} $$

which can be understood as a velocity squared per time, ie, a rate of kinetic energy loss or as power per unit mass.

For mechanical mixing where an impeller is adding shaft work to a control volume we have

$$ \bar\varepsilon = \frac{P}{M} = \frac{P}{\rho \rlap{\kern.08em--}V}$$

where
* $P$ = power input into the control volume
* $M$ = mass of fluid in the control volume
* $\rlap{\kern.08em--}V$ = volume of the control volume
* $\rho$ = density of the fluid

Velocity gradients are central to flocculation because it is the deformation of the fluid caused by the velocity gradient that causes particles to collide with each other. If everyone on a sidewalk is walking in the same direction at exactly the same velocity, then there will never be any collisions between people. If, however, people at one side of the sidewalk stand still and people walk progressively faster as a function of how far they are away from the zero velocity side of the sidewalk, then there will be many collisions between the pedestrians.  Indeed, the rate of collisions is proportional to the velocity gradient.

Estimation of velocity gradients for various flow geometries is the basis for the design of rapid mix, flocculators, and plate settlers and thus our goal is to define the velocity gradients consistently across the range of possible flow regimes. There are three approaches to calculating the average velocity gradient within a control volume.
1) Use the Navier Stokes equations and solve for the spatially averaged velocity gradient.
1) Use computation fluid dynamics to solve for the spatially averaged velocity gradient.
1) Use the total mechanical energy loss in the control volume to calculate the energy dissipation rate. Estimate the velocity gradient directly from the energy dissipation rate, $G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}}$, as defined by Camp and Stein in 1943 (Camp, T. R., and Stein, P. C. (1943) ‘‘Velocity Gradients and Hydraulic Work in Fluid Motion,’’ J. Boston Soc. Civil Eng., 30, 203–221.).

The first approach would be ideal but is difficult in practice because Navier Stokes solutions are only available for limited geometries and laminar flow. Computational Fluid Dynamics could be used but is difficult to use as a general engineering design approach given the large number of geometries that are used in drinking water treatment plants. For these reasons we will use the control volume approach to estimate the average velocity gradient. This method incorrectly assumes that the energy dissipation rate is completely uniform in the control volume and hence the velocity gradient is also uniform. This method results in an over estimation of the velocity gradient.

The Camp-Stein estimate of $G_{CS} $ is based on a control volume where the velocity gradient is uniform. Consider a layer of fluid of depth $H$ and apply a velocity, $v$ at the top of the fluid. The velocity gradient, $G$, is thus $\frac{v}{H}$ everywhere in the fluid. The force required to move the top of the fluid at velocity v can be obtained from the required shear, $\tau$. From Newtons Law of Friction we have

$$\tau = \mu \frac{v}{H} = \mu G = \nu\rho G$$

Where $\tau$ is force required per unit plan view area. The power per unit area required to move the fluid at velocity $v$ is $\tau v$. The mass per unit area is $\rho H$. Thus the energy dissipation rate or the power per mass is

$$\varepsilon = \frac{P}{M} = \frac{\tau v}{\rho H} = \frac{\nu \rho G v}{\rho H} = \nu G^2 $$

This equation has no approximations, but has one very important assumption. We derived this equation for a control volume where the velocity gradient was uniform. The reactors and control volumes that we will be using as we design water treatment plants will not have uniform velocity gradients. Indeed, several of the water treatment processes will be turbulent and thus the velocity gradients in the fluid will vary in both space and time. Even in laminar flow in a pipe the velocity gradient is far from uniform with high velocity gradients at the wall and zero velocity gradient at the center of the pipe.

We'd like to know if we can apply the previous equation
$$\varepsilon = \nu G^2 $$

to the case where the energy dissipation rate and velocity gradients are nonuniform by simply introducing average values of both quantities.

$$\bar\varepsilon \overset{?}{=} \nu \bar G^2 $$

Consider a hypothetical reactor (case 2) that is 4 times as large in plan view area as the uniform velocity gradient case explored above (case 1). In addition, assume that 3/4 of the reactor has a velocity gradient of zero. The average energy dissipation rate for case 1 is

$$\bar \varepsilon_1 = \frac{P_1}{M_1} =  \nu \bar G_1^2 $$

The average energy dissipation rate for case 2 is
$$\bar \varepsilon_2 = \frac{P_1}{4M_1} = \frac{\bar \varepsilon_1}{4} $$
This makes sense because we are putting in the same amount of energy into a control volume that is 4 times bigger.

Now we calculate the velocity gradients. As previously determined,

$$\bar G_1 = \sqrt{\frac{\bar\varepsilon_1}{\nu}}$$.

The average velocity gradient in the second control volume is simply the volume weighted average
$$\bar G_2 = \bar G_1\frac{1}{4}+ 0 \frac{3}{4}$$
where 1/4 of the case 2 control volume has the same velocity gradient as the case 1 control volume and 3/4 of the control volume has a velocity gradient of 0. The Camp Stein method would suggest that $\bar G_2$ is equal to

$$\bar G_2 \overset{?}{=} \sqrt{\frac{\bar\varepsilon_2}{\nu}}= \sqrt{\frac{\bar\varepsilon_1}{4\nu}}$$

Now we check to see if the Camp Stein method of estimating the average velocity gradient, $\bar G$, is correct.

$$\bar G_2 = \frac{\bar G_1}{4} \neq \sqrt{\frac{\bar\varepsilon_1}{4\nu}} =  \frac{\bar G_1}{2}$$

Given that the energy dissipation rate is proportional to the square of the velocity gradient the mean of the energy dissipation rate is **not** proportional to the mean of the velocity gradient. Thus the Camp Stein method of calculating the average velocity gradient is not correct except in the case of uniform velocity gradient. The Camp Stein equation is dimensionally correct and could be corrected by adding a dimensionless constant $\Pi_{CS}$ that is a function of the energy dissipation rate distribution within the control volume.

$$\bar G =\Pi_{CS}\sqrt{\frac{\bar\varepsilon}{\nu}}$$

where $\Pi_{CS}$ is 1 for a uniform velocity gradient and is less than one for non uniform velocity gradients. We can think $\Pi_{CS}$ as a measure of the efficiency of using energy to deform the fluid. We can calculate $\Pi_{CS}$ for cases where we have either a Navier Stokes  or a computation fluid dynamics estimate of $\bar G$.

The conventional approach to design of flocculators uses the Camp Stein definition of
$$G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}}$$
where $G_{CS}$ is **not** the average velocity gradient, but is larger than the average velocity gradient by a factor of $\Pi_{CS}$. Thus we have

$$G_{CS} = \Pi_{CS}\bar G $$

Use of the Camp Stein velocity gradient in design of mixing units and flocculators results in an error when applying results from one reactor to another. If the energy dissipation rate distribution within the reactors is different, then $\Pi_{CS}$ will be different for the two reactors and the actual average velocity gradient, $\bar G$ will be different for the two reactors.

Given that energy is used more efficiently to produce velocity gradients if the velocity gradients are uniform, our goal is to design mixing and flocculation units that have relatively uniform velocity gradients. If all of our reactors at both research scale and municipal scale have similar values of $\Pi_{CS}$, then we can use the Camp Stein definition of $G_{CS}$ and not introduce any significant errors. It will not be reasonable, however, to expect similar performance based on similar values of $G_{CS}$ if one reactor has relatively uniform energy dissipation rates and the other reactor has zones with very high energy dissipation rates and zones with very low energy dissipation rates.

We will demonstrate later that mechanically mixed reactors typically have a much wider range of energy dissipation rates than do well designed hydraulically mixed reactors. Thus comparisons between mechanically mixed and hydraulically mixed reactors must account for differences in $\Pi_{CS}$.

We will use the Camp Stein definition $ G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}} $ as the design parameter of convenience in this textbook.
