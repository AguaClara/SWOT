# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


# **Flow Control and Measurement**
### Why is there drag?
$$\frac{p_1}{\rho g} + {z_1} + \frac{V_1^2}{2g} = \frac{p_2}{\rho g } + {z_2} + \frac{V_2^2}{2g}$$


### Orifice Equation
$${A_{vc}} = {\Pi_{vc}}{A_{or}}$$

$$Q = VA$$

$$Q = \Pi_{vc} A_{or} \sqrt{2g\Delta h}$$

$$\frac{p_{in}}{\rho g} + z_{in} + \alpha_{in} \frac{V_{in}^2}{2g} + h_P = \frac{p_{out}}{\rho g} + z_{out} + {\alpha_{out}} \frac{V_{out}^2}{2g} + h_T + h_L$$


### Head Loss in a Long STRAIGHT Tube (due to wall shear): Major Losses
$$h_{\rm{f}} = {\rm{f}} \frac{8}{g \pi^2} \frac{LQ^2}{D^5}$$

$${\rm{Re}}=\frac{4Q}{\pi D\nu} = \frac{\rho VD}{\mu} = \frac{VD}{\nu}$$

$$\rm{f} = \frac{64}{Re}$$


$$h_{\rm{f}} = \frac{32\mu L V}{\rho gD^2} = \frac{128\mu Q}{\rho g\pi D^4}$$

$${\rm{f}} = \frac{0.25} {\left[ \log \left( \frac{\epsilon }{3.7D} + \frac{5.74}{{\rm Re}^{0.9}} \right) \right]^2}$$

$$\frac{\varepsilon}{D}$$


### Head Loss due to Sudden Expansion: Conservation of Energy
$$h_e = K_e \frac{V^2}{2g}$$

$$h_e = \frac{p_{in} - p_{out}}{\rho g} + \frac{V_{in}^2 - V_{out}^2}{2g}$$

Rearranged
$$\frac{p_{in} - p_{out}}{\rho g} = \frac{V_{out}^2 - V_{in}^2}{2g} + h_e$$


### Head loss due to Sudden Expansion: Conservation of Momentum
$$\bf{M_1 + M_2 = W + F_{p_1} + F_{p_2} + F_{ss}}$$

$$M_{in \, x} + M_{out \, x} = F_{p_{in \, x}} + F_{p_{out \, x}}$$

$$M_{1x} =  - \rho V_{in}^2 A_{in}$$

$$M_{2x} =  \rho V_{out}^2 A_{out}$$

$$ - \rho V_{in}^2 A_{in} + \rho V_{out}^2 A_{out} = p_{in} A_{out} - p_{out} A_{out}$$

$$\frac{p_{in} - p_{out}}{\rho g} = \frac{V_{out}^2 - V_{in}^2 \frac{A_{in}}{A_{out}}}{g}$$


### Head loss due to sudden expansion
$$h_e = \frac{p_{in} - p_{out}}{\rho g} + \frac{V_{in}^2 - V_{out}^2}{2g}$$

$$\frac{p_{in} - p_{out}}{\rho g} = \frac{V_{out}^2 - V_{in}^2 \frac{A_{in}}{A_{out}}}{g}$$

$$h_e = \frac{V_{out}^2 - V_{in}^2\frac{V_{out}}{V_{in}}}{g} + \frac{V_{in}^2 - V_{out}^2}{2g}$$

$$h_e = \frac{V_{out}^2 - 2 V_{in} V_{out} + V_{in}^2}{2g}$$
$$h_e = \frac{\left( V_{in}  - V_{out} \right)^2}{2g}$$
$${h_e} = \frac{V_{in}^2}{2g}{\left( {1 - \frac{A_{in}}{A_{out}}} \right)^2}$$

**Off-slide**
$$\begin{array}{l}
h_e = \frac{V_{in}^2}{2g}  \left( 1 -
\frac{A_{in}}{A_{out}} \right)^2
\\
\frac{A_{in}}{A_{out}} = \frac{V_{out}}{V_{in}}
\\
V_{in} = \frac{V_{out} A_{out}} {A_{in}}
\\
h_e = \frac{V_{out}^2}{2g}   \left( \frac{{{A_{out}}}}{{{A_{in}}}} - 1 \right)^2
\end{array}$$


### Minor Loss Coefficient for an Orifice in a Pipe ($D_{Orifice}$ < < $D_{pipe}$)
$$K_{e_{orifice}} = \left( \frac{A_{Pipe}}{\Pi_{vc} A_{Orifice}} - 1 \right)^2$$

$$K_{e_{orifice}} = \left( \frac{D_{Pipe}^2}{\Pi_{vc} D_{Orifice}^2} - 1 \right)^2$$


### Equation for the diameter of an orifice in a pipe given a headloss
$$h_e = \left( \frac{D_{Pipe}^2}{\Pi_{vc} D_{Orifice}^2} - 1 \right)^2 \frac{8Q^2}{g \pi^2 D_{Pipe}^4}$$


$$D_{Orifice} = \frac{D_{Pipe}} {\sqrt{\Pi_{vc} \left( \sqrt {\frac{h_e g}{8}} \frac{\pi D_{Pipe}^2}{Q} + 1 \right)} }$$


### Hole in a bucket doesn't give a constant flow rate
$$A_{vc} \cong 0.62 A_{or}$$

$$\Pi_{vc} \cong 0.62$$

$$Q = \Pi_{vc} A_{or} \sqrt{2g\Delta h}$$


### Use Conservation of Mass and Minor Loss equation
$$Q =  - \frac{d\rlap{--}V}{dt} = - \frac{{A_{Tank}}dh}{dt}$$

$$h_e = K_e \frac{Q^2}{2gA_{Valve}^2}$$

$$Q = A_{Valve} \sqrt{\frac{2 h_e g}{K_e}}$$

$$A_{Tank} \frac{dh}{dt} + A_{Valve} \sqrt{\frac{2gh}{K_e}} = 0$$


$$Q =  - \frac{d\rlap{--}V}{dt} = - \frac{{A_{Tank}}dh}{dt}$$


### Finding the chlorine depth as f(t)
$$\frac{ -A_{Tank}}{{A_{Valve}} \sqrt{\frac{2g}{K_e}} }   \int \limits_{h_0}^h \frac{dh}{\sqrt h} = \int \limits_0^t {dt}$$

$$\frac{ -A_{Tank}}{A_{Valve} \sqrt{ \frac{2g}{K_e}} } 2 \left( h^{1/2} - h_0^{1/2} \right) = t$$

$$\sqrt h  = \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{tank}} \sqrt {\frac{2g}{K_e}}$$


### Finding Q as f(t)
$$Q = A_{Valve} \sqrt{\frac{2g}{K_e}} \left( \sqrt{h_0}  - t \frac{A_{Valve}}{2 A_{tank}} \sqrt{\frac{2g}{K_e}} \right)$$

$$A_{Valve} = \frac{Q_{0}}{ \sqrt{ \frac{2 h_0 g}{K_e}} }$$

**Off-slide**
$$Q = \Pi_{vc} A_{or} \sqrt{2g} \left( \sqrt{h_0} - \frac{t \Pi_{vc}}{2} \frac{A_{or}}{A_{tank}} \sqrt{2g} \right)$$


### Surprise… Q and chlorine dose  decrease linearly with time!
$$Q = A_{Valve} \sqrt{ \frac{2g}{K_e} } \left( \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{Tank}} \sqrt{ \frac{2g}{K_e} } \right)$$

$$\frac{Q}{Q_0} = 1 - \frac{t Q_0}{2 A_{Tank} h_0}$$

$$Q_0 t_{Design} = A_{Tank} h_{Tank}$$

$$\frac{Q_0}{A_{Tank}} = \frac{h_{Tank}}{t_{Design}}$$

$$\frac{Q}{Q_0} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$$

$$\frac{C_{Cl_2}} {C_{Cl_{2_0}}} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$$


### Relfections
$$ \frac{Q}{Q_0} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$$

$$t = 2 t_{design}$$

$$\bar{Q} = \frac{Q_0}{2}$$


### Effect of tank height above Valve
$$h = \frac{Q^2}{Q_0^2} h_0$$


### A related tangent... Design a drain system for a tank
$$\sqrt h  = \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{tank}} \sqrt {\frac{2g}{K_e}}$$

$$A_{Valve} = \frac{\pi D_{Valve}^2}{4}$$

$$D_{Valve} = \sqrt{ \frac{8 L_{Tank} W_{Tank}}{\pi t_{Drain}}} {\left( \frac{K_{e} H_{Tank}}{2g} \right)^{\frac{1}{4}}}$$

**Off-slide**
$$A_{Valve} = \frac{2 A_{Tank}}{t_{Drain}}\sqrt {\frac{K_e h_0} {2g}}$$


### Constant Head: Float Valve
$$ d_{float}^2 \cdot{h_{submerged}} = d_{orifice}^2 \cdot{h_{tank}}$$

$$\frac{h_{tank}}{h_{submerged}} = \frac{d_{float}^2}{d_{orifice}^2}$$


### Float valve and small straight tube variable head
$$Q = \frac{h_{\rm{f}} g \pi D^4}{128\nu L}$$

$$h_L = z_{in} - z_{out}$$


### Design specificationsfor the float valve
$$A_{or} = \frac{Q}{ \Pi_{vc} \sqrt{2g\Delta h} }$$

$$D_{or} = \sqrt{\frac{4Q}{\pi \Pi_{vc} \sqrt{2g \Delta h} }}$$


### Nonlinearity Error Analysis: The problem of minor losses
$$h_e = \frac{8 Q^2}{g \pi^2 D^4} \sum{K_e}$$

$$h_{\rm{f}} = \frac{128\mu LQ}{\rho g\pi D^4}$$

$$h_L(Q) = \left( \frac{128\nu L}{g \pi D^4} + \frac{8Q}{g \pi ^2 D^4} \sum{K_e} \right) Q$$


### Relationship between Q and L given minor loss error constraints
$$\Pi_{Error} = \frac{h_{Linear} - h_L}{h_{Linear}} = 1 - \frac{h_L}{h_{Linear}}$$

$$1 - \Pi_{Error} = \frac{\left( \frac{128 \nu L}{g \pi D^4} + \frac{8Q}{g \pi^2 D^4} \sum{K_e} \right)}   {\left( \frac{128 \nu L}{g \pi D^4} + \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e} \right)}     =     \frac{\left( \frac{128 \nu L}{g \pi D^4} \right)}{\left( \frac{128 \nu L}{g \pi D^4} + \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e} \right)}$$

$$\left( 1 - \Pi_{Error} \right)  \frac{128 \nu L}{g \pi D^4} + \left( 1 - \Pi_{Error} \right) \frac{8 Q_{Max}}{g \pi ^2 D^4} \sum{K_e}  =  \frac{128 \nu L}{g \pi D^4}$$

$$- \Pi_{Error} \frac{128 \nu L}{g \pi D^4} + \left( 1 - \Pi_{Error} \right) \frac{8 Q_{Max}}{g \pi^2 D^4} \sum{K_e}  = 0$$

$$L = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{Q_{Max}}{16 \nu \pi} \sum{K_e}$$


### Relationship between Q and L given head loss error constraints
$$h_L = \left( \frac{128 \nu L Q_{Max}}{g \pi D^4} + \frac{8 Q_{Max}^2}{g \pi^2 D^4} \sum{K_e} \right)$$

$$L = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{Q_{Max}}{16 \nu \pi} \sum{K_e}$$

$$h_L = \left( \frac{8 \sum{K_e} }{g \pi^2 D^4} \left( \frac{1}{\Pi_{Error}} \right) \right) Q_{Max}^2$$

$$Q_{Max} = \frac{\pi D^2}{4} \sqrt{\frac{2 h_L g \Pi_{Error}}{\sum{K_e} }}$$

$$D = \left[ \frac{8K Q^2}{\Pi_{Error} h_l g \pi^2} \right]^{\frac{1}{4}}$$

$$V_{Max} = \sqrt{ \frac{2 h_L g \Pi_{Error}}{\sum{K_e} }}$$

**Off-slide**
$$L = \left( \frac{1 - \Pi_{Error}}{\Pi_{Error}} \right) \frac{1}{16 \nu \pi} \frac{\pi D^2}{4} \sum{K_e} \sqrt{ \frac{2 h_L g \Pi_{Error}}{\sum{K_e} }}$$

$$L = \frac{\left( 1 - \Pi_{Error} \right) D^2}{64 \nu} \sqrt{ \frac{2 h_L g \sum{K_e} }{\Pi_{Error}}}$$

$$D = \sqrt{ \frac{4 Q_{Max}}{\pi} \sqrt{ \frac{K}{2 h_L g \Pi_{Error}}}} $$


### Dosing Tube Lengths
$$L = \frac{\left( 1 - \Pi_{Error} \right) D^2}{64 \nu} \sqrt{ \frac{2 h_L g \sum{K_e}}{\Pi_{Error}} }$$

$$h_{L_{Max}} = \left( \frac{128 \nu L{Q_{Max}}}{g \pi D^4} + \frac{8 Q_{Max}^2}{g \pi^2 D^4} \sum{K_e} \right)$$

$$L = \left( \frac{g h_{L_{Max}} \pi D^4}{128 \nu Q_{Max}} - \frac{Q_{Max}}{16 \pi \nu} \sum{K_e} \right)$$


### Tube Diameter for Flow/Dose Controller (English tube sizes)
$${\rm Re}  = \frac{V D}{\nu}$$

$$V = \frac{4 Q}{\pi D^2}$$

$$D = \frac{4 Q_{\max}}{\pi \nu {\rm Re}_{\max}}$$

$$D = \left[ \frac{8 K Q^2}{\Pi_{Error} h_l g \pi^2} \right]^{\frac{1}{4}}$$

$$h_l = 20cm$$

$$\Pi_{Error} = 0.1$$


### Dose Controller Accuracy
$$\Delta h_{SubmergedFloat} = \frac{\Delta h_{StockTank}}{\frac{d_{Float}^2}{d_{Orifice}^2} \Pi_{Lever}}$$


### Maximum plant flow rate using linear flow controller
$$Q_C C_C = Q_P C_P$$

$$Q_P = Q_C \frac{C_C}{C_P}$$

$$Q_P = 0.0087 \frac{L}{s} \frac{\left( 160 \frac{g}{L} \right)}{\left( 0.03\frac{g}{L} \right)}$$

$$Q_P = 46 \frac{L}{s}$$



# **Extras!**
### Closed Conduit options for flow controllers
$$Q \propto h_f$$

$$Q \propto \sqrt{\frac{h_f}{f}}$$

$$Q \propto \sqrt {\Delta h}$$


### Open Channel Flow relationships
$$Q = \frac{2}{3} C_d W \sqrt{2g} H^{3/2}$$

$$Q = \frac{8}{15} C_d \sqrt{2g} \tan \left( \frac{\theta}{2} \right) H^{5/2}$$

$$Q = C_d W \sqrt{g} \left( \frac{2}{3} H \right)^{3/2}$$

$$Q = C_d W y_g \sqrt{2 g y_1}$$

$$V = \sqrt{2gH}$$


### Dose Controller with non-linear scale
$$\begin{array}{l}
Q_C = K_C h_C^{n_C}
\\
Q_P = K_P h_P^{n_P}
\\
C_P = \frac{C_C Q_C}{Q_P}
\\
C_P = \frac{C_C K_C h_C^{n_C}}{K_P h_P^{n_P}}
\\
h_C = K_L h_P
\\
C_P = \frac{C_C K_C K_L^{n_C} h_P^{n_C}}{K_P h_P^{n_P}}
\end{array}$$


### Constant dose with changing plant requirements
$$C_P = \frac{C_C K_C K_L^{n_C} h_P^{n_C}}{K_P h_P^{n_P}}$$

$$C_P \propto \frac{K_L^{n_C} h_P^{n_C}}{h_P^{n_P}}$$

$$Q_P = K_P h_P^{n_P}$$

**Off-slide**
$$n_P = n_C$$


### Dose scale on the lever arm?
$$C_P = \sqrt{K_L} \frac{C_C K_C}{K_P}$$

$$\sqrt{K_L} \propto C_P$$


### Surface Tension
$$F_g = \frac{4 \pi r^3}{3 \cdot 2}\rho g$$

$$\frac{4 \pi r^3}{3 \cdot 2} \rho g + \rho g \Delta h \left( \pi r^2 \right) = 2 \pi r \sigma$$

$$\rho g \Delta h \left( \pi r^2 \right)$$


### Surface Tension can prevent flow!
$$\Delta h = \frac{2 \pi r \sigma - \frac{4 \pi r^3}{3 \cdot 2} \rho g}{\rho g \left( \pi r^2 \right)}$$

$$\Delta h = \frac{2 \sigma}{\rho g r} - \frac{2r}{3}$$


### Kinematic Viscosity of Coagulants
$$\nu_{Alum} = \left[ 1 + 4.225 \times {10}^{-6}\left( \frac{C_{Alum}}{\frac{kg}{m^3}} \right)^{2.289} \right] \nu_{{H_2}O}$$

$$\nu_{PACl} = \left[ 1 + 2.383 \times {10}^{-5}\left(\frac{C_{PACl}}{\frac{kg}{m^3}} \right)^{1.893} \right] \nu_{{H_2}O}$$


### Porous Media Head Loss: Kozeny equation
$$V_{pore} = \frac{V_a}{\varepsilon}$$

$$h_{\rm{f}} \approx \frac{32 \mu L V_{pore}}{\rho g d_{pore}^2}$$

$$\nu  = \frac{\mu}{\rho}$$

$$\frac{h_{\rm{f}}}{L} = 36k \frac{\left( 1 - \varepsilon \right)^2}{\varepsilon^3} \frac{\nu V_a}{g d_{sand}^2}$$


### Float Valve head loss
$$D_{or} = \sqrt{ \frac{4Q}{\pi \Pi_{vc} \sqrt{ 2 g \Delta h} }}$$

$$D_{or} = \sqrt{ \frac{4 \left( 0.0000075 \frac{m^3}{s} \right)}{\pi \left( 0.62 \right) \sqrt{2 \left( 9.8 \frac{m}{s^2} \right) \left( 0.3m \right)} }}  = 2.5mm$$
