
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

```python
""" importing """
from aide_design.play import*
from aguaclara_research.play import*
import aguaclara_research.floc_model as fm
import matplotlib.pyplot as plt
from matplotlib.ticker import FormatStrFormatter
imagepath = 'AguaClara Water Treatment Plant Design/Chapter 3_Rapid Mix/Images/'
Temperature = 15*u.degC
```

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

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/rapid%20mix%20macro%20to%20nano%20scale.png" width="800">

Figure x.

## Transport steps
* Turbulence
  * Large scale eddies
  * Inner viscous length scale
* Shear-diffusion transport
  * Estimate diffusion time scale
  * Einstein's diffusion equation


## Length and time scales for each of the processes
Let's begin by describing the coagulant injection for a 60 L/s plant. We will use a linear flow orifice meter with 20 cm of head loss.

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
V_lfom = (Q_plant/pc.area_circle(pipe.ID_SDR(ND_LFOM,SDR_LFOM))).to_base_units()
print(V_lfom)
```

The LFOM requires a 16 inch diameter pipe. How long will it take for turbulent eddies to mix the coagulant across the area of the pipe? We will use a rule of thumb that the velocity of the largest eddies is about 10% of the mean velocity. We can use the eddy velocity to estimate how long it will take for an eddy to cross the diameter of the pipe.

We will eventually develop designs for hydraulic devices to accomplish the multiple steps of transporting coagulant nanoparticles to interactions with dissolved and suspended contaminants. Initially we will assume that a design has been created that results in an energy dissipation rate of $1\frac{W}{kg}$.

The smallest scale that

We can estimate the characteristic velocity of any size of eddy based on the assumption that the rate of loss of energy

| length scale | Length | Time | Velocity |
| - | - | - | - |
|largest eddies | flow dimension perpendicular to the mean velocity |  | |

$\epsilon \sim \frac{u^3}{L}$


```python

V_lfom = (Q_plant/pc.area_circle(pipe.ID_SDR(ND_LFOM,SDR_LFOM))).to_base_units()
print(V_lfom)
t_large_scale_mix = (pipe.ID_SDR(ND_LFOM,SDR_LFOM)/(0.1*V_lfom)).to_base_units()
print(t_large_scale_mix)
```
The smallest scale at which inertia containing eddies causing mixing is set by the final damping of inertia by viscosity. Turbulence occurs when fluid inertia is too large to be damped by viscosity. The ratio of inertia to viscosity is given by the Reynolds number.

$${\rm{Re}} = \frac{VD}{\nu}$$
Flows with high Reynolds numbers are turbulent (inertia dominated) and with low Reynolds are laminar (viscosity dominated). The transition Reynolds number is a function of the flow geometry and the velocity and length scale that are used to characterize the flow. In all turbulent flows there is a length scale at which inertia finally loses to viscosity. The scale where viscosity wins is some multiple of the Kolmogorov length scale, which is defined as:

$$\eta_K = \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$

where $\eta_K$ is the Kolmogorov length scale. At the Kolmogorov length scale viscosity completely dampens the inertia of the eddies and effectively "kills" the turbulence.

The length scale at which most of the kinetic energy contained in the small eddies is dissipated by viscosity is the inner viscous length scale, $\lambda_v$, which is about [50 times larger than](http://dimotakis.caltech.edu/pdf/Dimotakis_JFM2000.pdf) the Kolmogorov length scale. Thus we have

$$\lambda_\nu = \Pi_{K\nu}\left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$
where $\Pi_{K\nu} = 50$
```python
EDR_array = np.logspace(0,4,num=50)*u.mW/u.kg
Temperature = 20*u.degC
fm.RATIO_KOLMOGOROV
def Inner_viscous(EDR, Temperature):
	return fm.RATIO_KOLMOGOROV * fm.eta_kolmogorov(EDR, Temperature)

fig, ax = plt.subplots()
ax.semilogx(EDR_array.to(u.mW/u.kg),Inner_viscous(EDR_array, Temperature).to(u.mm))
ax.yaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.xaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.set(xlabel='Energy dissipation rate (W/kg)', ylabel='Inner viscous length scale (mm)')
ax.text(30, 6, 'Eddies cause mixing', fontsize=12,rotation=-30)
ax.text(1, 5, 'Shear and diffusion cause mixing', fontsize=12,rotation=-30)
fig.savefig(imagepath+'Inner_viscous_vs_EDR')
plt.show()
```
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Inner_viscous_vs_EDR.png" width="400">

Figure x. Eddies can cause fluid mixing down to the scale of a few millimeters for energy dissipation rates used in rapid mix units and flocculators.

We are searching for the rate limiting step in the mixing process as we transition from the scale of the flow down to the scale of the coagulant nanoparticles. We can estimate the time required for eddies to mix at their length scales by assuming that the eddies pass all of their energy to smaller scales in the time it takes for an eddy to travel this distance equal to the length scale of the eddy. This time is known as the *[eddy turnover time](http://ceeserver.cee.cornell.edu/eac20/cee637/handouts/TURBFLOW_1.pdf)*.

$$T_{eddy} \sim \frac{L_{eddy}}{u_{eddy}} $$

The rate of energy loss to smaller scales is
$$ \epsilon \sim\frac{u_{eddy}^2}{T_{eddy}} $$

Combining the two equations
$$ \epsilon \sim\frac{u_{eddy}^3}{L_{eddy}} $$

We can use this equation to estimate the eddy velocity given an energy dissipation rate.
$$u_{eddy} \sim \left( \epsilon \, L_{eddy} \right)^\frac{1}{3} $$
Now we can solve for the eddy turnover time which is a measure of the mixing time at the eddy scale.

$$T_{eddy} \sim \frac{L_{eddy}}{\left( \epsilon \, L_{eddy} \right)^\frac{1}{3}} $$

$$T_{eddy} \sim \left( \frac{L_{eddy}^2}{ \epsilon }\right)^\frac{1}{3} $$

We can plot the eddy turnover time as a function of scale from the inner viscous length scale up to the scale of the flow.
```python
EDR_graph = np.array([0.01,0.1,1,10 ])*u.W/u.kg
Temperature
"""Use the highest EDR to estimate the smallest length scale"""
Inner_viscous_graph = Inner_viscous(EDR_graph[2], Temperature)
Inner_viscous_graph
L_flow = 0.5*u.m
L_scale = np.logspace(np.log10(Inner_viscous_graph.magnitude),np.log10(L_flow.magnitude),50)
L_scale
fig, ax = plt.subplots()
for i in range(len(EDR_graph)):
  ax.semilogx(L_scale,((L_scale**2/EDR_graph[i])**(1/3)).to_base_units())

ax.legend(EDR_graph)

#ax.yaxis.set_major_formatter(FormatStrFormatter('%.f'))
#ax.xaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.set(xlabel='Length (m)', ylabel='Eddy turnover time (s)')
fig.savefig(imagepath+'Eddy_turnover_time')
plt.show()
```
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Eddy_turnover_time.png" width="400">

Figure x. Eddy turnover times as a function of length scale for a range of energy dissipation rates.

The eddy turnover times are longest for the largest eddies and this analysis suggests that it only takes a few seconds for turbulent eddies to mix from the scale of the flow down to the inner viscous length scale.

This large scale mixing time is critical for the design of water treatment plants where after coagulant addition the flow is split into multiple treatment trains. In this case it is critical that the coagulant be mixed equally between all of the treatment trains and thus the mixing times shown in the previous graph represent a minimum time between where the coagulant is added and where the flow is divided into the parallel treatment trains.

##### Example problem: Energy dissipation rate in a straight pipe
A water treatment plant that is treating 120 L/s of water injects the coagulant into the middle of the pipe that delivers the raw water to the plant and then splits the flow into 2 parallel treatment trains for subsequent flocculation. Estimate the minimum distance between the injection point and the flow split. You may assume the pipe diameter was selected to have less than 10 cm  of head loss per meter of pipe length.

Solution scheme
1) Use straight pipe head loss equations to estimate the size of the pipe
1) Round up to the nearest available pipe size that meets the head loss criteria
1) Calculate the actual head Loss
$$ \epsilon = \frac{gh_{\rm{f}}}{\theta} $$

The residence time can be expressed as a function of Length and velocity.
$$ \theta = \frac{L}{V}  $$

$$h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{V^2}{2g}$$

Combining the 3 previous equations we obtain the energy dissipation rate for pipe flow
$$ \epsilon = \frac{\rm{f}}{2} \frac{V^3}{D} $$

For the case of laminar flow in a straight pipe we have

$$\rm{f} = \frac{64}{Re}$$

and thus the energy dissipation rate in a straight pipe under conditions of laminar flow is
$$ \epsilon =\frac{32}{Re}  \frac{V^3}{D} $$

We can combine the equation that estimates the largest eddy velocity and the
$$  \epsilon = \frac{\rm{f}}{2} \frac{V^3}{D}  \sim\frac{u_{eddy}^3}{L_{eddy}} $$

Solve for the ratio of the eddy velocity to the mean flow velocity and note that the length scale for the largest eddy is the diameter of the pipe.

$$ N_{D_{pipe}} \sim \frac{V}{u_{eddy}} \sim \left(\frac{2}{\rm{f}} \right)^\frac{1}{3} $$

Where $N_{D_{pipe}}$ is the distance in number of pipe diameters downstream of the injection point where complete mixing will have occurred. The velocity ratio can be used to estimate the distance required for mixing perpendicular to the flow direction in a straight pipe.

#### Design challenge
Estimate the minimum distance between the injection point and the location where the flow is split into two treatment trains for a 16 inch nominal pipe diameter SDR 26 with a flow of 120 L/s. The pipe is PVC. The water temperature is $0^{\circ}C$.

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
What about {{L_mixing}}

```python
Mix_HRT = np.array([0.5,15,25,35,85])*u.s
Mix_G = np.array([4000,1500,950,850,750])/u.s
Mix_CP = np.multiply(Mix_HRT, np.sqrt(Mix_G))
Mix_Gt = np.multiply(Mix_HRT, Mix_G)
Mix_EDR = (Mix_G**2*pc.viscosity_kinematic(Temperature))

fig, ax = plt.subplots()
ax.plot(Mix_G.to(1/u.s),Mix_HRT.to(u.s),'o')
ax.yaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.xaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.set(xlabel='Velocity gradient (Hz)', ylabel='Residence time (s)')
fig.savefig(imagepath+'Mechanical_RM_Gt')
plt.show()

```
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Mechanical_RM_Gt.png" width="400">

Figure x. Mechanical rapid mix units use a wide range of velocity gradients and residence times.

```python

```

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
V_Coag_injection = ((2 * u.gravity * HL_Coag_injection)**0.5).to(u.m/u.s)
print(V_Coag_injection)
D_Coag_injection_min = pc.diam_circle(Q_PACl_max/V_Coag_injection)
print(D_Coag_injection_min.to(u.mm))
```   


## Mixing length scale and transport mechanisms

The next step is turbulent eddy shuffling of the fluid packets. Turbulent eddies distort the fluid such that the coagulant is mixed with the raw water. There are three critical goals of this shuffling.
1. If the plant design calls for the flow to be split between several flocculators, then it is critical that the coagulant be sufficiently mixed with the raw water prior to the splitting of the flow so that each flocculator receives the same coagulant dose.
1. The turbulent eddies shuffle the fluid packets down to the scale of the smallest eddies. (We need to figure out what this scale is!)
1. Fluid deformation (shear) and molecular diffusion cause Al nanoparticles to collide with inorganic particles




### Length scales of coagulant nanoparticles and clay

The coagulant nanoparticles eventually will attach to clay particles. The clay particles have a diameter of approximately $5 \mu m$ and thus it is clear from the length scale in the figure above that turbulent eddies aren't able to transport all the way to attachment to clay.

### Diffusion and Shear Transport Coagulant Nanoparticles to Clay

The time required for shear and diffusion to transport coagulant nanoparticles to clay has previously been assumed to be a rapid process. The

* Diffusion blends the coagulant with the raw water sufficiently so that the coagulant precipitates and forms nanoparticles.
* Dissolved organic molecules diffuse to the coagulant nanoparticles and adhere to the nanoparticle surface.
* The coagulant nanoparticles are transported to suspended particle surfaces by a combination of diffusion and fluid shear.

The following is a very preliminary estimate of the time required for attachment of the nanoparticles to the clay particles.
This analysis includes multiple simplifying assumptions and there is a reasonable possibility that some of those assumptions are wrong. However, the core assumptions that coagulant nanoparticles are transported to clay particles by a combination of fluid deformation (shear) and molecular diffusion is reasonable.

The volume of the suspension that is cleared of nanoparticles is proportional to a collision area defined by a ring around the clay particle with width of the diameter of the nanoparticle diffusion band. This diffusion band is the length scale over which diffusion is able to transport coagulant particles to the clay surface during the time that the nanoparticles are sliding past the clay particle.
$$\propto \pi \, d_{Clay} \, L_{Diff_{NC}}$$
The volume cleared is proportional to time
$$ \propto t$$
The volume cleared is proportional to the relative velocity between clay and nanoparticles. This scaling
$$ \propto v_r$$

$$ V_{\rm{Cleared}} = \pi  d_{Clay} \, L_{Diff_{NC}}  v_r  t $$

Use dimensional analysis to get a relative velocity for the long range transport controlled by shear.
$$v_r = f \left( \varepsilon ,\nu ,\Lambda_{Clay} \right)$$


$$v_r = \Lambda_{Clay} f \left( \varepsilon ,\nu \right)$$
$$v_r \approx \Lambda_{Clay} G$$

$$\Lambda_{Clay} = \left[ {\rm{L}} \right]
\, \, \, \, \, \, \,
\varepsilon = \left[ \frac{{\rm{L}}^2}{{\rm{T}}^3} \right]
\, \, \, \, \, \, \,
\nu = \left[ \frac{{\rm{L}}^2}{{\rm{T}}} \right]$$


### Diffusion band thickness


<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Diffusion%20length%20scale.png" width="400">

Figure x. The time required for shear to transport all of the fluid past the clay so that diffusion can transport the coagulant nanoparticles to the clay surface is significant.

$$D_{Diffusion} = \frac{k_B T}{3 \pi \, \mu \, d_P}$$

$$L_{Diff} \approx \sqrt{D_{Diffusion} t_{Diffusion}} $$

The time for nanoparticles to diffuse through the boundary layer around the clay particle is equal to the distance they travel around the clay particle divided by their velocity. The distance they travel scales with $d_{Clay}$ and their average velocity scales with the thickness of the diffusion layer/2 * the velocity gradient.

$$t_{Diffusion} = \frac{ 2d_{Clay}} {L_{Diff} G}$$

$$L_{Diff} \approx \left( \frac{2k_B T d_{Clay}}{3 \pi \,\mu  \, d_{NC} G}\right)^\frac{1}{3} $$

Let's estimate the thickness of the diffusion band
```python
T_graph = np.linspace(0,30,4)*u.degC
G = np.arange(50,5000,50)*u.Hz

def L_Diff(Temperature,G):
  return (((2*u.boltzmann_constant*Temperature * fm.Clay.Diameter*u.m)/(3 * np.pi *pc.viscosity_dynamic(Temperature)* (fm.PACl.Diameter*u.m)*G))**(1/3)).to_base_units()

fig, ax = plt.subplots()
for i in range(len(T_graph)):
  ax.semilogx(G,L_Diff(T_graph[i],G).to(u.nm))

ax.legend(T_graph)
ax.yaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.xaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.set(xlabel='Velocity gradient (Hz)', ylabel='Diffusion band thickness ($nm$)')
fig.savefig(imagepath+'Diffusion_band_thickness')
plt.show()
```
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Diffusion_band_thickness.png" width="400">

Figure x.
## Collision Rates
$${\rlap{-} V_{\rm{Cleared}}} \approx \pi d_{Clay} L_{Diff_{NC}} v_r t$$

$$t_c = \frac{\Lambda_{NC}^3}{\pi d_{Clay} L_{Diff_{NC} v_r}}$$

$$v_r \approx \Lambda_{Clay} G$$

$$\rlap{-} V_{Occupied} = \Lambda_{Clay}^3$$

This is the average time for a clay particle to have the entire volume of water that it occupies sweep past the clay particle.

$$t_c = \frac{\Lambda_{Clay}^3}{\pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G}$$


$$dN_c = \pi d_{Clay} L_{Diff_{NC}}{\Lambda^{-2}_{Clay}} G dt$$


### Collision Rate and Particle Removal
A fraction of the remaining coagulant nanoparticles are removed during the time required for one sweep past the clay particle.

$$\frac{dn_{NC}}{ - k \, n_{NC}} = dN_c$$

$$\frac{dn_{NC}}{ - k \, n_{NC}} = \pi d_{Clay} L_{Diff_{NC}}{\Lambda^{-2}_{Clay}} G dt$$

### Integrate the coagulant transport model
Integrate from the initial coagulant nanoparticle concentration to the concentration at time t.
$$\int \limits_{n_{NC_0}}^{n_{NC}} n_{NC}^{- 1} \, dn_{NC}  =  - \pi d_{Clay} L_{Diff_{NC}} \Lambda^{-2}_{Clay} G \, k  \int \limits_0^t {dt} $$

Use pC notation to be consistent with how we describe removal efficiency of other contaminants.

$$2.3 p C_{NC} = \pi d_{Clay}\,  L_{Diff_{NC}}\,  \Lambda^{-2}_{Clay}\,  G k  t $$

Solve for the time required to reach a target efficiency of application of coagulant nanoparticles to clay.

$$t = \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} }$$



In the equation above, the first fraction after the equal sign is dimensionless and the square root term has dimensions of time. In the aggregation of clay particles (looking ahead to flocculation) the

The time required for the coagulant to be transported to clay surfaces is strongly dependent on the turbidity as indicated by the average spacing of clay particles, $\Lambda_{Clay}$. As turbidity increases the spacing between clay particles decreases and the time required for shear to transport coagulant nanoparticles to the clay decreases. Increasing the shear also results in faster transport of the coagulant nanoparticles to clay surfaces. The times required are strongly influenced by the size of the coagulant nanoparticles because larger nanoparticles diffuse more slowly.

Below we estimate the time required to achieve 80% attachment of nanoparticles in a 10 NTU clay suspension.

```python
"""I needed to attach units to material properties due to a bug in floc_model. This will need to be fixed when floc_model is updated."""
def Nano_coag_attach_time(pC_NC,C_clay,G,Temperature):
  """We assume that 70% of nanoparticles attach in the average time for one collision."""
  k_nano = 1-np.exp(-1)
  num=2.3*pC_NC*(fm.sep_dist_clay(C_clay,fm.Clay))**2
  den = np.pi * G* k_nano * fm.Clay.Diameter*u.m * L_Diff(Temperature,G)
  return (num/den).to_base_units()

C_Al = 2 * u.mg/u.L
C_clay = 10 * u.NTU
pC_NC = -np.log10(1-0.8)
"""apply 80% of the coagulant nanoparticles to the clay"""

G = np.arange(50,5000,10)*u.Hz

fig, ax = plt.subplots()

for i in range(len(T_graph)):
  ax.semilogx(G,Nano_coag_attach_time(pC_NC,C_clay,G,T_graph[i]))

ax.semilogx(Mix_G.to(1/u.s),Mix_HRT.to(u.s),'o')
ax.legend([*T_graph, "Conventional rapid mix"])
"""* is used to unpack T_graph so that units are preserved when adding another legend item."""
ax.yaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.xaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.set(xlabel='Velocity gradient (Hz)', ylabel='Nanoparticle attachment time (s)')
fig.savefig(imagepath+'Coag_attach_time')
plt.show()
```
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Coag_attach_time.png" width="400">

Figure x. An estimate of the time required for 80% of the coagulant nanoparticles to attach to clay particles given a raw water turbidity of 10 NTU.

### Energy tradeoff for coagulant transport
$$  \Delta h =   \frac{G^2 \nu \theta}{g} $$
```python
Nano_attach_time = Nano_coag_attach_time(pC_NC,C_clay,G,Temperature)

def HL_coag_attach(pC_NC,C_clay,G,Temperature):
  return (G**2*pc.viscosity_kinematic(Temperature)*Nano_attach_time/u.gravity).to(u.cm)

fig, ax = plt.subplots()

for i in range(len(T_graph)):
  ax.loglog(G,HL_coag_attach(pC_NC,C_clay,G,T_graph[i]))

ax.legend(T_graph)
ax.yaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.xaxis.set_major_formatter(FormatStrFormatter('%.f'))
ax.set(xlabel='Velocity gradient (Hz)', ylabel='Head loss (cm)')
fig.savefig(imagepath+'Coag_attach_head_loss')
plt.show()

```
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Coag_attach_head_loss.png" width="400">

Figure x  The total energy required to attach coagulant nanoparticles to raw water inorganic particles increases rapidly with the velocity gradient used in the rapid mix process.

There is often a tradeoff between reactor volume and energy input. The reactor volume results in a higher capital cost and the energy input requires both higher operating costs and higher capital costs. This provides an opportunity to optimize rapid mix design once we have a confirmed model characterizing the process.

The total potential energy used to operate an AguaClara plant is approximately 2 m. This represents the difference in elevation between where the raw water enters the plant and where the filtered water exits the plant. If we assume that the rapid mix energy budget is a fraction of that total and thus for subsequent analysis we will assume somewhat arbitrarily that the energy available to attach the coagulant nanoparticles to the raw water particles is 50 cm.  

We solve the coagulant transport model for G given a head loss.

$$t = \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} }$$

$$  \Delta h =   \frac{G^2 \nu \theta}{g} $$

Replace $\theta$ with t.

$$  \Delta h =  \frac{G^2 \nu}{g} \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} } $$

$$L_{Diff} \approx \left( \frac{2k_B T d_{Clay}}{3 \pi \,\mu  \, d_{NC} G}\right)^\frac{1}{3} $$

$$  \Delta h =  \frac{G^2 \nu}{g} \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}} \left( \frac{3 \pi \,\mu  \, d_{NC} G}{2k_B T d_{Clay}}\right)^\frac{1}{3}$$


Solve for the velocity gradient.
$$  \Delta h =  \frac{G^\frac{4}{3} \nu}{g} \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi k \, d_{Clay}} \left( \frac{3 \pi \,\mu  \, d_{NC} }{2k_B T d_{Clay}}\right)^\frac{1}{3}$$

$$  G =  d_{Clay}\left(\frac{\pi k \,g\Delta h }{2.3p C_{NC} \, \Lambda_{Clay}^2 \nu} \right)^\frac{3}{4} \left( \frac{2k_B T }{3 \pi \,\mu  \, d_{NC} }\right)^\frac{1}{4}$$

```python
"""find G for target head loss"""
HL_nano_transport = np.linspace(10,100,10)*u.cm
def G_max_head_loss(pC_NC,C_clay,HL_nano_transport,Temperature):
  k_nano = 1-np.exp(-1)
  num = u.gravity * HL_nano_transport * np.pi * k_nano
  den= 2.3 * pC_NC * (fm.sep_dist_clay(C_clay,fm.Clay))**2 * pc.viscosity_kinematic(Temperature)
  num2 = 2 * u.boltzmann_constant * Temperature
  den2 = 3 * np.pi * pc.viscosity_dynamic(Temperature) * (fm.PACl.Diameter*u.m)
  return fm.Clay.Diameter*u.m*((((num/den)**(3) * (num2/den2)).to_base_units())**(1/4))
"""Note the use of to_base_units BEFORE raising to the fractional power.
This prevents a rounding error in the unit exponent."""

G_max = G_max_head_loss(pC_NC,C_clay,20*u.cm,Temperature)
print(G_max)

"""The time required?"""
Nano_attach_time = Nano_coag_attach_time(pC_NC,C_clay,G_max,Temperature)
print(Nano_attach_time)
print(G_max*Nano_attach_time)
```
According to the analysis above, the maximum velocity gradient that can be used to achieve 80% coagulant nanoparticle attachment using only 20 cm of head loss is 142 Hz. This requires a residence time of 100 seconds. These model results must be experimentally verified and it is very likely that the model will need to be modified.

The analysis of the time required for shear and diffusion to transport the coagulant nanoparticles the last few millimeters suggests that it is this last step that requires the most time. Indeed, the time required for coagulant nanoparticle attachment to raw water particles is comparable to the time that will be required for the next step in the processs, flocculation.


## Coagulant attachment mechanism
* Surface charge neutralization hypothesis
  * coagulant nanoparticles attach to each other
  *
* Polar bonds
  * Electronegativity reveals that the aluminum - oxygen bond is more polar than the hydrogen - oxygen bond
  * The bond between a coagulant nanoparticle and a clay surface can potentially be stronger than the bond between a water molecule and the clay surface.

## Design for Mixing
This is all about deforming the fluid.

### Jet Mixing

In both mixing for the application of coagulant nanoparticles and for flocculation we have the goal of deforming the fluid to facilitate collisions between particles. As engineers we need to design reactors that deform the fluid. There are several approaches
* coiled tube flocculators (laminar flow)
* rotating propellers
* hydraulic jet

Coiled tube flocculators are commonly used by AguaClara Cornell researchers for small laboratory scale (a few mL/s) experiments.

[add equations here for coiled flocculators]

## Conventional Rapid Mix

Conventional rapid mix units use mechanical or potential energy to generate intense turbulence to begin the mixing process. Conventional design is based on the use of $
\bar G$ (an average velocity gradient) as a design parameter. We don’t yet know what the design objective is for rapid mix and thus it isn’t clear which parameters matter. We hypothesize that both velocity gradients that cause deformation of the fluid and time for molecular diffusion are required to ultimately transport coagulant nanoparticles to the surfaces of clay particles.

The velocity gradient can be obtained from the rate at which mechanical energy is being dissipated and converted to heat by viscosity.

$$ \epsilon = G^2 \nu $$

where $\epsilon$ is the energy dissipation rate, $G$ is the velocity gradient, and $\nu$ is the kinematic viscosity of water.
We can estimate the power input required to create a target energy dissipation rate for a conventional design by noting that power is simple the energy dissipation rate times the mass of water in the rapid mix unit.

$$P = \epsilon \rlap{--}V \rho $$

$$ P = G^2 \nu \rlap{--}V \rho $$

We can relate reactor volume to a hydraulic residence time, $\theta$, and volumetric flow rate, Q.

$$ P = \rho G^2 \nu Q \theta $$

This equation is perfectly useful for estimating electrical motor sizing requirements for mechanical rapid mix units. For gravity powered hydraulic rapid mix units it would be more intuitive to use the change in water surface elevation, $\Delta h$ instead of power input.

$$P = \rho g Q \Delta h$$

Combining the two equations we obtain.

$$  \Delta h =   \frac{G^2 \nu \theta}{g} $$

Typical values for residence time and average velocity gradient are given below.

| Residence Time (s) | Velocity gradient G (1/s) | Energy dissipation rate (W/kg)  | Equivalent height (m)* |
| - | - | - | - |
| 0.5 | 4000 | 16 | 0.8 |
| 10 - 20 | 1500 | 2.25 | 2.3 - 4.6 |
| 20 - 30 | 950 | 0.9 | 1.8 - 2.8 |
| 30 - 40 | 850 | 0.72 | 2.2 - 2.9 |
| 40 - 130 | 750 | 0.56 | 2.3 - 7.5 |
From Environmental Engineering: A Design Approach by Sincero and Sincero. 1996. page 267.

Rotating propellers can either be installed in open tanks or enclosed in pipes. From a mixing and fluids perspective it doesn't make any difference whether the tank is open to the atmosphere or not. The parameters of interest are the rate of fluid deformation and the residence time in the mixing zone.


<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Backmix.jpg" width="400">

Figure x.	Open tank, backmix system that uses a relatively large tank with a submerged impeller.  

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Inline.jpg" width="400">

Figure x.	Enclosed mix system that uses a relatively small volume.



Chemical Engineering Science, Vol. 50, No. 12, pp. 1877-1880, 1995
THE INFLUENCE OF VISCOSITY ON MIXING IN JET REACTORS
Jo BALDYGA, J. R. BOURNE* and R. V. GHOLAP
Technisch-Chemisches Laboratorium, ETH-Zentrum, CH-8092 Zurich, Switzerland

$$ \varepsilon_{Centerline} \cong \frac{50 D_{Jet}^3 V_{Jet}^3}{ \left( x - 2 D_{Jet} \right)^4}$$

$$ \varepsilon_{Max} \cong \frac{\left( \frac{50}{\left( 5 \right)^4} \right) V_{Jet}^3}{D_{Jet}}$$

$$ \varepsilon_{Max} \cong \frac{\left( \Pi_{RoundJet} V_{Jet} \right)^3}{D_{Jet}}$$

$$\Pi_{RoundJet} \cong 0.5$$

```python
def Energy_dissipation_jet_centerline(D_jet,V_jet,x):
  return (50 * D_jet**3*V_jet**3/(x-2*D_jet)**4).to_base_units()

def Energy_dissipation_jet_max(D_jet,V_jet):
  return (con.RATIO_JET_ROUND * V_jet)**3/D_jet

V_jet = 1 * u.m/u.s
D_jet = 0.1 * u.m
EDR_max = Energy_dissipation_jet_max(D_jet,V_jet)
x=np.linspace(7,20,24)*D_jet
fig, ax = plt.subplots()
ax.plot(x/D_jet,Energy_dissipation_jet_centerline(D_jet,V_jet,x))
ax.set(xlabel='Jet diameters downstream', ylabel='Energy dissipation rate (W/kg)')
fig.savefig(imagepath+'Jet_centerline_EDR')
plt.show()
```

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Jet_centerline_EDR.png" width="400">
### Orifice Diameter to obtain Target Mixing
$$ A_{Orifice} \Pi_{vc} = A_{Jet}$$

$$ D_{Orifice} \sqrt{\Pi_{vc}} = D_{Jet}$$

$$ \varepsilon_{Max} \cong \frac{ \left( \Pi_{JetRound} \frac{4Q}{\pi D_{Jet}^2} \right)^3}{D_{Jet}}$$

$$ D_{Orifice} \cong \left( \frac{4 Q \Pi_{JetRound}}{\varepsilon_{Max}^{\frac{1}{3}} \pi} \right)^{\frac{3}{7}} \frac{1}{\sqrt{\Pi_{vc} }}$$

**Off-slide**
$$\varepsilon_{Max} \cong  \frac{ \left( \Pi_{Jet} \frac{4 Q_{Jet}}{\pi} \right)^3 }{D_{Orifice}^7 \sqrt{\Pi_{vc}^7} }
$$


### Rapid Mix Head Loss
$$ D_{Orifice} \cong \left( \frac{4 Q \Pi_{JetRound}}{\varepsilon_{Max}^{\frac{1}{3}} \pi} \right)^{\frac{3}{7}}$$

$$V_{Jet} \cong \frac{\left( D_{Jet} \, \varepsilon_{Max} \right)^{\frac{1}{3}}}{\Pi_{JetRound}}$$

$$h_e = \frac{ \left( D_{Jet} \, \varepsilon_{Max} \right)^{\frac{2}{3}}}{ 2g \Pi_{JetRound}^2}$$

$$h_e = \frac{ \left( \frac{4 \Pi_{JetRound} Q \varepsilon_{Max}^2}{\pi} \right)^{\frac{2}{7}}}{2 g \Pi_{JetRound}^2}$$

**Off-slide**
$$Q = \frac{D_{Jet}^{\frac{7}{3}} \pi \varepsilon_{Max}^{\frac{1}{3}}}{4 \Pi_{Jet}}$$
