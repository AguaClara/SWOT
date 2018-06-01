<<<<<<< HEAD
=======

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Conventional Rapid Mix](#conventional-rapid-mix)
- [Coagulant nanoparticle application](#coagulant-nanoparticle-application)
	- [Transport steps](#transport-steps)
	- [Length and time scales for each of the processes](#length-and-time-scales-for-each-of-the-processes)
	- [Mixing length scale and transport mechanisms](#mixing-length-scale-and-transport-mechanisms)
		- [Length scales of coagulant nanoparticles and clay](#length-scales-of-coagulant-nanoparticles-and-clay)
		- [Diffusion and Shear Transport Coagulant Nanoparticles to Clay](#diffusion-and-shear-transport-coagulant-nanoparticles-to-clay)
		- [Diffusion band thickness](#diffusion-band-thickness)
	- [Collision Rates](#collision-rates)
		- [Collision Rate and Particle Removal](#collision-rate-and-particle-removal)
		- [Integrate the coagulant transport model](#integrate-the-coagulant-transport-model)
		- [Energy tradeoff for coagulant transport](#energy-tradeoff-for-coagulant-transport)
	- [Coagulant attachment mechanism](#coagulant-attachment-mechanism)
	- [Design for Mixing](#design-for-mixing)
		- [Jet Mixing](#jet-mixing)
		- [Orifice Diameter to obtain Target Mixing](#orifice-diameter-to-obtain-target-mixing)
		- [Rapid Mix Head Loss](#rapid-mix-head-loss)

<!-- /TOC -->

## Introduction

Rapid mix is the term commonly used to describe the processes that occur between the coagulant addition to the raw water and the flocculation tanks. The processes that occur are not well understood and thus design guidelines are empirical.

“In summary, little is known about rapid mix, much less any sensitivity to scale. However, the models and data reviewed suggest the need to be on the lookout for certain effects. From what is presently known, it can be speculated that since coagulant precipitation is sensitive to both micro- and macro-mixing, scale-up must consider not only energy dissipation rate, but also the reaction injection point and the contacting method.”
 - [Mixing in Coagulation and Flocculation 1991 page 292](https://books.google.com/books/about/Mixing_in_coagulation_and_flocculation.html?id=dkFSAAAAMAAJ)

Rapid mix units often require significant energy and this has led some municipal water treatment plant operators to experiment with turning off rapid mix units. There is a need to understand the physical and chemical processes that occur when a concentrated liquid coagulant is added to water.

# Coagulant nanoparticle application
Rapid mix sets the stage for aggregation of both suspended particles and dissolved substances. Particle and dissolve substance aggregation is mediated by coagulant nanoparticles. The nanoparticles attach to raw water particles as well as to some dissolved species (the topic of these notes). After the nanoparticles have been mixed with the raw water and have attached to raw water particles the next process, flocculation, can begin. Flocculation is the process of producing collisions between particles to create flocs (aggregates) (next set of notes).

Nanoparticle application includes multiple steps that must occur before the raw water particles can begin to aggregate. The sticky nanoparticles can be aluminum $(Al^{+3})$ or iron $(Fe^{+3})$ based and in either case the nanoparticles are formed from precipitated hydroxide species $(Al(OH)_3)$ or $(Fe(OH)_3)$. The series of events that are contained in the broad designation of "rapid mix" are:

1. Liquid coagulant with a low pH is injected into the raw water
1. Large scale eddies mix the coagulant with the raw water by creating large fluid deformations. This stretching and turning of the raw water and coagulant is analogous to shuffling a deck of cards. The cards are randomized, but the cards maintain their identity. The original liquids retain their chemical composition.
1. Turbulent eddies disintegrate into smaller and smaller eddies.
1. At a very small scale (Kolmogorov length scale) viscosity becomes significant and the kinetic energy of the eddies is converted to heat by viscosity.  
1. Molecular diffusion causes true blending of the two fluids  
1. The coagulant is diluted by the raw water, the pH of the mixture is higher and the higher pH causes the coagulant to begin to precipitate as $Al_{12}AlO_4(OH)_{24}(H_2O)_{12}^{7+}$, an $Al_{13}$ nanoparticle.
1. The precipitating $Al_{13}$ molecules aggregates with other nearby $Al_{13}$ molecules to form aluminum hydroxide nanoparticles.
1. Molecular diffusion and fluid shear cause the Al nanoparticles,  dissolved species, inorganic particles (such as clay) and organic particles (such as viruses, bacteria, and protozoans) to collide and potential attach.

These multiple steps cover a wide range of length scales and it is not clear at the onset which processes might be the rate limiting steps. We will develop time scale estimates for several of these steps to help identify which processes will likely require the most attention to design.   

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/rapid%20mix%20macro%20to%20nano%20scale.png" width="800">

Figure x.

## Transport steps
* Turbulence
  * Large scale eddies
  * Inner viscous length scale
* Shear-diffusion transport
  * Estimate diffusion time scale
  * Einstein's diffusion equation


>>>>>>> master
## Length and time scales for each of the processes
Let's begin by describing the coagulant injection for a 60 L/s plant. We will use a [linear flow orifice meter](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Flow%20Control%20and%20Measurement/FCM_Design.md#linear-flow-orifice-meter-lfom) with 20 cm of head loss.

```python
Q_plant = 60 * u.L/u.s
HL_LFOM = 20 * u.cm
Pi_LFOM_safety = 1.2
SDR_LFOM = 26
from aide_design.unit_process_design import lfom as lfom
ND_LFOM = lfom.nom_diam_lfom_pipe(Q_plant,HL_LFOM)
print(ND_LFOM, '(',ND_LFOM.to(u.cm), ')')

L_flow = pipe.ID_SDR(ND_LFOM,SDR_LFOM)
L_flow
v_lfom = (Q_plant/pc.area_circle(pipe.ID_SDR(ND_LFOM,SDR_LFOM))).to_base_units()
print(v_lfom)
```

The LFOM requires a 16 inch diameter pipe.

10% velocity rule
```python

v_lfom = (Q_plant/pc.area_circle(pipe.ID_SDR(ND_LFOM,SDR_LFOM))).to_base_units()
print(v_lfom)
t_large_scale_mix = (pipe.ID_SDR(ND_LFOM,SDR_LFOM)/(0.1*v_lfom)).to_base_units()
print(t_large_scale_mix)
```


##### Example problem: Energy dissipation rate in a straight pipe
A water treatment plant that is treating 120 L/s of water injects the coagulant into the middle of the pipe that delivers the raw water to the plant and then splits the flow into 2 parallel treatment trains for subsequent flocculation. The pipe is PVC 16 inch nominal pipe diameter SDR 26. The water temperature is $0^{\circ}C$. Estimate the minimum distance between the injection point and the flow split.

Solution scheme
1) Calculate the friction factor

```python
T_water=0*u.degC
Pipe_roughness = mat.PIPE_ROUGH_PVC
Pipe_roughness
Nu_water = pc.viscosity_kinematic(T_water)
Q_pipe = 120 * u.L/u.s
ND_pipe = 16*u.inch
SDR_pipe = 26
ID_pipe = pipe.ID_SDR(ND_pipe,SDR_pipe)
f_pipe = pc.fric(Q_pipe,ID_pipe,Nu_water,Pipe_roughness)
N_pipe_diameters = (2/f_pipe)**(1/3)
N_pipe_diameters
"""The minimum length for mixing is thus"""
L_mixing = ID_pipe*N_pipe_diameters
print('The minimum distance required for mixing across the diameter of the pipe is ',L_mixing.to_base_units())
```
The previous analysis provides a minimum distance for sufficient mixing so that equal mass flux of coagulant will end up in both treatment trains. This assumes that the coagulant was injected in the pipe centerline. Injection at the wall of the pipe is a poor practice and would require many more pipe diameters because it takes significant time for the coagulant to be mixed out of the slower fluid at the wall.
The time required for mixing at the scale of the flow in the plant is thus accomplished in a few seconds. This ends up being the fastest part of the transport of the coagulant nanoparticles on their way to attachment to the clay particles.

Next we will determine a typical flow rate of coagulant. **Aluminum** concentrations for polyaluminum chloride (PACl) typically range from 1 to 10 mg/L. The maximum PACl stock solution concentration is about 70 g/L as **Al**.

```python
C_PACl_stock = 70 *u.g/u.L
C_PACl_dose_max = 10 * u.mg/u.L
Q_PACl_max = (Q_plant*C_PACl_dose_max/C_PACl_stock).to(u.mL/u.s)
print(Q_PACl_max)
```
We can estimate the diameter of the injection port by setting the kinetic energy loss where the coagulant is injected into the main flow to be 10 cm. The amount of energy we invest in injecting the coagulant into the raw water is a compromise between having to raise the entire chemical feed system including the stock tanks to increase the potential energy and a goal of not having pressure fluctuations inside the LFOM pipe cause flow oscillations in the chemical dosing tube. Thus our goal is to have the kinetic energy at the injection point be large compared with the expected pressure fluctuations in the LFOM.

```python
HL_Coag_injection = 10 * u.cm
v_Coag_injection = ((2 * u.gravity * HL_Coag_injection)**0.5).to(u.m/u.s)
print(v_Coag_injection)
D_Coag_injection_min = pc.diam_circle(Q_PACl_max/v_Coag_injection)
print(D_Coag_injection_min.to(u.mm))
```   
