<<<<<<< HEAD
# Energy Dissipation and Velocity Gradients

Water treatment plants at research and municipal scales deploy a wide range of flow geometries. The following list includes the flow geometries that are commonly used for mixing processes and example locations.

* Straight pipe (wall shear) - [uncommon, but included for completeness]
* Coiled tube (wall shear and expansions) - [research scale mixing]
* Series of expansions (expansions) - [hydraulic flocculators]
* Mechanical mixing - [mechanical rapid mix and flocculators]
* Between flat plates (wall shear) - [plate settlers]
* Round jet -  (expansion) - [hydraulic rapid mix]
* Plane jet - (expansion) - [inlet into sedimentation tank]
* Behind a flat plate - (expansion) - [mechanical mixers]

This section can serve as a convenient reference to the equations and to the equation derivations.

Summary table of equations for control volume averaged values.
| Geometry | $h_L$ |$\bar\varepsilon$ | $G_{CS}(\bar v)$ |  $G_{CS}(Q)$|
| - | :-: | :-: | :-: | :-: |
| Straight pipe | $h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$ |$\bar\varepsilon = \frac{\rm{f}}{2} \frac{\bar v^3}{D}$ |$G_{CS} = \left(\frac{\rm{f}}{2\nu} \frac{\bar v^3}{D} \right)^\frac{1}{2}$ |  $G_{CS} = \left(\frac{\rm{32f}}{ \pi^3\nu} \frac{Q^3}{D^7} \right)^\frac{1}{2}$ |
| Straight pipe laminar|$h_{\rm{f}} = \frac{32\nu L\bar v}{ g D^2}$| $\bar\varepsilon =32\nu \left( \frac{\bar v}{D} \right)^2$ |$G_{CS} =4\sqrt2 \frac{\bar v}{D}$ | $G_{CS} =\frac{16\sqrt2}{\pi} \frac{Q}{D^3}$ |
| Coiled Tube | - |- | $G_{CS_{coil}} = G_{CS}\left[ 1 + 0.033\left(log_{10}De\right)^4  \right]^\frac{1}{2}$ | - |
| Expansions | $h_e =  \mathbf{K_e}\frac{\bar v_{out}^2}{2g}$ | $\bar\varepsilon = \mathbf{K_e}\frac{\bar v_{out}^3}{2H}$ | $G_{CS} = \bar v_{out}\sqrt{\frac{\mathbf{K_e}\bar v_{out}}{2H\nu}}$ | - |

The equations used to convert between columns in the table above are

$ \bar\varepsilon = \frac{gh_{\rm{L}}}{\theta} $, $ G_{CS} = \sqrt{\frac{\bar \varepsilon}{\nu}}$, $\bar v=\frac{4Q}{\pi D}$

=======
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
# Energy dissipation rate, velocity gradients, and mixing
##Introduction

Mixing, collisions between particles, shear that prevents floc deposition on reactor walls, floc breakup in high shear zones. Each of these processes requires an understanding of fluid dynamics and specifically the relationships between turbulence, fluid deformation, and shear.

Estimation of velocity gradients for various flow geometries is the basis for the design of rapid mix, flocculators, and plate settlers and thus our goal is to define the velocity gradients consistently across the range of possible flow regimes. There are three approaches to calculating the average velocity gradient within a control volume.
* Use the Navier Stokes equations and solve for the spatially averaged velocity gradient.
* Use computation fluid dynamics to solve for the spatially averaged velocity gradient.
* Use the total mechanical energy loss in the control volume to calculate the average energy dissipation rate. Calculate the velocity gradient directly from the energy dissipation rate. $\bar G = \sqrt{\frac{\bar \varepsilon}{\nu}}$

The first approach would be ideal but is difficult in practice because Navier Stokes solutions are only available for limited geometries and laminar flow. Computational Fluid Dynamics could be used but is difficult to use as a general engineering design approach given the large number of geometries that are used in drinking water treatment plants. For these reasons we will use the control volume approach to estimate the average velocity gradient. This method incorrectly assumes that the energy dissipation rate is completely uniform in the control volume and hence the velocity gradient was also uniform. This method results in an over estimation of the velocity gradient.    


* Average (control volume) estimates
  * Straight pipe (major losses)
  * Curved tube (laminar flow)
  * Series of expansions
* Maximum velocity gradients
  * Straight pipe walls (major losses)
  * Curved tube (laminar flow)
  * Expansions
    * Between flat plates
    * Round jet
    * Plane jet
    * Behind a flat plate

#### Output
* table of equations for velocity gradients
* table of equations for average energy dissipation rates

Table of equations for control volume averaged values.
| Geometry | $h_L$ |$\bar\varepsilon$ | $\bar G(\bar v)$ |  $\bar G(Q)$|
| - | :-: | :-: | :-: | :-: |
| Straight pipe (laminar and turbulent) | $h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$ |$\bar\varepsilon = \frac{\rm{f}}{2} \frac{\bar v^3}{D}$ |$\bar G = \left(\frac{\rm{f}}{2\nu} \frac{\bar v^3}{D} \right)^\frac{1}{2}$ |  $\bar G = \left(\frac{\rm{32f}}{ \pi^3\nu} \frac{Q^3}{D^7} \right)^\frac{1}{2}$ |
| Straight pipe laminar|$h_{\rm{f}} = \frac{32\nu L\bar v}{ g D^2}$| $\bar\varepsilon =32\nu \left( \frac{\bar v}{D} \right)^2$ |$\bar G =4\sqrt2 \frac{\bar v}{D}$ | $\bar G =\frac{16\sqrt2}{\pi} \frac{Q}{D^3}$ |
| Coiled Tube | - |- | $\overline{G_{coil}} = \bar G\left[ 1 + 0.033\left(log_{10}De\right)^4  \right]^\frac{1}{2}$ | - |
| Expansions | $h_e =  \mathbf{K_e}\frac{\bar v_{out}^2}{2g}$ | $\bar\varepsilon = \mathbf{K_e}\frac{\bar v_{out}^3}{2H}$ | $\bar G = \bar v_{out}\sqrt{\frac{\mathbf{K_e}\bar v_{out}}{2H\nu}}$ | - |
The equations used to convert between columns in the table above are
$\bar\varepsilon = \frac{gh_{\rm{L}}}{\theta}$, $\bar G = \sqrt{\frac{\bar \varepsilon}{\nu}}$, $\bar v=\frac{4Q}{\pi D}$
>>>>>>> master


Table of equations for maximum values.
| Geometry |  $G_{max}$|
| - | :-: |
| Straight pipe  | $G_{wall} =\rm{f}  \frac{\bar v^2}{8\nu}$|
| Straight pipe laminar | $G_{wall} =  \frac{8\bar v}{D}$|
| Coiled pipe | $G_{CS_{wall_{coil}}} =\rm{f} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]  \frac{\bar v^2}{8\nu}$|

## Equation development
### Straight pipe (wall shear)
The average energy dissipation rate, $ \bar\varepsilon$, in a control volume with residence time $\theta$ is
$$ \bar\varepsilon = \frac{gh_{\rm{L}}}{\theta} $$

$$ \theta = \frac{L}{\bar v}  $$

For straight pipe flow the only head loss is due to wall shear and thus we have the Darcy Weisbach equation.

$$h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$$

Combining the 3 previous equations we obtain the energy dissipation rate for pipe flow
$$ \bar\varepsilon = \frac{\rm{f}}{2} \frac{\bar v^3}{D} $$

The average velocity gradient was defined by Camp as

$$ G_{CS} = \sqrt{\frac{\bar \varepsilon}{\nu}}$$

where this approximation neglects the fact that square root of an average is not the same as the average of the square root.  

$$  G_{CS} = \left(\frac{\rm{f}}{2\nu} \frac{\bar v^3}{D} \right)^\frac{1}{2}$$


$$  G_{CS} = \left(\frac{\rm{32f}}{ \pi^3\nu} \frac{Q^3}{D^7} \right)^\frac{1}{2}$$


$$\rm{f} = \frac{64}{Re}$$

Reynolds number is defined as
$$Re= \frac{\bar vD}{\nu}$$

The Darcy Weisbach head loss equation simplifies to

$$h_{\rm{f}} = \frac{32\nu L\bar v}{gD^2}$$

and thus the energy dissipation rate in a straight pipe under conditions of laminar flow is

$$ \bar\varepsilon =32\nu \left( \frac{\bar v}{D} \right)^2$$

The average velocity gradient in a long straight laminar flow tube is thus
$$ G_{CS}^2 =32 \left( \frac{\bar v}{D} \right)^2$$
$$ G_{CS} =4\sqrt2 \frac{\bar v}{D} $$

<<<<<<< HEAD
Our estimate of $ G_{CS} $ based on $\bar \varepsilon$ is an overestimate because it assumes that the energy dissipation is completely uniform through the control volume. The true spatial average velocity gradient for laminar flow in a pipe is

[$$ \bar G = \frac{8}{3}\frac{\bar v}{D} $$](https://doi.org/10.1016/0009-2509(81)80126-1)

The our estimate of $ G_{CS} $ for the case of laminar flow in a pipe is too high by a factor of $\frac{3}{\sqrt2}$.
=======
Our estimate of $\bar G$ based on $\bar \varepsilon$ is an overestimate because it assumes that the energy dissipation is completely uniform through the control volume. The true spatial average velocity gradient for laminar flow in a pipe is

[$\overline {G_{spatial}} = \frac{8}{3}\frac{\bar v}{D}$](https://doi.org/10.1016/0009-2509(81)80126-1)

The our estimate of $\bar G$ for the case of laminar flow in a pipe is too high by a factor of $\frac{3}{\sqrt2}$.
>>>>>>> master

```python
3/np.sqrt(2)
```
As a function of flow rate we have
$$ \bar v=\frac{Q}{A} = \frac{4Q}{\pi D^2}$$

$$ G_{CS} =\frac{16\sqrt2}{\pi} \frac{Q}{D^3} $$

## Coiled tubes

The ratio of the coiled to straight friction factors is given by [Mishra and Gupta](https://doi.org/10.1021/i260069a017)


$$De = Re\left(\frac{D}{D_c}\right)^\frac{1}{2}  $$

where $D$ is the inner diameter of the tube and $D_c$ is the diameter of the coil. Note that the tubing coils are actually helixes and that for the tubing diameters and coil diameters used for flocculators that the helix doesn't significantly change the radius of curvature.

$$\frac{\rm{f}_{coil}}{\rm{f}} = 1 + 0.033\left(log_{10}De\right)^4  $$

$$h_{\rm{f}_{coil}} = h_{\rm{f}} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right] $$

The average velocity gradient is proportional to the square root of the head loss and thus we obtain

$$G_{CS_{coil}} = G_{CS}\left[ 1 + 0.033\left(log_{10}De\right)^4  \right]^\frac{1}{2}$$

## Expansions

The average energy dissipation rate for a flow expansion really only has meaning if there is a defined control volume where the mechanical energy is lost. Hydraulic flocculators provide such a case because the same flow expansion is repeated and thus the mechanical energy loss can be assumed to happen in the volume associated with one flow expansion. I this case we have

$$ h_e =  \mathbf{K_e}\frac{\bar v_{out}^2}{2g} $$
In this equation $\mathbf{K_e}$ represents the fraction of the kinetic energy that is dissipated.

If we define the length of the control volume as $H$ then the residence time is
$$\theta = \frac{H}{\bar v}$$

$$ \bar\varepsilon = \frac{gh_{\rm{e}}}{\theta} $$
Combining the previous equations we obtain

$$ \bar\varepsilon = \mathbf{K_e}\frac{\bar v_{out}^3}{2H} $$


$$ G_{CS} = \sqrt{\frac{\bar \varepsilon}{\nu}}$$

$$ G_{CS} = \bar v_{out}\sqrt{\frac{\mathbf{K_e}\bar v_{out}}{2H\nu}}$$

# Maximum velocity gradients
## Straight pipe walls (major losses)
The maximum velocity gradient in

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/pipe_pressure_shear_force_balance.png" width="400">

Figure x. A fluid flowing from left to right due to a pressure gradient results in wall shear.

A force balance for the case of steady flow in a round pipe requires that sum of the forces in the x direction must equal zero. Given a pipe with diameter, D, and length, L, we obtain

$$ \left(P_{in}- P_{out}\right)\frac{\pi D^2}{4} = \tau_{wall} \pi D L $$

$$ -\Delta P\frac{D}{4} = \tau_{wall} L $$
For this control volume the energy equation simplifies to

$$-\Delta P=\rho g h_{\rm{f}}$$

The relationship between shear and velocity gradient is

$$\tau_{wall} = \mu \frac{du}{dy}_{wall} = \mu G_{wall} $$

Combining the energy equation, the force balance, and the relationship between shear and velocity gradient we obtain
$$ \rho g h_{\rm{f}}\frac{D}{4} = \mu G_{wall} L $$

$$ G_{wall} = \frac{g h_{\rm{f}}D}{4\nu L} $$
This equation is valid for both laminar flow. For  turbulent flow it is necessary to make the approximation that wall shear perpendicular to the direction of flow is insignificant in increasing the magnitude of the wall shear.

$$ G_{wall} =\rm{f}  \frac{\bar v^2}{8\nu} $$

For laminar flow we have

$$ G_{wall} =  \frac{8\bar v}{D} $$
This equation is useful for finding the velocity gradient at the wall of a tube settler.

## Curved tube (laminar flow)
The shear on the wall of a coiled tube is not uniform. The outside of the curve has a higher velocity gradient than the inside of the curve and there are secondary currents that results in wall shear that is not purely in the locally defined upstream direction. We do not have a precise equation for the wall shear. The best we can do currently is define an average wall shear in the locally defined direction of flow by combining $ G_{CS_{wall_{coil}}} =\rm{f_{coil}}  \frac{\bar v^2}{8\nu} $ and $\rm{f}_{coil} = \rm{f} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right] $ to obtain

$$ G_{CS}_{wall_{coil}} =\rm{f} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]  \frac{\bar v^2}{8\nu} $$
## Expansions
### Round jet



Chemical Engineering Science, Vol. 50, No. 12, pp. 1877-1880, 1995
THE INFLUENCE OF VISCOSITY ON MIXING IN JET REACTORS
Jo BALDYGA, J. R. BOURNE* and R. V. GHOLAP
Technisch-Chemisches Laboratorium, ETH-Zentrum, CH-8092 Zurich, Switzerland

[$$ \varepsilon_{Centerline} \cong \frac{50 D_{Jet}^3 \bar v_{Jet}^3}{ \left( x - 2 D_{Jet} \right)^4}$$](https://doi.org/10.1016/0009-2509(95)00049-B)

$$ \varepsilon_{Max} \cong \frac{\left( \frac{50}{\left( 5 \right)^4} \right) \bar v_{Jet}^3}{D_{Jet}}$$

$$ \varepsilon_{Max} \cong \frac{\left( \Pi_{RoundJet} \bar v_{Jet} \right)^3}{D_{Jet}}$$

$$\Pi_{RoundJet} \cong 0.5$$
(The equation for $ \varepsilon_{Max}$ would be more similar to the equation for energy dissipation in a pipe if we defined $\Pi_{RoundJet}$ to be outside the exponent of 3. In that case it would simply be $\frac{50}{5^4}$ = 0.08. Would this require any significant changes in subsequent equations?)

```python
""" importing """
from aide_design.play import*
from aguaclara_research.play import*
import aguaclara_research.floc_model as fm
import matplotlib.pyplot as plt
from matplotlib.ticker import FormatStrFormatter
imagepath = 'AguaClara Water Treatment Plant Design/Chapter 3_Rapid Mix/Images/'
Temperature = 15*u.degC

def Energy_dissipation_jet_centerline(D_jet,v_jet,x):
  return (50 * D_jet**3*v_jet**3/(x-2*D_jet)**4).to_base_units()

def Energy_dissipation_jet_max(D_jet,v_jet):
  return (con.RATIO_JET_ROUND * v_jet)**3/D_jet

v_jet = 1 * u.m/u.s
D_jet = 0.1 * u.m
EDR_max = Energy_dissipation_jet_max(D_jet,v_jet)
x=np.linspace(7,20,24)*D_jet
fig, ax = plt.subplots()
ax.plot(x/D_jet,Energy_dissipation_jet_centerline(D_jet,v_jet,x))
ax.set(xlabel='Jet diameters downstream', ylabel='Energy dissipation rate (W/kg)')
fig.savefig(imagepath+'Jet_centerline_EDR')
plt.show()
```

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/Jet_centerline_EDR.png" width="400">

### Plane jet
### Behind a flat plate
