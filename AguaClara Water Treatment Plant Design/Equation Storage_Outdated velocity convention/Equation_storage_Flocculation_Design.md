# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


# **Flocculation Design**
### Floc model for viscous dominated collisions
$$v_r \approx \Lambda G$$

$$pC^\ast = \frac{3}{2}\log \left( \frac{2}{3} \pi k\frac{d_{Clay}^2}{\Lambda_0^2} \bar Gt \alpha + 1 \right)$$

$$\bar Gt = \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_{Clay}^2 \alpha }$$

$$\left( \frac{\varepsilon}{\nu} \right)^\frac{1}{2}$$


### Head Loss coefficient for a Baffle
$$h_e = \frac{V_{out}^2}{2g} \left( \frac{A_{out}}{A_{in}} - 1 \right)^2$$

$$K_e = \left( \frac{A_{out}}{A_{in}} - 1 \right)^2$$

$$K_e = \left( \frac{1}{\Pi_{VCBaffle}} - 1 \right)^2 = 2.56$$


### Simplify flocculator design by designing for high efficiency
$$\Pi_{\bar \epsilon}^{\epsilon_{Max}}  = \frac{\varepsilon_{Max}}{\bar \varepsilon}$$

$$\Pi_{\bar{\epsilon}}^{\epsilon_{Max}}$$


### Collision Potential
$$\bar G\theta  = \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_P^2 \alpha}$$


### Energy use (head loss) in flocculation controls velocity gradient
$$g h_{Floc} =  \theta \bar \varepsilon$$

$$h_e = K_e \frac{V^2}{2g}$$

$$h_{Floc} = \sum K_e \frac{V^2}{2g}$$

$$\bar G = \sqrt{ \frac{\bar \varepsilon}{\nu}}$$

$$\bar \varepsilon = \nu \bar G^2$$

$$h_{Floc} = \bar G \theta \frac{\nu \bar G}{g}$$


### The design inputs for Flocculation
$$\bar G \theta  = \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_P^2 \alpha}$$


### Key equations that we can use to design flocculators
$$g h_e = K_e \frac{V^2}{2}$$

$$g h_e = \theta \bar \varepsilon$$

$$\bar G = \sqrt{ \frac{\bar \varepsilon}{\nu}}$$

$$\bar V  = \frac{H_e}{\theta}$$

$$\bar V = \frac{Q}{W S}$$


### Our current choice of parameter that sets energy input is head loss
$$\bar G = \sqrt{ \frac{g h_e}{\theta \nu}}$$

$$\theta = \frac{G \theta}{G}$$

$$h_{Floc} = \bar G \theta \frac{\nu \bar G}{g}$$

$$\bar G = \frac{g h_{Floc}}{\left( \bar G \theta \right) \nu}$$

$$\bar G \theta  = \sqrt{ \frac{g h_e \theta}{\nu}}$$


### Design the reactor geometry to get the target velocity gradient
$$\bar \varepsilon = K_e \frac{\bar V^2}{2} \frac{1}{\theta}$$

$$\bar \varepsilon  = \nu \bar G^2$$

$$\nu \bar G^2 = \frac{K_e \bar V^3}{2 H_e}$$

$$\theta  = \frac{H_e}{\bar V}$$

$$\bar V = \frac{Q}{W S}$$

$$\nu \bar G^2 = \frac{K_e}{2 H_e} \left( \frac{Q}{W S} \right)^3$$

$$\bar G = \sqrt{ \frac{K_e}{2 \nu H_e} \left( \frac{Q}{W S} \right)^3}$$

**Off-slide**
$$S = \left[ \frac{K_{Exp}}{2 \Pi_{HS_{Max}}\bar \varepsilon } \left( \frac{Q}{W} \right)^3 \right]^\frac{1}{4}$$


### Solve for channel width to set constraints on viable solutions
$$\nu \bar G^2 = \frac{K_e}{2 H_e} \left( \frac{Q}{W S} \right)^3$$

$$W = \frac{Q}{S}\left( \frac{K_e}{2 H_e \nu \bar G^2} \right)^\frac{1}{3}$$

$$S = \frac{H_e}{\Pi_{HS}}$$

$$H_e = \Pi_{HS}S$$

$$W_{Min} = \frac{\Pi_{HS} Q}{H_e} \left( \frac{K_e}{2 H_e \nu \bar G^2} \right)^\frac{1}{3}$$


### Minimum number of expansions per depth of flocculator (given W)
$$\Pi_{HS} = \frac{H_e}{S}$$

$$S = \frac{H_{e_{Max}}}{\Pi_{HS_{Max}}}$$

$$H_{e_{Max}} = \left[ \frac{K_e}{2 \nu \bar G^2} \left( \frac{Q \Pi_{HS_{Max}}}{W} \right)^3 \right]^\frac{1}{4}$$

$$N_{e_{Min}} = \frac{H_{Floc}}{H_{e_{Max}}}$$


### Design Algorithm (as of 2016) Start with $ℎ_{𝐹𝑙𝑜𝑐}$ and G $\theta$
$$\bar G = \frac{g h_{Floc}}{\left( \bar G \theta \right) \nu}$$

$$\theta = \frac{G \theta}{G}$$

$$W_{Min} = \frac{\Pi_{HS} Q}{H_e} \left( \frac{K_e}{2 H_e \nu \bar G^2} \right)^\frac{1}{3}$$

$$S = \left( \frac{K_e}{2 H_e G^2 \nu } \right)^\frac{1}{3} \frac{Q}{W}$$

$$N_{e_{Min}} = \frac{H_{Floc}}{H_{e_{Max}}}$$


### Viscous Collision Potential per Flow Expansion (the detailed perspective)
$$G \theta  = \theta \sqrt \frac{\varepsilon}{\nu}$$

$$\theta_e = \frac{H_e}{\bar V}$$

$$\bar \varepsilon = K_e \frac{\bar V^2}{2} \frac{\bar V}{H_e}$$

$$G \theta_e = \frac{H_e}{\bar V} \sqrt{ \frac{K_e}{\nu} \frac{\bar V^2}{2} \frac{\bar V}{H_e}}$$

$$G \theta_e = \sqrt{ \frac{H_e K_e \bar V}{2 \nu}}$$

$$G \theta_e = \sqrt{ \frac{H_e K_e Q}{2\nu W S}}$$


### Velocity guidelines?
$$\nu \bar G^2 = \frac{K_e V^3}{2 H_e}$$

$$\varepsilon_{Max} \cong \frac{\left( \Pi_{RoundJet} V_{Jet} \right)^3}{D_{Jet}}$$


### Use a Pipe with orifices to make a flocculator for small flows (S = D)
$$\nu \bar G^2 = \frac{K_e V^3}{2 H_e}$$

$$\bar V = \frac{4 Q}{\pi D_{Pipe}^2}$$

$$H_e = \Pi_{HS} D_{Pipe}$$

$$\nu \bar G^2 = \frac{K_e}{2 \Pi_{HS} D_{Pipe}} \left( \frac{4 Q}{\pi D_{Pipe}^2} \right)^3$$

$$D_{Pipe} = \left[ \frac{K_e}{2 \Pi_{HS} \nu \bar G^2} \left( \frac{4 Q}{\pi} \right)^3 \right]^\frac{1}{7}$$

**Off-slide**
$$\bar \varepsilon = \left( \frac{g H L_{Floc}}{\alpha_\varepsilon ^\frac{1}{6} \psi_{Floc}} \right)^\frac{3}{2}$$

$$S = \left[ \frac{K_{Exp}}{2 \Pi_{HS_{Max}} \bar \varepsilon} \left( \frac{Q}{W} \right)^3 \right]^\frac{1}{4}$$


### Estimate the orifice diameter
$$K_{e_{orifice}} = \left( \frac{D_{Pipe}^2}{\Pi_{vc} D_{Orifice}^2} - 1 \right)^2$$

$$D_{Orifice} = \frac{D_{Pipe}}{\sqrt{ \Pi_{vc} \left( \sqrt{ K_{e_{orifice}}}  + 1 \right)} }$$


### Estimate the orifice diameter using the required value of Ke given the actual pipe ID
$$H_e = \Pi_{HS} D_{Pipe}$$

$$h_e = K_e \frac{V^2}{2 g}$$

$$\bar G = \sqrt{ \frac{g h_e}{\theta \nu}}$$

$$\bar G = \sqrt{ \frac{4 g h_e Q}{\nu \pi  H_e D_{Pipe}^2} }$$

$$h_e = \frac{\bar G^2 \nu \pi H_e D_{Pipe}^2}{4 g Q}$$

$$h_e = K_e \frac{V^2}{2 g}
= K_e \frac{16Q^2}{2 g \pi^2 D_{Pipe}^4}
= \frac{\bar G^2 \nu \pi H_e D_{Pipe}^2}{4 g Q}$$

$$K_e = \frac{\pi^3 D_{Pipe}^7 \bar G^2 \nu \Pi_{HSMax}}{32 Q^3}$$


### Use a Pipe with orifices to make a flocculator for small flows (H = D)
$$\nu \bar G^2 = \frac{K_e V^3}{2 H_e}$$

$$\bar V = \frac{4 Q}{\pi D_{Pipe}^2}$$

$$H_e = D_{Pipe}$$

$$\nu \bar G^2 = \frac{K_e}{2 D_{Pipe}} \left( \frac{4 Q}{\pi D_{Pipe}^2} \right)^3$$

$$D_{Pipe} = \left[ \frac{K_e}{2 \nu \bar G^2} \left( \frac{4 Q}{\pi} \right)^3 \right]^\frac{1}{7}$$

**Off-slide**
$$\bar \varepsilon = \left( \frac{g H L_{Floc}}{\alpha_\varepsilon ^\frac{1}{6} \psi_{Floc}} \right)^\frac{3}{2}$$

$$S = \left[ \frac{K_{Exp}}{2 \Pi_{HS_{Max}} \bar \varepsilon} \left( \frac{Q}{W} \right)^3 \right]^\frac{1}{4}$$


### Reflection Questions
**Off-slide**
$$\bar G \theta_e = \sqrt{ \frac{H_e K_e Q}{2 \nu W S}}$$

$$\Pi_{\bar G}^{G_{Max}} = \sqrt{ \Pi_{\bar \epsilon}^{\epsilon_{Max}} }  = \sqrt{2}$$

$$\bar G^2 \nu \theta = g h_{Floc} = \sum K_e \frac{V^2}{2}$$


### Shear limits the size of flocs by not allowing them to grow
$$\begin{array}{l}
V_{r_1} =  - \frac{Gr_1}{2}
\\ \\
V_{r_2} =  + \frac{Gr_2}{2}
\\ \\
\Delta V_r = \frac{G}{2} \left( r_1 + r_2 \right)
\\ \\
\left( r_1 + r_2 \right)_{Max} = \frac{2 \Delta V_{r_{Max}}}{G}
\end{array}$$


### Estimating the ratio
$$\varepsilon_{Max} \frac{ \left( \Pi_{JetPlane} V_{Jet} \right)^3}{S_{Jet}}$$

$$\Pi_{\bar \epsilon}^{\epsilon_{Max}} = \frac{\varepsilon_{Max}}{\bar \varepsilon}$$

$$\bar V = \frac{Q}{SW}$$

$$\varepsilon_{Max} \frac{1}{S \Pi_{VCBaffle}} \left( \frac{\Pi_{JetPlane} \bar V}{\Pi_{VCBaffle}} \right)^3$$

$$V_{Jet} = \frac{\bar V}{\Pi_{VCBaffle}}$$

$$\bar \varepsilon = K_e \frac{\bar V^2}{2} \frac{1}{\theta_B} = \frac{K_e}{\bar V^3} 2 H_e$$

$$\theta_B = \frac{H}{\bar V}$$

$$\Pi_{\bar \epsilon}^{\epsilon_{Max}} = \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \frac{2 H_e}{K_e S}$$

**Off-slide**
$$\begin{array}{l}
K_B = \left( \frac{1}{\Pi_{vc}^2} - 1 \right)^2
\\
\Pi_{VCBaffle} = \frac{1}{\sqrt{K_B}  + 1}
\\
\Pi_{VCBaffle}^2 = \frac{1}{\left( \sqrt{K_B}  + 1 \right)^2}
\\
\Pi_{VCBaffle}^2 = \frac{1}{K_B + 2 \sqrt{K_B}  + 1}
\end{array}$$

$$\alpha_\varepsilon = \frac{1}{S \Pi_{VCBaffle}} \left( \frac{\Pi_{PlaneJet} \bar V}{\Pi_{VCBaffle}} \right)^3 \frac{2 H}{K_B \bar V^3}$$

$$\varepsilon_{Max} \cong 2 \Pi_{JetPlane}^3 \frac{V_{Jet}^2}{2} \frac{V_{Jet}}{S_{Jet}}$$

### Estimating $\Pi_{JetPlane}$
$$\Pi_{\bar \epsilon}^{\epsilon_{Max}}$$

$$\frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \frac{2 H_e}{K_e S}$$

$$\Pi_{JetPlane} = 0.225$$

$$\Pi_{JetPlane} = \left(
  \Pi_{\bar \epsilon}^{\epsilon_{Max}} \Pi_{VCBaffle}^4 \frac{K_e}{2} \frac{S}{H_e}
  \right)^\frac{1}{3}$$


### Results of the CFD analysis and our model equations
$$\frac{\Pi_{VCBaffle}^4 K_e}{\Pi_{JetPlane}^3}$$

$$\Pi_{\bar \epsilon}^{\epsilon_{Max}} = \frac{\varepsilon_{Max}}{\bar \varepsilon } = \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \frac{2 H_e}{K_e S}$$

$$\Pi_{\bar \epsilon}^{\epsilon_{Max}} = 2$$

$$\Pi_{\bar G}^{G_{Max}} = \sqrt{ \Pi_{\bar \epsilon}^{\epsilon_{Max}} }  = \sqrt{2}$$
