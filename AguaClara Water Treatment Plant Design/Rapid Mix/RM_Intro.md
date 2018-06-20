# Introduction
Rapid mix is the term commonly used to describe the processes that occur between the coagulant addition to the raw water and the flocculation process. The processes that occur are not well understood and thus design guidelines have been empirical.

“In summary, little is known about rapid mix, much less any sensitivity to scale. However, the models and data reviewed suggest the need to be on the lookout for certain effects. From what is presently known, it can be speculated that since coagulant precipitation is sensitive to both micro- and macro-mixing, scale-up must consider not only energy dissipation rate, but also the reaction injection point and the contacting method.”
 - [Mixing in Coagulation and Flocculation 1991 page 292](https://books.google.com/books/about/Mixing_in_coagulation_and_flocculation.html?id=dkFSAAAAMAAJ)



Rapid mix units often require significant energy and this has led some municipal water treatment plant operators to experiment with turning off rapid mix units. There is a need to understand the physical and chemical processes that occur when a concentrated liquid coagulant is added to water.

# Coagulant nanoparticle application
Rapid mix sets the stage for aggregation of both suspended particles and dissolved substances. Particle and dissolve substance aggregation is mediated by coagulant nanoparticles. The nanoparticles attach to raw water particles as well as to some dissolved species (the topic of these notes). After the nanoparticles have been mixed with the raw water and have attached to raw water particles the next process, flocculation, can begin. Flocculation is the process of producing collisions between particles to create flocs (aggregates) (next set of notes).

Nanoparticle application includes multiple steps that must occur before the raw water particles can begin to aggregate. The sticky nanoparticles can be aluminum $(Al^{+3})$ or iron $(Fe^{+3})$ based and in either case the nanoparticles are formed from precipitated hydroxide species $(Al(OH)_3)$ or $(Fe(OH)_3)$. The series of events that are contained in the broad designation of "rapid mix" are:

1. Liquid coagulant stock solution with a low pH is injected into the raw water
1. Turbulent eddies randomize the fluids (but don't blend them)
    1. Large scale eddies mix the coagulant with the raw water by creating large fluid deformations. This stretching and turning of the raw water and coagulant is analogous to shuffling a deck of cards. The cards are randomized, but the cards maintain their identity. The original liquids retain their chemical composition.
    1. Turbulent eddies disintegrate into smaller and smaller eddies.
    1. At a very small scale (Inner viscous length scale) viscosity becomes significant and the kinetic energy of the eddies begins to be converted to heat by viscosity.  
1. The coagulant is blended with the raw water by molecular diffusion
1. The higher pH of the raw water causes the coagulant to begin to precipitate as $Al_{12}AlO_4(OH)_{24}(H_2O)_{12}^{7+}$, an aluminum, Al, nanoparticle.
1. The precipitating $Al_{13}$ molecules aggregates with other nearby $Al_{13}$ molecules to form aluminum hydroxide nanoparticles. It is also possible that the nanoparticles are already formed in the coagulant stock suspension. Polyaluminum chloride stock solutions turn white in about a year at room temperature and this suggests that nanoparticles have reached
1. The Al nanoparticles attach to other dissolved species and suspended particles.
1. Molecular diffusion causes some dissolved species and Al nanoparticles to aggregate.
1. Fluid shear and molecular diffusion cause Al nanoparticles with attached formerly dissolved species to collide with inorganic particles (such as clay) and organic particles (such as viruses, bacteria, and protozoans).

These multiple steps cover a wide range of length scales and it is not clear at the onset which processes might be the rate limiting steps. We will develop time scale estimates for several of these steps to help identify which processes will likely require the most attention to design. Many of these processes are presumed to occur in parallel.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/rapid%20mix%20macro%20to%20nano%20scale.png" width="800">

**Figure x:**. Transport of coagulant nanoparticles occurs over length scales ranging from meter to a fraction of a nanometer.

## Energy Dissipation Rate, Velocity Gradient, and Mixing
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

These concepts and their interactions first become relevant in Rapid Mix, the step in which the coagulant gets added to the raw water.

The two concepts that were not covered in the previous chapter, [fluids review](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Fluids_Review_Design.md), are velocity gradient $G$ and energy dissipation rate $\varepsilon$. While these will be very thoroughly described over the course of this introduction, a brief and simple explanation is included to help get the ball rolling.

### Understanding $G$ and $\varepsilon$

$G$, or velocity gradient, is a measure of fluid deformation. It is defined by how quickly one point of water along one streamline moves in comparison to another point on another streamline ($v_A$ compared to $v_B$, for example), taking into account the distance between the streamlines, $\Delta h$. A visual example of a velocity gradient is shown in the image below:

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Velocity_gradient_image.jpg" width=700></center>

</br>

**Note on terminology:** "Fluid deformation" is equivalent to "velocity gradient," and the two terms can be used interchangeably. They are different ways of thinking about the same concept. Thus, $G$ is the measure of both terms.

$\varepsilon$, or energy dissipation rate, is the rate that the kinetic energy of the fluid is being converted to heat. EDR is a very useful concept because the last step of converting kinetic energy into heat is accomplished by viscosity ($\nu$). This kinetic energy being dissipated by viscosity is the energy associated with velocity gradients ($G$). Thus, through EDR there is a direct connection between $\nu$ and $G$. This connection will be further covered later on in this introduction.

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/EDR_image.jpg" width=700></center>

As mentioned above, EDR and velocity gradients play an important role in mixing and in causing suspended particles to collide with each other, both of which are important topics in flocculation. Their use is not limited to flocculation, they are also helpful in understanding failure modes of plate settlers ([Sedimentation](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Sedimentation)) and terminal head loss of sand filters ([Filtration](https://github.com/AguaClara/CEE4540_Master/tree/master/AguaClara%20Water%20Treatment%20Plant%20Design/Filtration)).

We will begin by defining the concept of energy dissipation rate for a control volume. In a control volume that does not include pumps, turbines or other external energy sources or sinks, the mechanical energy lost is indicated by a change in elevation and quantified as $g h_L$. That mechanical energy is lost in the time that the fluid is in the control volume, $\theta$.

$$ \bar\varepsilon \theta = g h_L$$

This equation simply states that the average rate of energy dissipation times the time over which that dissipation occurs is equal to the total lost mechanical energy. The dimensions of $\varepsilon$ are:

$$ \varepsilon = \frac{[m^3]}{[s^3]} = {\rm \frac{W}{kg}} $$

These dimensions can be understood as a velocity squared per time, otherwise known as a rate of kinetic energy loss (recall that kinetic energy is ${\rm Ke} = \frac{v^2}{2g}$, or ${\rm Ke} \propto v^2$), or as power per unit mass, which would be ${\rm \frac{W}{kg}}$.

Velocity gradients are central to flocculation because they cause the deformation of the fluid, and this results in particle collisions. Consider a real-world example via the image below: if everyone on a sidewalk is walking in the same direction at exactly the same velocity, then there will never be any collisions between people (top). If, however, people at one side of the sidewalk stand still and people walk progressively faster as a function of how far they are away from the zero velocity side of the sidewalk, then there will be many collisions between the pedestrians.  Indeed, the rate of collisions is proportional to the velocity gradient.

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Pedestrians_on_sidewalk.jpg" width=600></center>
