# Average Energy Dissipation Rate and Camp-Stein Velocity Gradient Derivations
## Straight pipe (wall shear)
The average energy dissipation rate, $\bar\varepsilon$, in a control volume with residence time $\theta$ is
$$ \bar\varepsilon = \frac{gh_{\rm{L}}}{\theta} $$

The residence time can be expressed as a function of length and average velocity.
$$ \theta = \frac{L}{\bar v}  $$

For straight pipe flow the only head loss is due to wall shear and thus we have the Darcy Weisbach equation.

$$h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$$

Combining the 3 previous equations we obtain the energy dissipation rate for pipe flow
$$\color{purple}{
  \bar\varepsilon = \frac{\rm{f}}{2} \frac{\bar v^3}{D}
}$$

The average velocity gradient was defined by Camp and Stein as

$$ G_{CS} = \sqrt{\frac{\bar \varepsilon}{\nu}}$$

where this approximation neglects the fact that square root of an average is not the same as the average of the square roots.  

$$\color{purple}{
  G_{CS} = \left(\frac{\rm{f}}{2\nu} \frac{\bar v^3}{D} \right)^\frac{1}{2}
}$$

or in terms of flow rate, we have:

$$  G_{CS} = \left(\frac{\rm{32f}}{ \pi^3\nu} \frac{Q^3}{D^7} \right)^\frac{1}{2}$$

## Straight Pipe Laminar
Laboratory scale apparatus is often limited to laminar flow where viscosity effects dominate. The equations describing laminar flow conditions always include viscosity. For the case of laminar flow in a straight pipe, we have:

$$\rm{f} = \frac{64}{Re}$$

Reynolds number is defined as
$$Re= \frac{\bar vD}{\nu}$$

The Darcy Weisbach head loss equation simplifies to the Hagen–Poiseuille equation for the case of laminar flow.

$$h_{\rm{f}} = \frac{32\nu L\bar v}{gD^2}$$

and thus the energy dissipation rate in a straight pipe under conditions of laminar flow is

$$\color{purple}{
  \bar\varepsilon =32\nu \left( \frac{\bar v}{D} \right)^2
}$$

The Camp-Stein velocity gradient in a long straight laminar flow tube is thus

$$ G_{CS}^2 =32 \left( \frac{\bar v}{D} \right)^2$$

$$\color{purple}{
  G_{CS} =4\sqrt2 \frac{\bar v}{D}
}$$


Our estimate of $G_{CS}$ based on $\bar \varepsilon$ is an overestimate because it assumes that the energy dissipation is completely uniform through the control volume. The true spatial average velocity gradient, $\bar G$, for laminar flow in a pipe is

[$$\bar G = \frac{8}{3}\frac{\bar v}{D}$$](https://doi.org/10.1016/0009-2509(81)80126-1)

The our estimate of $G_{CS}$ for the case of laminar flow in a pipe is too high by a factor of $\frac{3}{\sqrt2}$.

As a function of flow rate we have
$$ \bar v=\frac{Q}{A} = \frac{4Q}{\pi D^2}$$

$$ G_{CS} =\frac{16\sqrt2}{\pi} \frac{Q}{D^3} $$

## Parallel plates Laminar

Flow between parallel plates occurs in plate settlers in the sedimentation tank. We will derive the velocity gradient at the wall using the Navier Stokes equation.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/Parallel_Plate_schematic.png" width="400">

Figure x. A fluid flowing from left to right due to a pressure gradient results in wall shear on the parallel plates. This flow profile is for the case when $\frac{dp}{dx}$ is negative.

We start with the Navier-Stokes equation written for flow in the x direction.

$$\frac{y^2}{2} \frac{dp}{dx} + Ay + B = \mu u$$
where $u$ is the velocity in the x direction.

Apply the no slip condition at bottom plate.

$$u=0 \quad at \quad y=0$$

Thus the constant $B=0$.

Apply the no slip condition at top plate.
$$u=0 \quad at \quad y=S$$

Thus the constant $A = \frac{- S}{2} \frac{dp}{dx}$

Substitute the values for constants $A$ and $B$ into the original equation.

$$\frac{y^2}{2} \frac{dp}{dx} - \frac{S}{2} \frac{dp}{dx} y = \mu \,u$$

Simply the equation to obtain

$$u = \frac{y \left( y - S \right)}{2 \mu} \frac{dp}{dx}$$

We need a relationship between average velocity and $\frac{dp}{dx}$. We can obtain this by integrating from 0 to $S$.

$${\bar v } = \frac{q}{S}
= \frac{1}{S}\int\limits_0^S u dy
= \frac{1}{S} \int\limits_0^S
\left(
  \frac{y^2 - S y}{2 \mu} \left( \frac{dp}{dx} \right)
\right) dy$$

$$\bar v = - \frac{S^2}{12 \mu} \frac{dp}{dx}$$

Solving for $\frac{dp}{dx}$

$$\frac{dp}{dx} = - \frac{12 \mu \bar v}{S^2}$$

From the Navier Stokes equation after integrating once we get

$$\mu \,\left( \frac{du}{dy} \right) = y \frac{dp}{dx} + A$$

Substituting our boundary condition, $A = \frac{- S}{2} \frac{dp}{dx}$ we obtain

$$\frac{du}{dy}_{y = 0} = - \frac{S}{2 \mu} \frac{dp}{dx}$$

Substituting the result for $\frac{dp}{dx}$ we obtain

$$\frac{du}{dy}_{y = 0} = \frac{6 \bar v}{S}$$

Therefore in velocity gradient notation we have

$$G_{wall} = \frac{6 \bar v}{S}$$

The energy dissipation rate at the wall

$$\varepsilon_{wall} = G_{wall}^2 \nu$$

$$\varepsilon_{wall} = \left( \frac{6 \bar v}{S}\right)^2 \nu$$

Head loss due to shear on the plates is obtained from a force balance on a control volume between two parallel plates.
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/pipe_pressure_shear_force_balance.png" width="400">

Figure x. A fluid flowing between parallel plates from left to right due to a pressure gradient results in wall shear.

A force balance gives

$$2 \tau L W = -\Delta P W S$$

$$\Delta P = -\frac{2 \tau L}{S}$$

The equation relating shear and velocity gradient is

$$\tau = \nu \rho \frac{du}{dy} = \nu \rho G$$

The velocity gradient at the wall is

$$G_{wall} = \frac{6 \bar v}{S}$$

$$\tau  = \nu \rho \frac{6 \bar v}{S}$$

Substituting into the force balance equation

$$\Delta P = -\frac{2 \nu \rho 6 \bar v L}{S^2}$$

The head loss for horizontal flow at uniform velocity simplifies too

$$h_{\rm{f}} = \frac{-\Delta P}{\rho g}$$

$$h_{\rm{f}} = 12\frac{ \nu \bar v L}{gS^2}$$

The average energy dissipation rate is

$$ \bar\varepsilon = \frac{gh_{\rm{L}}}{\theta} $$

$$ \bar\varepsilon = 12 \nu \left(\frac{  \bar v}{S} \right)^2  $$

The Camp-Stein velocity gradient for laminar flow between parallel plates is
$$G_{CS} = 2\sqrt{3}\frac{  \bar v}{S}$$

## Coiled tubes (laminar flow)
Coiled tubes are used as flocculators at laboratory scale. The one shown below is a doubled coil. A single coil would only go around one cylinder

[<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/Tube_flocculator_AC.JPG" width="500">](https://confluence.cornell.edu/display/AGUACLARA/Laminar+Tube+Floc?preview=/10422268/258146480/ReportLaminarTubeFlocSpring2014.pdf)

Figure x. The double coiled flocculator creates secondary currents that oscillate in direction. This may be helpful in creating much more mixing than would occur in a straight laminar flow pipe.

The ratio of the coiled to straight friction factors is given by [Mishra and Gupta](https://doi.org/10.1021/i260069a017)

The Dean number is defined as:

$$De = Re\left(\frac{D}{D_c}\right)^\frac{1}{2}  $$

where $D$ is the inner diameter of the tube and $D_c$ is the diameter of the coil. Note that the tubing coils are actually helixes and that for the tubing diameters and coil diameters used for flocculators that the helix doesn't significantly change the radius of curvature.

$$\frac{\rm{f}_{coil}}{\rm{f}} = 1 + 0.033\left(log_{10}De\right)^4  $$

$$h_{L_{coil}} = h_{\rm{f}} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right] $$

where $h_{\rm{f}} = \frac{32\nu L\bar v}{ g D^2}$. Note that we switch from major losses to total head loss here because the head loss from flowing around the coil is no longer simply due to shear on the wall.

$$h_{L_{coil}} = \frac{32\nu L\bar v}{ g D^2} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right] $$

The average energy dissipation rate is

$$\bar\varepsilon = 32\nu \left( \frac{\bar v}{D} \right)^2 \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]$$

The average velocity gradient is proportional to the square root of the head loss and thus we obtain

$$
  G_{CS_{coil}} = G_{CS}\left[ 1 + 0.033\left(log_{10}De\right)^4  \right]^\frac{1}{2}
$$

where $G_{CS} =4\sqrt2 \frac{\bar v}{D}$ for laminar flow in a straight pipe.

$$\color{purple}{
  G_{CS_{coil}} = 4\sqrt2 \frac{\bar v}{D}\left[ 1 + 0.033\left(log_{10}De\right)^4  \right]^\frac{1}{2}
}$$

## Expansions

The average energy dissipation rate for a flow expansion really only has meaning if there is a defined control volume where the mechanical energy is lost. Hydraulic flocculators provide such a case because the same flow expansion is repeated and thus the mechanical energy loss can be assumed to happen in the volume associated with one flow expansion. I this case we have

$$\color{purple}{
  h_e =  \mathbf{K_e}\frac{\bar v_{out}^2}{2g}
}$$

In this equation $\mathbf{K_e}$ represents the fraction of the kinetic energy that is dissipated.

If we define the length of the control volume (in the direction of flow) as $H$ then the residence time is
$$\theta = \frac{H}{\bar v}$$

$$ \bar\varepsilon = \frac{gh_{\rm{e}}}{\theta} $$
Combining the previous equations we obtain

$$\color{purple}{
  \bar\varepsilon = \mathbf{K_e}\frac{\bar v_{out}^3}{2H}
}$$


$$G_{CS} = \sqrt{\frac{\bar \varepsilon}{\nu}}$$

$$\color{purple}{
  G_{CS} = \bar v_{out}\sqrt{\frac{\mathbf{K_e}\bar v_{out}}{2H\nu}}
}$$

## Maximum velocity gradients
### Straight pipe (major losses)
The maximum velocity gradient in pipe flow occurs at the wall. This is true for both laminar and turbulent flow. In either case a force balance on a control volume of pipe gives us the wall shear and the wall shear can then be used to estimate the velocity gradient at the wall.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/pipe_pressure_shear_force_balance.png" width="400">

Figure x. A fluid flowing from left to right due to a pressure gradient results in wall shear.

A force balance for the case of steady flow in a round pipe requires that sum of the forces in the x direction must equal zero. Given a pipe with diameter, D, and length, L, we obtain

$$ \left(P_{in}- P_{out}\right)\frac{\pi D^2}{4} = \tau_{wall} \pi D L $$

$$ -\Delta P\frac{D}{4} = \tau_{wall} L $$
For this control volume the energy equation simplifies to

$$-\Delta P=\rho g h_{\rm{f}}$$

The relationship between shear and velocity gradient is

$$\tau_{wall} = \mu \frac{du}{dy}_{wall} = \nu \rho G_{wall} $$

Combining the energy equation, the force balance, and the relationship between shear and velocity gradient we obtain

$$ \rho g h_{\rm{f}}\frac{D}{4} = \nu \rho G_{wall} L $$

$$ G_{wall} = \frac{g h_{\rm{f}}D}{4\nu L} $$

This equation is valid for both laminar flow. For  turbulent flow it is necessary to make the approximation that wall shear perpendicular to the direction of flow is insignificant in increasing the magnitude of the wall shear. We can substitute the Darcy Weisbach equation for head loss to obtain

$$\color{purple}{
  G_{wall} =\rm{f}  \frac{\bar v^2}{8\nu}
}$$

The energy dissipation rate at the wall is
$$\varepsilon_{wall} = G_{wall}^2 \nu$$
$$\varepsilon_{wall} = \frac{1}{\nu}\left(\rm{f}  \frac{\bar v^2}{8} \right)^2 $$

For laminar flow we can substitute $ f = \frac{64}{Re} $ and the definition of the Reynolds number to obtain

$$\color{purple}{
  G_{wall} =  \frac{8\bar v}{D}
}$$
This equation is useful for finding the velocity gradient at the wall of a tube settler.

The energy dissipation rate at the wall is
$$\varepsilon_{wall} = G_{wall}^2 \nu$$
$$\varepsilon_{wall} = \left(\frac{8\bar v}{D} \right)^2 \nu$$


## Coiled tubes (laminar flow)
The shear on the wall of a coiled tube is not uniform. The outside of the curve has a higher velocity gradient than the inside of the curve and there are secondary currents that results in wall shear that is not purely in the locally defined upstream direction. We do not have a precise equation for the wall shear. The best we can do currently is define an average wall shear in the locally defined direction of flow by combining $G_{{CS}_{wall_{coil}}} =\rm{f_{coil}}  \frac{\bar v^2}{8\nu}$ and $\rm{f}_{coil} = \rm{f} \left[ 1 + 0.033\left(log_{10}De\right)^4 \right]$ to obtain

$$\color{purple}{
  G_{{CS}_{wall_{coil}}} =\rm{f} \left[ 1 + 0.033 \left(log_{10}De \right)^4 \right]  \frac{\bar v^2}{8\nu}
}$$

## Expansions
Flow expansions are used intentionally or unavoidable in multiple locations in hydraulically optimized water treatment plants. Rapid mix and hydraulic flocculation use flow expansions to generate fluid mixing and collisions between particles.

### Round jet

Chemical Engineering Science, Vol. 50, No. 12, pp. 1877-1880, 1995
THE INFLUENCE OF VISCOSITY ON MIXING IN JET REACTORS
Jo BALDYGA, J. R. BOURNE* and R. V. GHOLAP
Technisch-Chemisches Laboratorium, ETH-Zentrum, CH-8092 Zurich, Switzerland

[$$\varepsilon_{Centerline} = \frac{50 D_{Jet}^3 \bar v_{Jet}^3}{ \left( x - 2 D_{Jet} \right)^4}$$](https://doi.org/10.1016/0009-2509(95)00049-B)

$$ \varepsilon_{Max} = \frac{\left( \frac{50}{\left( 5 \right)^4} \right) \bar v_{Jet}^3}{D_{Jet}}$$

$$ \varepsilon_{Max} = \frac{\Pi_{RoundJet} \bar v_{Jet} ^3}{D_{Jet}}$$

$$\Pi_{RoundJet} = 0.08$$

The maximum velocity gradient in a jet is thus

$$ G_{Max} = \bar v_{Jet} \sqrt{\frac{\Pi_{RoundJet} \bar v_{Jet} }{\nu D_{Jet}}}$$

Below we plot the Baldyga et al. equation for the energy dissipation rate as a function of distance from the discharge location for the case of a round jet that is discharging into a large tank.

```python
""" importing """
from aide_design.play import*
from aguaclara_research.play import*
import aguaclara_research.floc_model as fm
import matplotlib.pyplot as plt
from matplotlib.ticker import FormatStrFormatter
imagepath = 'AguaClara Water Treatment Plant Design/Energy Dissipation and Velocity Gradients/Images/'
Temperature = 15*u.degC
RATIO_JET_ROUND = 0.08
def Energy_dissipation_jet_centerline(D_jet,v_jet,x):
  return (50 * D_jet**3*v_jet**3/(x-2*D_jet)**4).to_base_units()

def Energy_dissipation_jet_max(D_jet,v_jet):
  return RATIO_JET_ROUND*v_jet**3/D_jet

v_jet = 1 * u.m/u.s
D_jet = 0.1 * u.m
EDR_max = Energy_dissipation_jet_max(D_jet,v_jet)
x=np.linspace(7,20,24)*D_jet
fig, ax = plt.subplots()
ax.plot(x/D_jet,Energy_dissipation_jet_centerline(D_jet,v_jet,x))
ax.plot(7,Energy_dissipation_jet_max(D_jet,v_jet),'o')
ax.set(xlabel='Jet diameters downstream', ylabel='Energy dissipation rate (W/kg)')
ax.legend(['centerline energy dissipation rate','Maximum energy dissipation rate'])
fig.savefig(imagepath+'Jet_centerline_EDR')
plt.show()
```

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/Jet_centerline_EDR.png" width="400">

Figure x. The centerline energy dissipation rate downstream from a round jet. The distance downstream is measured in units of jet diameters. The energy dissipation rate between the jet and 7 jet diameters is developing as the shear between the stationary fluid and the jet propagates toward the center of the jet and turbulence is generated.

### Plane jet
Plane jets occur in hydraulic flocculators and in the sedimentation tank inlet jet system. We haven't been able to find a literature estimate of the maximum energy dissipation rate in a plane jet. Original measurements of a plane turbulent jet have been made by [Heskestad in 1965](http://dx.doi.org/10.1115/1.3627309) and it may be possible to use that data to get a better estimate of $\Pi_{JetPlane} $ from that source.

$$\Pi_{\bar \epsilon}^{\epsilon_{Max}} = \frac{\varepsilon_{Max}}{\bar \varepsilon}$$

$$\varepsilon_{Max} = \Pi_{JetPlane}  \frac{  \bar v_{Jet} ^3}{S_{Jet}}$$

The maximum velocity gradient is thus

$$G_{Max} = \bar v_{Jet}\sqrt{\frac{\Pi_{JetPlane} \bar v_{Jet}}{\nu S_{Jet}}}$$


$$\bar v = \frac{Q}{SW}$$

$$\bar v_{Jet} = \frac{\bar v}{\Pi_{VCBaffle}}$$

$$S_{Jet} = S \Pi_{VCBaffle}$$

The average hydraulic residence time for the fluid between two baffles is

$$\theta_B = \frac{H}{\bar v}$$

where $H$ is the depth of water. Substituting into the equation for $\varepsilon_{Max}$ to get the equation in terms of the average velocity $\bar v$ and flow dimension $S$

$$\varepsilon_{Max}= \frac{\Pi_{JetPlane}}{S \Pi_{VCBaffle}} \left( \frac{ \bar v}{\Pi_{VCBaffle}} \right)^3$$

From the control volume analysis the average energy dissipation rate is

$$\bar \varepsilon = K_e \frac{\bar v^2}{2} \frac{1}{\theta_B} = \frac{K_e}{2} \frac{\bar v^3}{H_e}$$

where $K_e$ is the minor loss coefficient for flow around the end of a baffle with a $180^\circ$ turn.

Substitute the values for $\bar \varepsilon$ and $\varepsilon_{Max}$ to obtain the ratio, $\Pi_{\bar \epsilon}^{\epsilon_{Max}}$

$$\Pi_{\bar \epsilon}^{\epsilon_{Max}} = \frac{\Pi_{JetPlane}}{\Pi_{VCBaffle}^4} \frac{2 H_e}{K_e S}$$

$\Pi_{\bar \varepsilon}^{\varepsilon_{Max}}$ has a value of 2 for $H_e/S<5$ (CFD analysis and [Haarhoff, 2001](https://search-proquest-com.proxy.library.cornell.edu/docview/1943098053?accountid=10267)) The transition value for $H_e/S$ is at 5 (from CFD analysis, our weakest assumption).


We also have that  $\Pi_{\bar \varepsilon}^{\varepsilon_{Max}}$ has a value of $\frac{\Pi_{JetPlane}}{\Pi_{VCBaffle}^4} \frac{2 H_e}{K_e S}$ for $H_e/S>5$. Thus we can solve for $\Pi_{JetPlane}$ at $H_e/S=5$

$$\Pi_{JetPlane} = \left(
  \Pi_{\bar \epsilon}^{\epsilon_{Max}} \Pi_{VCBaffle}^4 \frac{K_e}{2} \frac{S}{H_e}
  \right)$$

$$\Pi_{JetPlane} = 0.0124$$





```python
x=con.RATIO_VC_ORIFICE**2
Ratio_Jet_Plane = 2*con.RATIO_VC_ORIFICE**8 * con.K_MINOR_FLOC_BAFFLE/2/5
Ratio_Jet_Plane

con.RATIO_VC_ORIFICE**8*con.K_MINOR_FLOC_BAFFLE/Ratio_Jet_Plane
```
### Behind a flat plate
A flat plate normal to the direction of flow could be used in a hydraulic flocculator. In vertical flow flocculators it would create a space where flocs can settle and thus it is not a recommended design.

The impellers used in mechanical flocculators could be modeled as a rotating flat plate. The energy dissipation rate in the wake behind the flat plate is often quite high in mechanical flocculators and this may be responsible for breaking previously formed flocs.

Ariane Walker-Horn modeled the flat plate using Fluent in 2015.
<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Energy%20Dissipation%20and%20Velocity%20Gradients/Images/CFD_Flat_Plate.png" width="600">

Figure x. The energy dissipation rate and streamlines for a 1 m wide plate in two dimensional flow with an approach velocity of $1 m/s$. The maximum energy dissipation rate was approximately $0.04 W/kg$.


$$\varepsilon _{Max} = \Pi_{Plate}\frac{\bar v^3}{W_{Plate}}$$

The maximum velocity gradient is thus

$$G_{Max} = \bar v\sqrt{\frac{\Pi_{Plate} \bar v}{\nu W_{Plate}}}$$

$$\Pi_{Plate} = \frac{ \left( \varepsilon_{Max} W_{Plate} \right)}{\bar v^3}$$

```python
"""CFD analysis setup used by Ariane Walker-Horn in 2015"""
EDR_Max = 0.04*u.W/u.kg
v = 1*u.m/u.s
W = 1*u.m
Ratio_Jet_Plate = (EDR_Max * W/v**3).to_base_units()
print(Ratio_Jet_Plate)
```
