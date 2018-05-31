# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


# **Sedimentation**
### Sedimentation: Particle Terminal Fall Velocity
$$\sum F  = m a$$

$$F_d + F_b - W = 0$$

$$W = $$

$$\rlap{-} V_{Floc} \rho_{Floc} g$$

$$F_b = $$

$$\rlap{-} V_{Floc} \rho_{H_2O} g$$

$$F_d = C_D A_{Floc} \rho_{H_2O} \frac{V_t^2}{2}$$

$$\begin{array}{l}
\rlap{-} V_{Floc} = \rm{particle \, \, volume}
\\
A_{Floc} = \rm{particle \, \, cross \, \, sectional \, \, area}
\\
\rho_{Floc} = \rm{particle \, \, density}
\\
\rho_{H_2O} = \rm{water \, \, density}
\\
g = \rm{acceleration \, \, due \, \, to \, \, gravity}
\\
C_D = \rm{drag \, \, coefficient}
\\
V_t = \rm{particle \, \, terminal \, \, velocity}
\end{array}$$

$$V_t = \sqrt{ \frac{4}{3} \frac{g d}{C_D} \frac{\left( \rho_{Floc} - \rho_{H_2O} \right)}{\rho_{H_2O}} }$$


### Drag Coefficient on a Sphere
$$V_t = \frac{d^2 g}{18\nu} \frac{\rho_{Floc} - \rho_{H_2O}}{\rho_{H_2O}}$$

$$V_t = \sqrt{ \frac{4}{3} \frac{g d}{C_D} \frac{\left( \rho_{Floc} - \rho_{H_2O} \right)}{\rho_{H_2O}} }$$

$$C_d = \frac{24}{\rm Re}$$

$${\rm Re} = \frac{V_t d}{\nu}$$


### Floc Terminal Velocity
$$V_t = \frac{g d_0^2}{18 \Phi \nu_{H_2O}} \frac{\rho_{Floc_0} - \rho_{H_2O}} {\rho_{H_2O}} \left( \frac{d}{d_0} \right)^{D_{Fractal} - 1}$$


### Horizontal Flow Sedimentation Tank
$$\theta  = \frac{\rlap{-} V}{Q}$$

$$V_c = \frac{H}{\theta}$$

$$ = \frac{H Q}{\rlap{-} V}$$

$$ = \frac{Q}{L W}$$

$$ = \frac{Q}{A_s}$$



# Plate Settlers
### Settle Capture Velocity for Plate (and Tube) Settlers
$$L \cos \alpha $$

$$\frac{S}{\sin \alpha}$$

$$\cos \alpha  = \frac{S}{h_c}$$

$$h_c = \frac{S}{\cos \alpha}$$

$$h = L \sin \alpha$$

$$V_{net} = V_{Plate \uparrow} - V_c$$


### Compare times
$$\frac{h_c}{V_c} = \frac{h}{V_{Plate \uparrow} - V_c}$$

$$h_c = \frac{S}{\cos \alpha}$$

$$h = L \sin \alpha$$

$$\frac{S}{V_c \cos \alpha} = \frac{L \sin \alpha}{V_{Plate \uparrow} - V_c}$$

$$S V_{Plate \uparrow} - S V_c = L \sin \alpha V_c \cos \alpha$$

$$S V_{Plate \uparrow} = \left( L \sin \alpha \cos \alpha + S \right) V_c$$

$$V_c = \frac{S V_{Plate \uparrow}}{L\sin \alpha \cos \alpha + S}$$

$$\frac{V_{Plate \uparrow}}{V_c} = 1 + \frac{L}{S} \cos \alpha \sin \alpha$$


### Comparison with Q/As
$$Q = V_\alpha S W$$

$$\frac{V_{Plate \uparrow}}{V_\alpha} = \sin \alpha$$

$$Q = \frac{V_{Plate \uparrow S W}}{\sin \alpha}$$

$$A = \left( L\cos \alpha + \frac{S}{\sin \alpha} \right) W$$

$$V_c = \frac{Q}{A} = \frac{V_{Plate \uparrow S W}}{\sin \alpha}\frac{1}{\left( L\cos \alpha + \frac{S}{\sin \alpha} \right)W}$$

$$V_c = \frac{V_{Plate \uparrow} S}{L \cos \alpha \sin \alpha + S}$$


### Equation for capture velocity
$$V_c = \frac{S V_{Plate \uparrow}}{L \sin \alpha \cos \alpha + S}$$

$$V_{Plate \uparrow} = \frac{Q_{Plant}}{N_{Plate} W_{Plate} \frac{S}{\sin \alpha}}$$

$$V_c = \frac{Q_{Plant}}{N_{Plate} W_{Plate} \left(L \cos \alpha + \frac{S}{\sin \alpha} \right)}$$

$$V_c = \frac{V_\alpha}{\left( \frac{L}{S} \cos \alpha + \frac{1}{\sin \alpha} \right)}$$

$$L = \frac{S}{\cos \alpha} \left( \frac{V_\alpha}{V_c} - \frac{1}{\sin \alpha} \right)$$


### Performance ratio (conventional to plate/tube settlers)
$$A_{plate} = W \frac{S}{\sin \alpha} + W L \cos \alpha$$

$$A_{plate} = W \frac{S}{\sin \alpha}$$

$$ = A_{ratio} = 1 + \frac{L}{S} \cos \alpha \sin \alpha = \frac{V_{Plate \uparrow}}{V_c}$$


### Settle Capture Velocity Confusion
$$\frac{V_{Plate \uparrow}}{V_c} = \frac{L}{S} \cos \alpha \sin \alpha + \sin ^2 \alpha$$

$$\frac{V_{Plate \uparrow}}{V_c} = \frac{L}{S} \cos \alpha \sin \alpha + 1$$

**Off-slide**
$$\begin{array}{l}
\frac{V_\alpha \sin \alpha}{V_c} = \frac{L}{S} \cos \alpha \sin \alpha + \sin ^2 \alpha
\\
Q = \frac{\pi D^2}{4} V_c \left( \frac{L}{D} \cos \alpha + \sin \alpha \right)
\end{array}$$

$$\frac{V_\uparrow}{V_\alpha} = \sin \alpha$$


### Thick Plate Settlers
$$V_{Plate \uparrow} \cdot S = V_{Active \uparrow} \cdot B$$

$$B = S + T$$

$$V_{Plate \uparrow} = V_{Active \uparrow} \frac{S + T}{S}$$

$$V_c = \frac{S V_{Plate \uparrow}}{L \sin \alpha \cos \alpha + S}$$

$$V_c = \frac{S}{L \sin \alpha \cos \alpha + S} \left( V_{Active \uparrow} \frac{S + T}{S} \right)$$

$$B = \frac{L \sin \alpha \cos \alpha - T}{\frac{V_{Active \uparrow}}{V_c} - 1}$$

$$L = \frac{B \left( \frac{V_{Active \uparrow}}{V_c} - 1 \right) + T}{\sin \alpha \cos \alpha}$$

$$L = \frac{
  S\left( \frac{V_{Active \uparrow}}{V_c} - 1 \right) + T \frac{V_{Active \uparrow}}{V_c}
  } {\sin \alpha \cos \alpha}$$


### Plate Settler Design (AguaClara approach)
$$\frac{V_{Plate \uparrow}}{V_c} = 1 + \frac{L}{S} \cos \alpha \sin \alpha$$


### Floc Rollup Soultion Scheme: Another failure mode
$$V_\alpha = \frac{V_{Plate \uparrow }}{\sin \alpha}$$


### Infinite Horizontal Plates: Boundary Conditions
$$\frac{y^2}{2} \frac{dp}{dx} + Ay + B = \mu \,u$$

$$B = 0$$

$$\frac{S^2}{2} \frac{dp}{dx} + AS = 0$$

$$\frac{y^2}{2} \frac{dp}{dx} - \frac{S}{2} \frac{dp}{dx} y = \mu \,u$$

$$A = \frac{- S}{2} \frac{dp}{dx}$$

$$\frac{dp}{dx}$$

$$\mu \,\left( \frac{du}{dy} \right) = y \frac{dp}{dx} + A$$

$$\tau  = \left( y - \frac{S}{2} \right) \frac{dp}{dx}$$


### Navier Stokes Flow between Plates
$$u = \frac{y \left( y - S \right)}{2 \mu} \frac{dp}{dx}$$

$${V_\alpha } = \frac{q}{S}
= \frac{1}{S}\int\limits_0^S u dy
= \frac{1}{S} \int\limits_0^S
\left(
  \frac{y^2 - S y}{2 \mu} \left( \frac{dp}{dx} \right)
\right) dy$$

$$V_\alpha = - \frac{S^2}{12 \mu} \frac{dp}{dx}$$

$$\frac{dp}{dx} = - \frac{12 \mu V_\alpha}{S^2}$$

$$\mu \left( \frac{du}{dy} \right) = y \frac{dp}{dx} + A$$

$$\frac{du}{dy}_{y = 0} = - \frac{S}{2 \mu} \frac{dp}{dx}$$

$$\frac{du}{dy}_{y = 0} = \frac{6 V_\alpha}{S}$$

$$A = \frac{- S}{2} \frac{dp}{dx}$$

$$\frac{du}{dy} = \frac{1}{\mu} \left( y - \frac{S}{2} \right) \frac{dp}{dx}$$

**Off-slide**
$$\frac{du}{dy} = \frac{- 12 q}{S^3} \left( y - \frac{S}{2} \right)$$

$$\frac{du}{dy} = \frac{- 12 V_\alpha}{S^2} \left( y - \frac{S}{2} \right)$$

$$\frac{du}{dy}_{y = 0} = \frac{6 V_\alpha}{S}$$


### Laminar Flow through Circular Tubes: Equations no gravity
$$v_l = \frac{r^2 - R^2}{4 \mu} \frac{dp}{dx}$$

$$v_{\max} = - \frac{R^2}{4 \mu} \frac{dp}{dx}$$

$$V = - \frac{R^2}{8 \mu} \frac{dp}{dx}$$

$$Q = - \frac{\pi R^4}{8 \mu} \frac{dp}{dx}$$

$$Q = V A = V \pi R^2$$


### Velocity gradient at the wall
$$v_\alpha = \frac{r^2 - R^2}{4 \mu} \frac{dp}{dx}$$

$$\frac{dp}{dx} =  - \frac{8 \mu Q}{\pi R^4}$$

$$v_\alpha = - 2 Q \frac{r^2 - R^2}{\pi R^4}$$

$$\frac{d v_\alpha}{dr_{r = R}} = \frac{- 4 Q}{\pi R^3}$$

$$\frac{d v_\alpha}{dy_{y = 0}} = \frac{8 V_\alpha}{D}$$

$$\frac{d v_\alpha}{dy}_{y = 0} = \frac{6 V_\alpha}{S}$$


### Floc Rollup Constraint
$$v_\alpha \approx \left( \frac{6 V_\alpha}{S} \right) \frac{d}{2}$$

$$v_\alpha \approx \frac{3 V_{Plate \uparrow} d}{S \sin \alpha}$$

$$V_\alpha = \frac{V_{Plate \uparrow}}{\sin \alpha}$$

$$v_\alpha = V_{t \alpha} = V_t \sin \alpha$$

$$V_t \sin \alpha \approx \frac{3 V_{Plate \uparrow} d}{S \sin \alpha}$$

$$S \approx \frac{3 V_{Plate \uparrow} d}{V_t \sin^2 \alpha}$$

**Off-slide**
$$\begin{array}{l}
h = \frac{S}{2}
\\
u = \frac{1}{2 \mu} \left( \frac{\partial p}{\partial x} \right) \left( y^2 - h^2 \right)
\\
q = - \frac{2 h^3}{3 \mu} \left( \frac{\partial p}{\partial x} \right)
\\
- \frac{3 \mu q}{2 h^3} = \left( \frac{\partial p}{\partial x} \right)
\\
q = 2 V_\alpha h
\\
- \frac{3 \mu V_\alpha}{h^2} = \left( \frac{\partial p}{\partial x} \right)
\\
u = \frac{3}{2} V_\alpha \left( \frac{y^2 - h^2}{h^2} \right)
\\
u = \frac{3}{2 h^2} V_\alpha \left( y^2 - h^2 \right)
\\
2h = S
\\
\frac{du}{dy}_{y = h} = \frac{3y}{h^2} V_\alpha = \frac{3}{h} V_\alpha = \frac{6}{S} V_\alpha
\\
u ( d_{Floc} ) \approx \frac{6 d_{Floc}}{S} V_\alpha
\end{array}$$

$$\frac{3 d_{Floc}}{S} \frac{V_{Plate \uparrow}}{\sin \alpha} = \frac{g \sin (\alpha ) d_0^2}{18 \Phi \nu_{H_2O}} \frac{\rho_{Floc_0} - \rho_{H_2O}}{\rho_{H_2O}} \left( \frac{d}{d_0} \right)^{D_{Fractal} - 1}$$

$$V_{Plate \uparrow} = \frac{S g \sin^2(\alpha) d_0^{3 - D_{Fractal}} d^{D_{Fractal} - 2}}{54 \Phi \nu_{H_2O}}
\frac{\rho_{Floc_0} - \rho_{H_2O}} {\rho_{H_2O}}$$

$$S = V_{Plate \uparrow} \frac{54 \Phi \nu_{H_2O}}{g \sin^2(\alpha) d_0^{3 - D_{Fractal}} d^{D_{Fractal} - 2}}
\frac{\rho_{H_2O}}{\rho_{Floc_0} - \rho_{H_2O}}$$


### Spacing as a function of floc terminal velocity
$$S \approx \frac{3 V_{Plate \uparrow} d}{V_t \sin^2 \alpha}$$

$$d = d_0 \left( \frac{18 V_t \Phi \nu_{H_2O}}{g d_0^2} \frac{\rho_{H_2O}}{\rho_{Floc_0} - \rho_{H_2O}} \right)^\frac{1}{D_{Fractal} - 1}$$

$$S \approx \frac{3}{\sin^2 \alpha} \frac{V_{Plate \uparrow }}{V_t} d_0
\left( \frac{18 V_t \Phi \nu_{H_2O}}{g d_0^2} \frac{\rho_{H_2O}}{\rho_{Floc_0} - \rho_{H_2O}}
\right)^{\frac{1}{D_{Fractal} - 1}}$$


### Minimum plate settler spacing (function of $V_t$)
**Off-slide**
$$\frac{S}{d_0} \frac{V_t}{V_{Plate \uparrow}} \approx \frac{3}{\sin^2 \alpha}{\left( \frac{18 V_t \Phi \nu_{H_2O}}{g d_0^2} \frac{\rho_{H_2O}}{\rho_{Floc_0} - \rho_{H_2O}} \right)^\frac{1}{D_{Fractal} - 1}}$$


### Slide Capture Velocity
$$V_{Slide} \approx V_{Plate \uparrow}
\left[
  \left( \frac{3 d_0}{S \sin^2 \alpha} \right)^{D_{Fractal} - 1}
  \left(
    \frac{18 \Phi V_{Plate \uparrow } \nu_{H_2O}}{g d_0^2}
    \frac{\rho_{H_2O}}{\rho_{Floc_0} - \rho_{H_2O}}
  \right)
\right]^\frac{1}{D_{Fractal} - 2}$$


### Pressure drop (from head loss) through plate settlers
$$2 \tau L W = \Delta P W S$$

$$\Delta P = \frac{2 \tau L}{S}$$

$$\tau = \mu \frac{du}{dy}$$

$$\tau = \mu \left( \frac{6 V_{Plate \uparrow}}{S \sin \alpha} \right)$$

$$V_c = \frac{S V_{Plate \uparrow}}{L \sin \alpha \cos \alpha + S}$$

$$L = \frac{S \left( \frac{V_{Plate \uparrow}}{V_c} - 1 \right)}{\sin \alpha \cos \alpha}$$

$$\Delta P = 2 \mu \left( \frac{6 V_{Plate \uparrow}}{S \sin^2 \alpha \cos \alpha} \right) \left( \frac{V_{Plate \uparrow}}{V_c} - 1 \right)$$

$$h_{\rm{f}} = \frac{\Delta P}{\rho g}$$

$$h_{\rm{f}} = 2 \frac{\mu}{\rho g}
\left( \frac{6 V_{Plate \uparrow}}{S \sin^2 \alpha \cos \alpha} \right)
\left( \frac{V_{Plate \uparrow}}{V_c} - 1 \right)$$

$$V = \sqrt{2gh}$$



# Floc Blanket
### Density of the floc blanket
$$\rho_{FB} = 0.687 C_{FlocSolids} + \rho_{H_2O}$$

$$m_{Clay} = C_{Clay} V_{FB}$$

$$\rho_{FB} = \frac{m_{H_2O} + m_{Clay}}{V_{FB}}$$

$$\rho_{FB} = \left( 1 - \frac{C_{Clay}}{\rho_{Clay}} \right) \rho_{H_2O} + C_{Clay}$$

$$\rho_{FB} = \left( 1 - \frac{\rho_{H_2O}}{\rho_{Clay}} \right) C_{Clay} + \rho_{H_2O}$$

$$m_{H_2O} = \left( 1 - \frac{C_{Clay}}{\rho_{Clay}} \right) \rho_{H_2O} V_{FB}$$


### Flocculation in a floc blanket due to shear from suspended flocs
$$\frac{h_{L_{FB}}}{H_{FB}} = \frac{\rho_{FB} - \rho_{H_2O}}{\rho_{H_2O}}$$

$$\rho_{FB} = \left( 1 - \frac{\rho_{H_2O}}{\rho_{Clay}} \right) C_{Clay} + \rho_{H_2O}$$

$$G = \sqrt{ \frac{\varepsilon}{\nu} }$$

$$\varepsilon = \frac{g h_L}{\theta}$$

$$\theta = \frac{H_{FB} \phi_{FB}}{V_{Up}}$$

$$\varepsilon = \frac{g V_{Up}}{\phi_{FB}} \frac{h_L}{H_{FB}}$$

$$G = \sqrt{ \frac{g V_{Up}}{\nu \phi_{FB}} \frac{h_L}{H_{FB}} }$$

$$G = \sqrt {\frac{g V_{Up}}{\phi_{FB} \nu} \left( \frac{1}{\rho_{H_2O}} - \frac{1}{\rho_{Clay}} \right) C_{Clay} }$$

$$h_{L_{FB}} = H_{FB}
\left( \frac{\rho_{Clay}}{\rho_{H_2O}} - 1 \right)
\frac{C_{Clay}}{\rho_{Clay}}$$

**Off-slide**
$$\frac{\rho_{FB} - \rho_{H_2O}}{\rho_{H_2O}} =
\left( \frac{1}{\rho_{H_2O}} - \frac{1}{\rho_{Clay}} \right) C_{Clay}$$

$$G = \sqrt{ \frac{\rho_{FB} - \rho_{H_2O}}{\rho_{H_2O}} \frac{g V_{Up}}{\phi_{FB}\nu} }$$



# Diffusers
### Diffuser Slot Width
$$Q_{Diffuser} = V_{Jet} W_{Diffuser} S_{Diffuser} = V_{Sed} W_{Sed} B_{Diffuser}$$

$$W_{Diffuser} = \frac{V_{Sed} W_{Sed} B_{Diffuser}}{V_{Jet} S_{Diffuser}}$$

$$V_{Jet} = \sqrt{ 2 g h_{Jet} }$$

$$h_{Jet} = \frac{V_{Jet}^2}{2 g}$$

$$W_{Diffuser} = \frac{V_{Sed} W_{Sed} B_{Diffuser}}{S_{Diffuser} \sqrt{ 2 g h_{Jet} }}$$

$$B_{Diffusers}$$

**Off-slide**
$$\varepsilon_{Max} \cong \frac{\left( \Pi_{JetPlane} \frac{V_{Sed} W_{Sed} B_{Diffuser}}{S_{Diffuser}} \right)^3}{W_{Jet}^4}$$


### Diffuser Width
$$V_{Sed \uparrow} = 1 \frac{mm}{s}$$

$$h_{Jet} = 1 \, cm$$

$$W_{Sed} = 1 \, m$$

$$W_{Diffuser} = 2.7 \, mm$$

$$V_{Jet} = \frac{V_{Sed} W_{Sed} B_{Diffuser}}{W_{Diffuser} S_{Diffuser}}$$



# **Sedimentation Extras**
