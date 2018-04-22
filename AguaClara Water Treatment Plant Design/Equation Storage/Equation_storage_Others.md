# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


# **Disinfection**
###Chlorine and pH
$$pC^\ast = \frac{t_{contact} \cdot C_{Cl}^{0.85}}{0.2828 \left( pH^{2.69} \right)
\left( 0.933^{\left( T - 5 \right)} \right)}$$


### CT equation for Giardia
$$C_{Cl} \cdot t_{contact} = 0.2828 \left( pH^{2.69} \right)
\left( C_{Cl}^{0.15} \right)
\left( 0.933^{\left( T - 5 \right)} \right) pC^\ast$$

$$t_{contact} = 0.2828 \left( pH^{2.69} \right)
\left( C_{Cl}^{- 0.85} \right)
\left( 0.933^{\left( T - 5 \right)} \right) pC^\ast$$


### Dark side of Chlorine
$$\frac{1}{14,990 \frac{0.15}{312,640,961}} = 139,044$$



# **Disinfection Extras**
### Pathogen Poisson Process Probability
$$P_k = \frac{\left( C V \right)^k}{k!} e^{- C V}$$

$$P_k = \frac{\left( 2 \right)^2}{2!} e^{- 2} = 0.27$$


### Find probability that k > 0
$$P_k = \frac{\left( C V \right)^k}{k!} e^{- C V}$$

$$P_{k = 0} = \frac{\left( C V \right)^0}{0!} e^{- C V} = e^{- C V}$$

$$P_{k > 0} = 1 - e^{- C V}$$



# **Flocculator Extras**
$$\bar \varepsilon  = G^2 \nu$$

**Off-slide**
$$\begin{array}{l}
\frac{\bar \varepsilon}{\nu} = G^2
\\
\bar \varepsilon \theta = g h_l
\\
G = \sqrt{ \frac{g h_l}{\nu \theta} }
\end{array}$$


### Extracting eMax from Fluid Velocity Design Guidelines?
$$\bar \varepsilon = K_B \frac{\bar V^3}{2 H}$$


### Horizontal Flow Flocculator
$$S = \left( \frac{K_e}{2 H_e} \bar \varepsilon \right)^\frac{1}{3} \frac{Q}{W}$$

$$\theta_{Floc} = \left( \frac{\alpha_\varepsilon^\frac{1}{2} \psi_{Floc}^3}{g h_{Floc}} \right)^\frac{1}{2} = 390 \, {\rm s} = 6.5\min $$


### Minimum Flow rate for Horizontal Flocculators given H?
$$Q = W S \left( \frac{H \varepsilon_{\max}}{K_B} \right)^\frac{1}{3}$$

$$Q = W S^\frac{4}{3} \left( \frac{H}{S} \frac{\varepsilon_{Max}}{K_B} \right)^\frac{1}{3}$$


### Minimum Flow rate for Horizontal Flocculators?
$$Q_{Min} = W S^\frac{4}{3} \left( \frac{H}{S} \frac{2 \bar \varepsilon}{K_B} \right)^\frac{1}{3}$$


### Hydrostatic Force: Vertical flow flocculator
$$\begin{array}{l}
F_R = p_c A
\\
p_c = \rho g h_c
\\
F_R = \rho g h_c A
\end{array}$$


### Hydrostatic Force
$$\begin{array}{l}
H = 2 \, {\rm m}
\\
S = 0.67 \, {\rm m}
\\
W = 0.9 \, {\rm m}
\end{array}$$

$$H_{Baffle} = H - S = 2 \, {\rm m} - 0.67 \, {\rm m} = 1.33 \, {\rm m}$$

$$h_c = H_{Baffle} - \frac{H_{Plate}}{2}$$

$$H_{Plate} = \frac{H_{Baffle}}{4}$$

$$h_c = \frac{7}{8} H_{Baffle}$$

$$A = H_{Plate} W$$

$$F_R = \rho g h_c A$$

$$F_R = \frac{7}{8} \rho g H_{Baffle} H_{Plate} W$$

$$F_R ={\rm
  \frac{7}{8} \left( 1000 \frac{kg}{m^3} \right)
\left( 9.8\frac{m}{s^2} \right)
\left( 1.33 \, m \right)
\left( \frac{1.33 \, m}{4} \right)
\left( 0.9 \, m \right)
}$$


### Smallest Turbulent Flow Flocculator (analysis for lab flocculator)
$$S = \left( \frac{K_B}{H \varepsilon_{Max}} \right)^\frac{1}{3} \frac{Q}{W}$$

$$W = S$$

$$\frac{H}{S} = \Pi_{HS}$$

$$Q = \left( \frac{S^7 \Pi_{HS} \varepsilon_{Max}}{K_B} \right)^\frac{1}{3}$$

$$V = \frac{Q}{W S} = \frac{Q}{S^2} = \left( \frac{S \Pi_{HS} \varepsilon_{Max}}{K_B} \right)^\frac{1}{3}$$


### Add Reynolds constraint
$${\rm Re} = \frac{V d}{\nu} = \frac{S}{\nu} V$$

$$V = \left( \frac{S \Pi_{HS} \varepsilon_{Max}}{K_B} \right)^\frac{1}{3}$$

$${\rm Re} = \frac{S}{\nu} \left( \frac{S \Pi_{HS} \varepsilon_{Max}}{K_B} \right)^\frac{1}{3}$$

$$S = \left( \frac{\left( \nu {\rm Re} \right)^3 K_B}{\Pi_{HS} \varepsilon_{Max}} \right)^\frac{1}{4}$$


### Minimum Turbulent Flow Flocculation
$$Q = \left( \frac{S^7 \Pi_{HS} \varepsilon_{Max}}{K_B} \right)^\frac{1}{3}$$

$$S = \left( \frac{\left( \nu {\rm Re} \right)^3 K_B}{\Pi_{HS} \varepsilon_{Max}} \right)^\frac{1}{4}$$

$$Q = \left( \frac{\left( \nu {\rm Re} \right)^7 K_B}{\Pi_{HS} \varepsilon_{Max}} \right)^\frac{1}{4}$$


### Get equation for Spacing as function of head loss
$$h_e = \frac{\bar \varepsilon^\frac{2}{3} \alpha_\varepsilon^\frac{1}{6} \psi}{g}$$

$$\bar \varepsilon = \left( \frac{K_B}{2 H} \right)
\left( \frac{Q}{W S} \right)^3$$

$$h_e = \frac{\psi \alpha_\varepsilon^\frac{1}{6}}{g}
\left( \frac{K_B}{2 H} \right)^\frac{2}{3}
\left( \frac{Q}{W S} \right)^2$$

$$\alpha_\varepsilon = \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \frac{2 H}{K_B S}$$

$$h_e = \left( \frac{K_B}{2 H} \right)^\frac{1}{2}
\left( \frac{Q}{W} \right)^2
\frac{\psi}{g}
\left( \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \right)^\frac{1}{6}
\frac{1}{S^\frac{13}{6}}$$

$$S = \left[
  \left( \frac{K_B}{2 H} \right)^\frac{1}{2}
  \left( \frac{Q}{W} \right)^2
  \frac{\psi}{g h_e}
\right]^\frac{6}{13}
\left( \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \right)^\frac{1}{13}$$

$$\alpha_\varepsilon = 2$$

$$h_e = \frac{\psi}{\sqrt 2 g}
\left( \frac{K_B}{H} \right)^\frac{2}{3} \left( \frac{Q}{W S} \right)^2$$

$$\begin{array}{l}
S = \sqrt{ \frac{\psi}{\sqrt{2} g h_e} }
\left( \frac{K_B}{H} \right)^\frac{1}{3}
\left( \frac{Q}{W} \right)
\\
\frac{H}{S} = \Pi_{HS}
\\
S = \left( \frac{\psi}{\sqrt{2} g h_e} \right)^\frac{3}{8}
\left( \frac{K_B}{\Pi_{HS}} \right)^\frac{1}{4}
\left( \frac{Q}{W} \right)^\frac{3}{4}
\\
S = W = \left( \frac{\psi}{\sqrt{2} g h_e} \right)^\frac{3}{14}
\left( \frac{Q^3 K_B}{\Pi_{HS}} \right)^\frac{1}{7}
\end{array}$$

**Off-slide**
$$\theta = \frac{\alpha_\varepsilon^\frac{1}{6} \psi}{\bar \varepsilon^\frac{1}{3}}$$

$$S = W = \left( \frac{\psi}{\sqrt{2} g H_L} \right)^\frac{1}{4}
\left( \frac{K_B}{H} \right)^\frac{1}{6} \sqrt{Q}$$


### Find $\alpha_\varepsilon$ as function of head loss
$$\alpha_\varepsilon = \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \frac{2 H}{K_B S}$$

$$S = \left[
  \left( \frac{K_B}{2 H} \right)^\frac{1}{2}
  \left( \frac{Q}{W} \right)^2
  \frac{\psi}{g h_e}
\right]^\frac{6}{13}
\left( \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \right)^\frac{1}{13}$$

$$\alpha_\varepsilon = \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^{12}
\left( \frac{2 H}{K_B} \right)^{16}
\left( \frac{g h_e}{\psi} \right)^6
\right]^\frac{1}{13}$$

$$\alpha_\varepsilon = 2$$

**Off-slide**
$$S = \left[
  \left( \frac{K_B}{2 H} \right)^\frac{1}{2}
  \left( \frac{Q}{W} \right)^2
  \frac{\psi}{g H_L}
\right]^\frac{6}{13}
\left( \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \right)^\frac{1}{13}$$

$$\alpha_\varepsilon = \left[
\left( \frac{\Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \frac{W}{Q} \right)^{12}
\left[ \frac{g H_L}{\psi} \right]^6 \left( \frac{2 H}{K_B} \right)^{16} \right]^\frac{1}{13}$$


### Find residence time as function of Head Loss
$$\theta = \frac{\psi \alpha_\varepsilon^\frac{1}{6}}{\bar \varepsilon^\frac{1}{3}}$$

$$\bar \varepsilon =
\left( \frac{g h_e}{\alpha_\varepsilon^\frac{1}{6} \psi} \right)^\frac{3}{2}$$

$$\theta = \alpha_\varepsilon^\frac{1}{4} \sqrt{ \frac{\psi^3}{g h_e} }$$

$$\alpha_\varepsilon = \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^{12}
\left( \frac{2 H}{K_B} \right)^{16}
\left( \frac{g h_e}{\psi} \right)^6
\right]^\frac{1}{13}$$

$$\theta = \psi \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g h_e} \right)^5
\right]^\frac{1}{13}$$

$$\theta = 2^\frac{1}{4} \sqrt{ \frac{\psi^3}{g h_e} }$$

**Off-slide**
$$\theta = \psi \left[
\left( \frac{W \Pi_{PlaneJet}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{g H_L}{\psi} \right)^\frac{3}{2}
\right]^\frac{1}{13} \sqrt{ \frac{\psi}{g H_L} }$$

$$\theta = \psi \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g H_L} \right)^5
\right]^\frac{1}{13}$$


### Plan View Area as a function of head loss
$$A_{Plan} = \frac{Q \theta}{H}$$

$$\theta = \psi \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g h_e} \right)^5
\right]^\frac{1}{13}$$

$$A_{Plan} = \frac{\psi Q}{H} \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g h_e} \right)^5
\right]^\frac{1}{13}$$

$$\theta = 2^\frac{1}{4} \sqrt{ \frac{\psi^3}{g h_e} }$$

$$A_{Plan} = 2^\frac{1}{4} \frac{\psi Q}{H} \sqrt{ \frac{\psi}{g h_e} }$$


### Cost of floc baffles and walls due to head loss
$$Cost_{Floc} = Cost_A A_{Plan} + Cost_{h_e} h_e + Cost_{A*h_e} A_{Plan} h_e^\frac{5}{4}$$

$$\frac{A_{Plan}}{W_{Floc}} h_e + \frac{A_{Plan}}{S_{Floc}} h_e$$

$$S = W =
\left( \frac{\psi}{\sqrt{2} g h_e} \right)^\frac{1}{4}
\left( \frac{K_B}{H} \right)^\frac{1}{6} \sqrt{Q}$$

$$Cost_{A*h_e} = \frac{\frac{A_{Plan}}{W_{Floc}} h_e + \Pi_{Baffles} \frac{A_{Plan}}{S_{Floc}} h_e}{A_{Plan} h_e^\frac{5}{4}}$$

$$Cost_{A*h_e} = \left( 1 + \Pi_{Baffles} \right) \frac{A_{Plan} h_e}{S_{Floc} A_{Plan} h_e^\frac{5}{4}}$$


### Cost as function of head loss
$$\begin{array}{l}
Cost_{Floc} = Cost_A \frac{\psi Q}{H} \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g h_e} \right)^5
\right]^\frac{1}{13} + Cost_{h_e} h_e
\\
\frac{dCost_{Floc}}{dh_e} = \frac{- 5}{13} Cost_A \frac{\psi Q}{H} \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g} \right)^5 \frac{1}{h_e^{18}}
\right]^\frac{1}{13} + Cost_{h_e}
\\
h_e = \left[
\left( \frac{5 Cost_A}{13 Cost_{h_e}} \frac{\psi Q}{H} \right)^{13}
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g} \right)^5
\right]^\frac{1}{18}
\\
h_e = \psi \left[
\left( \frac{5 Cost_A}{13 Cost_{h_e}} \right)^{13}
\left( \frac{W \Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \right)^3
\left( \frac{2}{K_B} \right)^4 \frac{Q^{10}}{g^5 H^9}
\right]^\frac{1}{18}
\end{array}$$

$$\begin{array}{l}
Cost_{Floc} = Cost_A 2^\frac{1}{4} \frac{\psi Q}{H} \sqrt{ \frac{\psi}{g h_e} }  + Cost_{h_e} h_e + Cost_{A*h_e} 2^\frac{1}{4} \frac{\psi Q}{H} \sqrt{ \frac{\psi}{g h_e} } h_e^\frac{5}{4}
\\
\frac{dCost_{Floc}}{dh_e} = - \frac{1}{2} Cost_A 2^\frac{1}{4} \frac{\psi Q}{H} \sqrt{ \frac{\psi}g h_e^3}  + Cost_{h_e} + \frac{3}{4} Cost_{A*h_e} 2^\frac{1}{4} \frac{\psi Q}{H h_e^\frac{1}{4}} \sqrt{ \frac{\psi}{g} }
\end{array}$$

**Off-slide**
$$\begin{array}{l}
Cost_{Floc} = Cost_A \frac{\psi Q}{H} \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g H_L} \right)^5
\right]^\frac{1}{13} + Cost_{H_L} H_L
\\
\frac{dCost_{Floc}}{dH_L} = \frac{- 5}{13} Cost_A \frac{\psi Q}{H} \left[
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g} \right)^5 \frac{1}{H_L^{18}}
\right]^\frac{1}{13} + Cost_{H_L}
\\
H_L = \left[
\left( \frac{5 Cost_A}{13 Cost_{H_L}} \frac{\psi Q}{H} \right)^{13}
\left( \frac{W \Pi_{JetPlane}^3}{Q \Pi_{VCBaffle}^4} \right)^3
\left( \frac{2 H}{K_B} \right)^4
\left( \frac{\psi}{g} \right)^5
\right]^\frac{1}{18}
\\
H_L = \psi \left[
\left( \frac{5 Cost_A}{13 Cost_{H_L}} \right)^{13}
\left( \frac{W \Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4} \right)^3
\left( \frac{2}{K_B} \right)^4 \frac{Q^{10}}{g^5 H^9}
\right]^\frac{1}{18}
\end{array}$$


### Head loss
$$h_e = \frac{\psi}{g} \frac{\varepsilon_{Max}^\frac{2}{3}}{\alpha_\varepsilon^\frac{1}{2}}$$

$$\alpha_\varepsilon = \frac{\Pi_{JetPlane}^\frac{9}{4}}{\Pi_{VCBaffle}^3} \frac{2 H \varepsilon_{Max}^\frac{1}{4} W^\frac{3}{4}}{Q^\frac{3}{4} K_B}$$

$$h_e = \frac{\psi}{g} \frac{\varepsilon_{Max}^\frac{2}{3}}{
  \sqrt{ \frac{\Pi_{JetPlane}^\frac{9}{4}}{\Pi_{VCBaffle}^3} \frac{2 H \varepsilon_{Max}^\frac{1}{4} W^\frac{3}{4}}{Q^\frac{3}{4} K_B} }
}$$

$$h_e = \varepsilon_{Max}^\frac{13}{24} \frac{\psi}{g}
\left( \frac{K_B \Pi_{VCBaffle}^3}{2 H} \right)^\frac{1}{2}
\left( \frac{Q}{W \Pi_{JetPlane}^3} \right)^\frac{3}{8}$$


### What is the cost ratio?
$$Cost_{A h_e} = \frac{Cost_A}{Cost_{h_e}}$$

$$Cost_A = 2 \frac{T_{Wall} + W_{Floc}}{W_{Floc}} + \frac{H_{Floc}}{W_{Floc}}$$

$$Cost_{h_e} = 4 \sqrt{ Q_{Plant} A_{Plant} }$$

$$Cost_{A h_e} = \frac{2 + \frac{H_{Floc}}{W_{Floc}}}{4 \sqrt{ Q_{Plant} A_{Plant} }}$$


### Can I find Q where H/S is at transition?
$$S = \sqrt{ \frac{\psi}{\sqrt{2} g h_e} }
\left( \frac{K_B}{H} \right)^\frac{1}{3}
\left( \frac{Q}{W} \right)$$

$$Q_{Transition} = \sqrt{ \left( W S \right)^3 \frac{Cost_A}{Cost_{h_e}} \frac{g}{K_B} }$$

$$Q_{Transition} = \left[
\left( W \frac{H \Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4 K_B} \right)^3
\frac{2 + \frac{H_{Floc}}{W_{Floc}}}{4 \sqrt{A_{Plant}} }
\frac{g}{K_B} \right]^\frac{2}{5}$$

$$h_e = \frac{\psi}{2^\frac{1}{2} g^\frac{1}{3}}
\left( \frac{Cost_A}{Cost_{h_e}} \frac{Q}{H} \right)^\frac{2}{3}$$

$$S = \frac{H \Pi_{JetPlane}^3}{\Pi_{VCBaffle}^4 K_B}$$

$$Cost_{A h_e} = \frac{2 + \frac{H_{Floc}}{W_{Floc}}}{4 \sqrt{ Q_{Plant} A_{Plant} }}$$


### Starting from Max EDR
$$\theta = \frac{\alpha_\varepsilon^\frac{1}{2} \psi}{\varepsilon_{Max}^\frac{1}{3}}$$

$$h_e = \frac{\psi}{g} \frac{\varepsilon_{Max}^\frac{2}{3}}{\alpha_\varepsilon^\frac{1}{2}}$$

$$h_e = \frac{\psi \varepsilon_{Ave}^\frac{2}{3} \alpha_\varepsilon^\frac{1}{6}}{g}$$

$$\varepsilon_{Ave} =
\left( \frac{g h_e}{\psi \alpha_\varepsilon^\frac{1}{6}} \right)^\frac{3}{2}$$

$$S = \left( \frac{K_B}{2 H \bar \varepsilon} \right)^\frac{1}{3} \frac{Q}{W}$$

$$\bar \varepsilon = \frac{K_B}{2 H} \left( \frac{Q}{W S} \right)^3$$


### Starting from Average EDR
$$\theta = \frac{\psi \alpha_\varepsilon^\frac{1}{6}}{\bar \varepsilon^\frac{1}{3}}$$

$$h_e = \frac{\bar \varepsilon^\frac{2}{3} \alpha_\varepsilon^\frac{1}{6} \psi}{g}$$

$$W = \Pi_{HS} \left( \frac{K_B}{2 H \bar \varepsilon} \right)^\frac{1}{3} \frac{Q}{H}$$

$$S = \frac{H}{\Pi_{HS}}$$

**Off-slide**
$$\bar \varepsilon = \frac{K_B}{2 H} \left( \frac{Q}{W S} \right)^3$$

$$S = \left( \frac{K_B}{2 H \bar \varepsilon} \right)^\frac{1}{3} \frac{Q}{W}$$

$$S = \left( \frac{K_B}{2 \Pi_{HS} \bar \varepsilon} \right)^\frac{1}{4}
\left( \frac{Q}{W} \right)^\frac{3}{4}$$

$$\begin{array}{l}
S = \left( \frac{K_B}{2 S \Pi_{HS} \bar \varepsilon} \right)^\frac{1}{3}
\frac{Q}{W}
\\
\frac{H}{S} = \Pi_{HS}
\\
S = \left( \frac{K_B}{2 \Pi_{HS} \bar \varepsilon} \right)^\frac{1}{4}
\left( \frac{Q}{W} \right)^\frac{3}{4}
\end{array}$$


### Find maximum H given minimum W
$$\bar \varepsilon = \frac{K_B}{2 H} \left( \frac{Q}{W S} \right)^3$$

$$W = \Pi_{HS} \left( \frac{K_B}{2 H \bar \varepsilon} \right)^\frac{1}{3} \frac{Q}{H}$$

$$H = \left( \frac{K_B}{2 \bar \varepsilon} \right)^\frac{1}{4} \left( \frac{\Pi_{HS} Q}{W} \right)^\frac{3}{4}$$


### Find min Q that doesn’t require obstacles
$$\bar \varepsilon = \frac{K_B}{2 H} \left( \frac{Q}{W S} \right)^3$$

$$Q = \left( \frac{2 H \bar \varepsilon}{K_B} \right)^\frac{1}{3} W S$$

$$S = \frac{H}{\Pi_{HS}}$$

$$Q = \left( \frac{2 H \bar \varepsilon}{K_B} \right)^\frac{1}{3} W \frac{H}{\Pi_{HS}}$$


### Find Max Q for vertical flow flocculator
$$\bar \varepsilon = \frac{K_B}{2 H} \left( \frac{Q}{W S} \right)^3$$

$$Q = \left( \frac{2 H \bar \varepsilon}{K_B} \right)^\frac{1}{3} W \frac{H}{\Pi_{HS}}$$
