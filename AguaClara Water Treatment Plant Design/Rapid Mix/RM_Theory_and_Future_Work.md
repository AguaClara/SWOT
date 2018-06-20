# Rapid Mix Theory and Future Work
## **Previously in EDR and G Section** (delete this header once you are reacquainted with the document)
### Equations for $\varepsilon$ and $G$ in Varying Flow Geometries

Estimation of velocity gradients for various flow geometries is the basis for the design of rapid mix, flocculators, and plate settlers. Thus, our goal is to define the velocity gradients consistently across a range of possible flow regimes. There are three approaches to calculating the average velocity gradient within a control volume.
1) Use the Navier Stokes equations and solve for the spatially averaged velocity gradient.
1) Use Computational Fluid Dynamics (CFD) to solve for the spatially averaged velocity gradient.
1) Use the total mechanical energy loss in the control volume to calculate the energy dissipation rate. Estimate the velocity gradient directly from the energy dissipation rate, $G_{CS} = \sqrt{\frac{\bar\varepsilon}{\nu}}$, as defined by Camp and Stein in 1943 (Camp, T. R., and Stein, P. C. (1943) ‘‘Velocity Gradients and Hydraulic Work in Fluid Motion,’’ J. Boston Soc. Civil Eng., 30, 203–221.).

The first approach would be ideal but is difficult in practice because Navier Stokes solutions are only available for limited geometries and laminar flow. CFD could be used but is difficult to use as a general engineering design approach given the large number of geometries that are used in drinking water treatment plants. For these reasons we will use the control volume approach to estimate the average velocity gradient. This method incorrectly assumes that the energy dissipation rate is completely uniform in the control volume and hence the velocity gradient is also uniform. This method results in an over estimation of the velocity gradient.

The Camp-Stein estimate of $G_{CS}$ is based on a control volume where the velocity gradient is uniform. Consider a layer of fluid of depth $H$ and apply a velocity, $v$ at the top of the fluid. The velocity gradient, $G$, is thus $\frac{v}{H}$ everywhere in the fluid. The force required to move the top of the fluid at velocity v can be obtained from the required shear, $\tau$. From Newtons Law of Friction we have

$$\tau = \mu \frac{v}{H} = \mu G = \nu\rho G$$

Where $\tau$ is the force required per unit plan view area. The power per unit area required to move the fluid at velocity $v$ is $\tau v$. The mass per unit area is $\rho H$. Thus the energy dissipation rate or the power per mass is

$$\varepsilon = \frac{P}{m} = \frac{\tau v}{\rho H} = \frac{\nu \rho G v}{\rho H} = \nu G^2 $$

This equation has no approximations, but has one very important assumption. We derived this equation for a control volume where the velocity gradient was **uniform**. The reactors and control volumes that we will be using as we design water treatment plants will **not** have uniform velocity gradients. Indeed, several of the water treatment processes will be turbulent and thus the velocity gradients in the fluid will vary in both space and time. Even in laminar flow in a pipe the velocity gradient is far from uniform with high velocity gradients at the wall and zero velocity gradient at the center of the pipe.

We'd like to know if we can apply the previous equation
$$\varepsilon = \nu G^2 $$

to the case where the energy dissipation rate and velocity gradients are nonuniform by simply introducing average values of both quantities.

$$\bar\varepsilon \overset{?}{=} \nu \bar G^2 $$

We will test this option with a simple case. Consider a hypothetical reactor (case 2) that is 4 times as large in plan view area as the uniform velocity gradient case explored above (case 1). In addition, assume that 3/4 of the reactor has a velocity gradient of zero. The average energy dissipation rate for case 1 is

$$\bar \varepsilon_1 = \frac{P_1}{m_1} =  \nu \bar G_1^2 $$

The average energy dissipation rate for case 2 is
$$\bar \varepsilon_2 = \frac{P_1}{4m_1} = \frac{\bar \varepsilon_1}{4} $$
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
| Expansions | $h_e =  K\frac{\bar v_{out}^2}{2g}$ | $\bar\varepsilon = K\frac{\bar v_{out}^3}{2H}$ | $G_{CS} = \bar v_{out}\sqrt{\frac{K\bar v_{out}}{2H\nu}}$ | - |

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

$$ \bar\varepsilon = \frac{P}{m} = \frac{P}{\rho \rlap{-}V}$$

where
* $P$ = power input into the control volume
* $m$ = mass of fluid in the control volume
* $\rlap{-}V$ = volume of the control volume
* $\rho$ = density of the fluid

The Camp-Stein velocity gradient in a mechanically mixed reactor is

$$ G_{CS} = \sqrt{\frac{P}{\rho \nu \rlap{-}V}} $$


## **Previously in Rapid Mix Intro Section** (delete this header once you are reacquainted with the document)

<font color="red">Our understanding of rapid mix is currently quite speculative. This is an area that requires substantial research. We have anecdotal evidence that the process of transporting coagulant nanoparticles to suspended particle surfaces may be a slow, rate-limiting process. Dissolved organic matter may influence the rate of coagulant nanoparticle transport by effectively increasing the size of the coagulant nanoparticles and thus reducing the diffusion rate.

Developing a fundamental understanding of the mixing and transport processes that occur between coagulant addition and flocculation is a very high priority for the AguaClara program.</font>

## Estimates of time required for mixing processes
### Turbulent mixing
#### Large scale eddies at the dimension of flow

The first step in mixing is at the large scale of the dimension of the largest eddies where the dimension of the largest eddies is the smallest dimension normal to the direction of flow. Thus in a pipe the dimension of the largest eddies is set by the pipe diameter. In a open channel the dimension of the largest eddies is usually the water depth although it could be the width of the channel for the case of a narrow tall channel.

We can use the eddy velocity to estimate how long it will take for an eddy to cross the smallest dimension of flow. Eddy velocity is $v_{eddy} \approx \left( \bar\varepsilon \, L_{eddy} \right)^\frac{1}{3}$. The "$\approx$" indicates that this relationship is the same order of magnitude.  In a pipe we have
$$v_{eddy} \approx \left( \bar\varepsilon \, D \right)^\frac{1}{3} $$

For a long straight pipe
$\bar\varepsilon = \frac{\rm{f}}{2} \frac{\bar v^3}{D}$ and thus we can obtain the ratio between mean velocity and the velocity of the large scale eddies.

$$v_{eddy} \approx \left( \frac{\rm{f}}{2} \frac{\bar v^3}{D} \, D \right)^\frac{1}{3} $$

$$\frac{v_{eddy}}{\bar v} \approx \left( \frac{\rm{f}}{2}   \right)^\frac{1}{3} $$

Given a friction factor of 0.02, the eddy velocity is approximately 20% of the mean velocity. We can use this ratio to estimate how many pipe diameters downstream from an injection point will the coagulant be mixed across the diameter of the pipe.

$$ N_{D_{pipe}} \approx \frac{\bar v}{v_{eddy}} \approx \left(\frac{2}{\rm{f}} \right)^\frac{1}{3} $$

Where $N_{D_{pipe}}$ is the distance in number of pipe diameters downstream of the injection point where complete mixing will have occurred. This estimate is a minimum distance and a factor of safety of 2 or more would reasonably be applied. In addition it is best practice to inject the coagulant in the center of the pipe. Injecting the coagulant at the side of the pipe will require considerably greater distance downstream for mixing across the pipe.

```python
print((0.02/2)**(1/3))

```


#### Inner viscous length scale
The smallest scale at which inertia containing eddies causes mixing is set by the final damping of inertia by viscosity. Turbulence occurs when fluid inertia is too large to be damped by viscosity. The ratio of inertia to viscosity is given by the Reynolds number, $\rm Re$:

$${\rm{Re}} = \frac{\bar vD}{\nu}$$
Flows with high Reynolds numbers are turbulent (inertia dominated) and with low Reynolds are laminar (viscosity dominated). The transition Reynolds number is a function of the flow geometry and the velocity and length scale that are used to characterize the flow. In all turbulent flows there is a length scale at which inertia finally loses to viscosity. The scale where viscosity wins is some multiple of the Kolmogorov length scale, which is defined as:

$$\eta_K = \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$

where $\eta_K$ is the Kolmogorov length scale. At the Kolmogorov length scale viscosity completely dampens the inertia of the eddies and effectively "kills" the turbulence.

The length scale at which most of the kinetic energy contained in the small eddies is dissipated by viscosity is the inner viscous length scale, $\lambda_v$, which is about [50 times larger than](http://dimotakis.caltech.edu/pdf/Dimotakis_JFM2000.pdf) the Kolmogorov length scale. Thus we have

$$\lambda_\nu = \Pi_{K\nu}\left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$
{#eq:inner_viscous_length}

where $\Pi_{K\nu} = 50$

At length scales larger than the inner viscous length scale, $\lambda_v$, the dominant transport mechanism is by turbulent eddies. At length scales smaller than $\lambda_v$ the dominant transport mechanism is fluid deformation due to shear. If the flow regime is completely laminar such as in a small diameter tube flocculator, then the dominant transport mechanism is fluid deformation due to shear at length scales all the way up to the diameter of the tubing.

The dividing line between eddy transport and fluid deformation controlled by viscosity can be calculated as a function of the energy dissipation rate using [@eq:inner_viscous_length].

```python
""" importing """
from aide_design.play import*
from aguaclara_research.play import*
import aguaclara_research.floc_model as fm
import matplotlib.pyplot as plt
from matplotlib.ticker import FormatStrFormatter
imagepath = 'AguaClara Water Treatment Plant Design/Rapid Mix/Images/'
EDR_array = np.logspace(0,4,num=50)*u.mW/u.kg
Temperature = 20*u.degC
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
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Inner_viscous_vs_EDR.png" width="400">

**Figure x:** Eddies can cause fluid mixing down to the scale of a few millimeters for energy dissipation rates used in rapid mix units and flocculators.

### Turbulent mixing time as a function of scale

We are searching for the rate limiting step in the mixing process as we transition from the scale of the flow down to the scale of the coagulant nanoparticles. We can estimate the time required for eddies to mix at their length scales by assuming that the eddies pass all of their energy to smaller scales in the time it takes for an eddy to travel the distance equal to the length scale of the eddy. This time is known as the **[eddy turnover time](http://ceeserver.cee.cornell.edu/eac20/cee637/handouts/TURBFLOW_1.pdf)**, $t_{eddy}$. [The derivation for the equation below is found here](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/RM_Derivations.md#t_eddy).

$$t_{eddy} \approx \left( \frac{L_{eddy}^2}{ \bar\varepsilon }\right)^\frac{1}{3} $$

We can plot the eddy turnover time as a function of scale from the inner viscous length scale up to the scale of the flow. We will discover whether large scale mixing by eddies is faster or slower than small scale mixing by eddies.
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
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Eddy_turnover_time.png" width="400">

**Figure x:** Eddy turnover times as a function of length scale for a range of energy dissipation rates.

The eddy turnover times are longest for the largest eddies and this analysis suggests that it only takes a few seconds for turbulent eddies to mix from the scale of the flow down to the inner viscous length scale.

The large scale mixing time is critical for the design of water treatment plants for the case where  the flow is split into multiple treatment trains after coagulant addition. In this case it is critical that the coagulant be mixed equally between all of the treatment trains and thus the mixing times shown in the previous graph represent a minimum time between where the coagulant is added and where the flow is divided into the parallel treatment trains.

It is likely this process of mixing from the scale of the flow down to the inner viscous length scale is commonly referred to as "rapid mix." Here we showed that this mixing is indeed rapid and is really only a concern in the case where the coagulant injection point is very close to the location where the flow is split into multiple treatment trains.

### Shear-diffusion transport
After the first few seconds in which mixing occurs from the length scale of the flow down to the inner viscous length scale the next step in the transport process is blending of the coagulant uniformly with the raw water. At the end of the turbulent transport the coagulant stock has been stretched out into thin bands throughout the raw water, but the two fluids are not actually blended together by turbulence. The blending is accomplished by fluid deformation and then by molecular diffusion.  

#### Fluid deformation by Shear

The time scale for fluid deformation is $1/G$ where $G$ is the velocity gradient. This simple relationship is because the velocity of fluid deformation is proportional to the length scale and thus the time to travel any given distance is always the same. Velocity gradients in conventional mechanized rapid mix units are order 1000 Hz and thus the time for fluid deformation to blur concentration gradients is approximately 1 ms. This confirms the idea that blending the coagulant with the raw water is actually a very fast process with the slowest phase being the transport by turbulent eddies at the scale of reactor.


#### Einstein's diffusion equation

We can estimate the length scale at which fluid shear and diffusion provide transport at the same rate. Einstein's diffusion equation is

$$D_{Diffusion} = \frac{k_B T}{3 \pi \mu d_P}$$

where $k_B$ is the Boltzmann constant and $d_P$ is the diameter of the particle that is diffusion in a fluid with viscosity $\nu$ and density $\rho$. The diffusion coefficient $D_{Diffusion}$ has dimensions of $\frac{[L^2]}{[T]}$ and can be understood as the velocity of the particle multiplied by the length of the mean free path.


From dimensional analysis the time for diffusion to blur a concentration gradient over a length scale, $L_{Diffusion}$ is

$$t_{Diffusion} \approx \frac{L_{Diffusion}^2}{D_{Diffusion}}$$

The shear time scale is $1/G$ and thus we can solve for the length scale at which diffusion and shear have equivalent transport rates.

$$ 1/G \approx t_{Diffusion} \approx \frac{L_{Diffusion}^2}{D_{Diffusion}}  $$

Substitute Einstein's diffusion equation and solve for the length scale that transitions between shear and diffusion transport.

$$L_{Diffusion}^{Shear} \approx \sqrt{\frac{k_B T}{3 G \pi \mu  d_P}}  $$

```python
def L_Shear_Diffusion(G,Temperature,d_particle):
  return np.sqrt((u.boltzmann_constant*Temperature/
  (3 * G *  np.pi *pc.viscosity_dynamic(Temperature)* d_particle)).to_base_units())

G = 100*u.Hz
d_particle = fm.PACl.Diameter*u.m
x = (L_Shear_Diffusion(G,Temperature,d_particle)).to(u.nm)
print(x)
```
Molecular diffusion finishes the blending process by transporting the coagulant nanoparticles the last few hundred nanometers. The entire mixing process from the coagulant injection point to uniform blending with the raw water takes only a few seconds.

We have demonstrated that all of the steps for mixing of the coagulant nanoparticles with the raw water are very fast. Compared with the time required for flocculation, 10s to 1000s of seconds, the time required for this mixing is insignificant. The remaining steps are:
1. Molecular diffusion causes some dissolved species and Al nanoparticles to aggregate.
1. Fluid shear and molecular diffusion cause Al nanoparticles with attached formerly dissolved species to collide with inorganic particles (such as clay) and organic particles (such as viruses, bacteria, and protozoans).


### Length scales of coagulant nanoparticles and clay

The coagulant nanoparticles eventually will attach to clay particles. The clay particles have a diameter of approximately $5 \, {\rm \mu m}$ and thus it is clear from the length scale in the figure above that turbulent eddies aren't able to transport all the way to attachment to clay.

### Diffusion and Shear Transport Coagulant Nanoparticles to Clay

The time required for shear and diffusion to transport coagulant nanoparticles to clay has previously been assumed to be a rapid process. The

* Diffusion blends the coagulant with the raw water sufficiently so that the coagulant precipitates and forms nanoparticles.
* Dissolved organic molecules diffuse to the coagulant nanoparticles and adhere to the nanoparticle surface.
* The coagulant nanoparticles are transported to suspended particle surfaces by a combination of diffusion and fluid shear.

The following is a very preliminary estimate of the time required for attachment of the nanoparticles to the clay particles.
This analysis includes multiple simplifying assumptions and there is a reasonable possibility that some of those assumptions are wrong. However, the core assumptions that coagulant nanoparticles are transported to clay particles by a combination of fluid deformation (shear) and molecular diffusion is reasonable.

The volume of the suspension that is cleared of nanoparticles is proportional to a collision area defined by a ring around the clay particle with width of the diameter of the nanoparticle diffusion band. This diffusion band is the length scale over which diffusion is able to transport coagulant particles to the clay surface during the time that the nanoparticles are sliding past the clay particle.
$$ \propto \pi \, d_{Clay} \, L_{Diff_{NC}}$$
The volume cleared is proportional to time
$$ \propto t$$
The volume cleared is proportional to the relative velocity between clay and nanoparticles. This scaling
$$ \propto v_r$$

$$ \bar v_{\rm{Cleared}} = \pi  d_{Clay} \, L_{Diff_{NC}}  v_r  t $$

Use dimensional analysis to get a relative velocity for the long range transport controlled by shear.
$$v_r = f \left( \varepsilon ,\nu ,\Lambda_{Clay} \right)$$


$$v_r = \Lambda_{Clay} f \left( \varepsilon ,\nu \right)$$
$$v_r \approx \Lambda_{Clay} G$$

$$\Lambda_{Clay} = [L]
\, \, \, \, \, \, \,
\varepsilon = \frac{[L]^2}{[T]^3}
\, \, \, \, \, \, \,
\nu = \frac{[L]^2}{[T]}$$


### Diffusion band thickness


<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Diffusion%20length%20scale.png" width="400">

**Figure x:** The time required for shear to transport all of the fluid past the clay so that diffusion can transport the coagulant nanoparticles to the clay surface is significant.

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
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Diffusion_band_thickness.png" width="400">

**Figure x:**  

Using the equation for $L_{Diff}$ above, [we can solve for](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/RM_Derivations.md#t_coagulant%20application) the time required to reach a target efficiency of application of coagulant nanoparticles to clay:

$$t_{coagulant, \, application} = \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} }$$

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
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Coag_attach_time.png" width="400">

**Figure x:** An estimate of the time required for 80% of the coagulant nanoparticles to attach to clay particles given a raw water turbidity of 10 NTU.

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
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Coag_attach_head_loss.png" width="400">

**Figure x:**  The total energy required to attach coagulant nanoparticles to raw water inorganic particles increases rapidly with the velocity gradient used in the rapid mix process.

There is often a tradeoff between reactor volume and energy input. The reactor volume results in a higher capital cost and the energy input requires both higher operating costs and higher capital costs. This provides an opportunity to optimize rapid mix design once we have a confirmed model characterizing the process.

The total potential energy used to operate an AguaClara plant is approximately 2 m. This represents the difference in elevation between where the raw water enters the plant and where the filtered water exits the plant. If we assume that the rapid mix energy budget is a fraction of that total and thus for subsequent analysis we will assume somewhat arbitrarily that the energy available to attach the coagulant nanoparticles to the raw water particles is 50 cm.  

[We solve the coagulant transport model](), $t_{coagulant, \, application} = \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} }$, for G given a head loss.


$$G_{coagulant, \, application} =  d_{Clay}\left(\frac{\pi k \,g\Delta h }{2.3p C_{NC} \, \Lambda_{Clay}^2 \nu} \right)^\frac{3}{4} \left( \frac{2k_B T }{3 \pi \,\mu  \, d_{NC} }\right)^\frac{1}{4}$$

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


### Jet Mixing

In both mixing for the application of coagulant nanoparticles and for flocculation we have the goal of deforming the fluid to facilitate collisions between particles. As engineers we need to design reactors that deform the fluid. There are several approaches
* coiled tube flocculators (laminar flow)
* rotating propellers
* hydraulic jet

Coiled tube flocculators are commonly used by AguaClara Cornell researchers for small laboratory scale (a few mL/s) experiments.

[add equations here for coiled flocculators]

## Conventional Rapid Mix



### Maximum velocity gradients


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
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Mechanical_RM_Gt.png" width="400">

**Figure x:** Mechanical rapid mix units use a wide range of velocity gradients and residence times.




Conventional rapid mix units use mechanical or potential energy to generate intense turbulence to begin the mixing process. Conventional design is based on the use of $\bar G$ (an average velocity gradient) as a design parameter. We don’t yet know what the design objective is for rapid mix and thus it isn’t clear which parameters matter. We hypothesize that both velocity gradients that cause deformation of the fluid and time for molecular diffusion are required to ultimately transport coagulant nanoparticles to the surfaces of clay particles.

The velocity gradient can be obtained from the rate at which mechanical energy is being dissipated and converted to heat by viscosity.

$$ \varepsilon = G^2 \nu $$

where $\varepsilon$ is the energy dissipation rate, $G$ is the velocity gradient, and $\nu$ is the kinematic viscosity of water.
We can estimate the power input required to create a target energy dissipation rate for a conventional design by noting that power is simple the energy dissipation rate times the mass of water in the rapid mix unit.

$$P = \bar\varepsilon \rlap{-}V \rho $$

$$ P = \bar G^2 \nu \rlap{-}V \rho $$

We can relate reactor volume to a hydraulic residence time, $\theta$, and volumetric flow rate, Q.

$$ P = \rho \bar G^2 \nu Q \theta $$

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


<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Backmix.jpg" width="400">

**Figure x:**	Open tank, backmix system that uses a relatively large tank with a submerged impeller.  

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Inline.jpg" width="400">

**Figure x:**	Enclosed mix system that uses a relatively small volume.




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

$$\bar v_{Jet} \cong \frac{\left( D_{Jet} \, \varepsilon_{Max} \right)^{\frac{1}{3}}}{\Pi_{JetRound}}$$

$$h_e = \frac{ \left( D_{Jet} \, \varepsilon_{Max} \right)^{\frac{2}{3}}}{ 2g \Pi_{JetRound}^2}$$

$$h_e = \frac{ \left( \frac{4 \Pi_{JetRound} Q \varepsilon_{Max}^2}{\pi} \right)^{\frac{2}{7}}}{2 g \Pi_{JetRound}^2}$$

**Off-slide**
$$Q = \frac{D_{Jet}^{\frac{7}{3}} \pi \varepsilon_{Max}^{\frac{1}{3}}}{4 \Pi_{Jet}}$$
