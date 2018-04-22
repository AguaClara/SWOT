# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


# **Filtration**
### Net Velocity Concept for estimating plant size
$$A_{Dynamic} = \frac{Q}{V_{Dynamic}}$$

$$A_{Total} = \frac{Q}{V_{Dynamic}} + \frac{Q}{V_{Rough}} + \frac{Q}{V_{Slow}}$$

$$V_{Total} = \frac{Q}{A_{Total}}$$

$$V_{Total} = \frac{1}{\frac{1}{V_{Dynamic}} + \frac{1}{V_{Rough}} + \frac{1}{V_{Slow}}}$$


### Porosity
$$\phi_{FiSand} = \frac{\rlap{-} V_{voids}}{\rlap{-} V_{total}}$$


### Expanded Bed Porosity
$$\Pi_{FiBw} = \frac{H_{FiSandBw}}{H_{FiSand}}$$

$$\phi_{FiSandBw} =
\frac{\phi_{FiSand} H_{FiSand} A_{Fi} + \left( H_{FiSandBw} - H_{FiSand} \right) A_{Fi}}
{H_{FiSandBw} A_{Fi}}$$

$$\phi_{FiSandBw} = 1 - \frac{1 - \phi_{FiSand}}{\Pi_{FiBw}}$$

$$\Pi_{FiBw} = \frac{1 - \phi_{FiSand}}{1 - \phi_{FiSandBw}}$$


### Clean Bed Head Loss (Karmen Kozeny)
$$\frac{h_{\rm f}}{L} = \frac{32 \nu V}{g D^2}$$

$$\frac{h_l}{H_{FiSand}} = 36 k \frac{\left( 1 - \phi_{FiSand} \right)^2}{\phi_{FiSand}^3} \frac{\nu V_{Fi}}{g D_{60}^2}$$

$${\rm Re}  = \frac{D_{60} V_{Fi}}{\nu}$$


### Backwash Requirements – Head Loss (force balance)
$$P_{Manometer} = \rho_{Water} g
\left( H_{W_1} + H_{W_2} + \phi_{FiSand} H_{FiSand} \right)
+ \rho_{Sand} g \left( 1 - \phi_{FiSand} \right) H_{FiSand}$$

$$P_{Manometer} = \rho_{Water} g
\left( H_{W_1} + H_{W_2} + H_{FiSand} + h_{l_{FiBw}} \right)$$

$$h_{l_{FiBw}} = H_{FiSand}
\left( 1 - \phi_{FiSand} \right)
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right)$$

$$h_{l_{FiBw}}$$

$$H_{W_1}$$

$$H_{Manometer}$$

$$H_{FiSand}$$

$$H_{W_2}$$

$$\left( 1- \Phi_{FiSand} \right)
\left( \frac{\rho_{FiSand}}{\rho_{Water}} - 1 \right) = 0.99$$

**Off-slide**
$$\begin{array}{l}
\rho_{Water} g \left( H_{W_1} + H_{W_2} + H_{FiSand} + HL_{FiBw} \right)
= \rho_{Water} g \left( H_{W_1} + H_{W_2} + \varepsilon H_{FiSand} \right) +
\left( 1 - \varepsilon \right) H_{FiSand} \rho_{Sand} g
\\
HL_{FiBw} = \left( \varepsilon - 1 \right) H_{FiSand} +
\left( 1 - \varepsilon \right) H_{FiSand} \frac{\rho_{Sand}}{\rho_{Water}}
\\
HL_{FiBw} = H_{FiSand} \left( 1 - \varepsilon \right)
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right)
\end{array}$$

$$h_{l_{FiBw}} \rho_{Water} = H_{FiSand}
\left( 1 - \varepsilon_{FiSand} \right)
\left( \rho_{Sand} - \rho_{Water} \right)$$

$$\begin{array}{l}
\rho_{Water} g \left( H_{W_1} + H_{W_2} + H_{FiSand} + h_{l_{FiBw}} \right) =
\rho_{Water} g \left( H_{W_1} + H_{W_2} + \phi_{FiSand} H_{FiSand} \right) +
\rho_{Sand} g \left( 1 - \phi_{FiSand} \right) H_{FiSand}
\\
h_{l_{FiBw}} = \frac{\rho_{Sand} - \rho_{Water}}{\rho_{Water}} \left( 1 - \phi_{FiSand} \right) H_{FiSand}
\end{array}$$


### Backwash Requirements – Flow Rate
$$\frac{h_l}{H_{FiSand}} = 36 k \frac{\left( 1 - \phi_{FiSand} \right)^2}{\phi_{FiSand}^3} \frac{\nu V_{Fi}}{g D_{60}^2}$$

$$\frac{h_{l_{FiBw}}}{H_{FiSand}} =
\left( 1 - \phi_{FiSand} \right)
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right)$$

$$\left( 1 - \phi_{FiSand} \right)
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right) =
36 k \frac{\left( 1 - \phi_{FiSand} \right)^2}{\phi_{FiSand}^3} \frac{\nu V_{MinFluidization}}{g D_{60}^2}$$

$$V_{MinFluidization} = \frac{\phi_{FiSand}^3 g D_{60}^2}{36 k \nu \left( 1 - \phi_{FiSand} \right)}
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right)$$


### Backwash Velocity
$$V_{Bw} = \frac{\phi_{FiSandBw}^3 g D_{60}^2}{36 k \nu \left( 1 - \phi_{FiSandBw} \right)}
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right)$$

$$\phi_{FiSandBw} = 1 - \frac{1 - \phi_{FiSand}}{\Pi_{FiBw}}$$

**Off-slide**
$$V_{MinFluidization} = \Pi_{FiExpansion}
\frac{ \left( \frac{\varepsilon_{FiSand} - 1}{\Pi_{FiExpansion}} + 1 \right)^3
g D_{Sand}^2}
{36 k \nu \left( 1 - \varepsilon_{FiSand} \right)}
\left( \frac{\rho_{Sand}}{\rho_{Water}} - 1 \right)$$


### The Low Flow Challenge: Filter Set
$$\begin{array}{l}
Q_{Plant} = 6 \, {\rm \frac{L}{s}}
\\
V_{Fi} = 1.8 \, {\rm\frac{mm}{s}}
\\
V_{Bw} = 9 \, {\rm \frac{mm}{s}}
\\
N_{Fi} = \frac{V_{Bw}}{V_{Fi}} + 1 = 6
\\
A_{FiTotal} = \frac{Q_{Plant}}{V_{Fi}} \cdot \frac{N_{Fi}}{N_{Fi} - 1} =
4 \, {\rm m^2}
\\
A_{Fi} = \frac{A_{FiTotal}}{N_{Fi}} = {\rm 0.667 \, m^2}
\\
W_{Fi} = \sqrt{A_{Fi}} = 0.816 \, {\rm m^2}
\end{array}$$


### Store filter water?
$$\begin{array}{l}
Q_{Plant} = 6 \, {\rm \frac{L}{s}} \, \, \, \, \, \, V_{Fi} =
1.8 \, {\rm \frac{mm}{s}}
\\
V_{Bw} = 9 \, {\rm \frac{mm}{s}} \, \, \, \, \, \, Ti_{Bw} = 20 \, {\rm min}
\\
N_{Fi} = 2 \, \, \, \, \, \,  {\rm Assume \, \, 2 \, \, filters}
\\
A_{Fi} = \frac{Q_{Plant}}{V_{Fi} \cdot N_{Fi}} = 1.7 \, {\rm m^2}
\\
\rlap{-} V_{Bw} = T_{Bw} V_{Bw} A_{Fi} = 18 \, {\rm m^2}
\\
T_{FillTank} = \frac{\rlap{-} V_{Bw}}{Q_{Plant}} 0.83 \, {\rm hr}
\\
H_{Tank} = 1 \, {\rm m}
\\
V_{Tank} = \frac{H_{Tank}}{T_{FillTank}} = 0.33 \, {\rm \frac{mm}{s}}
\end{array}$$


### End Backwash cycle
$$\Pi_{FiBw} H_{FiSand}$$


### Head loss between manifolds: Assume expansion ratio of 1.3
$$\Pi_{FiBw} = \frac{H_{FiSandBw}}{H_{FiSand}}$$

$$H_{FiSand} = \frac{H_{FiSandBw}}{\Pi_{FiBw}}$$

$$ = 15.4 \, {\rm cm}$$



## Post-Refernces
### What is the Reynolds number for filtration flow?
$${\rm Re} = \frac{V l}{\nu}$$

$${\rm Re} = \frac{\left( 2.8 \cdot 10^{- 3} {\rm \frac{m}{s}} \right)
\left( 0.7 \cdot 10^{- 3} \, {\rm m} \right)}
{\left( 10^{- 6} {\rm \frac{m^2}{s}} \right)} = 2$$


### Dimensionless Force Ratios
$${\rm f}_i = \rho \frac{V^2}{l} $$

$${\rm Re} = \frac{\rho V l}{\mu}$$

$${\rm f}_u = \mu \frac{V}{l^2}$$

$${\rm Fr} = \frac{V}{\sqrt{g l}}$$

$${\rm f}_g = \rho g$$

$$W = \frac{V^2 l \rho}{\sigma}$$

$${\rm f}_\sigma = \frac{\sigma}{l^2}$$

$$M = \frac{V}{c}$$

$${\rm f}_{E_v} = \frac{\rho c^2}{l}$$

$$\left( \Delta p + \rho g \Delta z \right)$$

$${\rm C}_p = \frac{- 2 \left( \Delta p \right)}{\rho V^2}$$


### Gravity
$$v_{\rm g} = \frac{\left( \rho_p - \rho_w \right) g D_P^2}{18 \mu}$$

$$\Pi_{\rm g} = \frac{f_g}{f_\mu}$$

$$\Pi_{\rm g} = \frac{v_g}{V_0}$$

$$\Pi_{\rm g} = \frac{\Delta \rho g}{\mu \frac{V_{Fi}}{D_P^2}}$$

$$\Pi_{\rm g} = \frac{\left( \rho_p - \rho_w \right) g D_P^2}{18 \mu V_{Fi}}$$

$$\Pi_{\rm g} = \frac{\left( \rho_p - \rho_w \right) g D_P^2}{\mu V_{Fi}}$$


### Diffusion (Brownian Motion)
$$v_{Diffusion} \propto \frac{D_{Molecular}}{d_c}$$

$$D_{Molecular} = \frac{k_B T}{3 \pi \mu d_p} \left[ \frac{L^2}{T} \right]$$

$${\rm f}_u = \mu \frac{V}{l^2}$$

$$\Pi_{\rm Br} = \frac{k_B T}{3 \pi \mu d_P V_{Fi} d_c}$$


### Geometric Parameters
$$\Pi_z (z,d_c) = \frac{3 (1 - \phi_{Por})}{2 \ln(10)} \left( \frac{z}{d_c} \right)$$

$$\Pi_R = \frac{d_p}{d_c}$$

$$\Pi_z = \frac{z}{d_c}$$


### Write the functional relationship
$$pC^\ast = \alpha f \left( \Pi_R, \Pi_z, \phi, \Pi_{\rm g}, \Pi_{\rm Br} \right)$$

$$pC^\ast = \alpha \Pi_z f \left( \Pi_R, \phi, \Pi_{\rm g}, \Pi_{\rm Br} \right)$$


### Stacked Rapid Sand Filter predicted performance for biological particle
$$\begin{array}{l}
\rho_p = 1040 \, {\rm \frac{kg}{m^3}}
\\
V_a = 1.8 \, {\rm \frac{mm}{s}}
\\
T = 293 {\rm K}
\\
z = 20 {\rm cm}
\\
d_c = 0.5 {\rm mm}
\\
\alpha = 1
\\
\phi = 0.4
\end{array}$$


### Filter as Flocculator?
$$\bar G \theta = \sqrt{ \frac{g h_e \theta}{\nu} }$$


### Small particles slip through a small restriction
$$C_{Pore}^\ast = \left( \frac{D_C - D_P}{D_C} \right)^2$$


### A series of restrictions takes a toll on even the small particles
$$C_{Filter}^\ast = \left( \frac{D_C - D_P}{D_C} \right)^{2 N_{Pores}}$$

$$N_{Pores} = \frac{\ln(C_{Filter}^\ast)}{2 \ln\left( \frac{D_C - D_P}{D_C} \right)}$$


### Filtration of mixed particle sizes
$$pC_i^\ast = \alpha \Pi_z f( d_i)$$

$$C_i = C_{0_i} 10^{- pC_i^\ast}$$

$$C_i = C_{0_i} \cdot 10^{- \alpha \Pi_z f( d_i)}$$

$$pC^\ast = - \log
\left( \frac{\sum \limits_{i = 0}^n {C_i} }{\sum \limits_{i = 0}^n {C_{0_i}} } \right)$$


### Interception
$$C_{Pore}^\ast = \frac{\frac{\pi}{4} \left( D_C - D_P \right)^2}{\frac{\pi}{4} D_C^2}$$

$$C_{Pore}^\ast = \left( \frac{D_C - D_P}{D_C} \right)^2$$

**Off-slide**
$$\frac{\frac{\pi}{4} D_C^2 - \frac{\pi}{4} \left( D_C^2 - 2 D_C D_P + D_P^2 \right)}{\frac{\pi}{4} D_C^2}$$


### Flocculation may be a significant mechanism inside a filter
$$\begin{array}{l}
h_{\rm f} = \frac{32 \mu \theta V^2}{\rho g D^2}
\\
\bar \varepsilon = \frac{g h_f}{\theta}
\\
\bar G = \sqrt{ \frac{\bar \varepsilon}{\nu} }
\\
\theta = \frac{L}{V}
\\
\bar G = 4 \sqrt 2 \frac{V}{D}
\\
\bar G \theta  = 4 \sqrt 2 \frac{L}{D}
\end{array}$$

$$\frac{20 \, {\rm cm}}{0.2 \, {\rm mm}} 4 \sqrt{2} = 0.5657$$


### Siphon Geometry for Air trap
$$P \rlap{-} V = n R T$$

$$P_0 \rlap{-} V_0 = P_1 \rlap{-} V_1$$

$$\begin{array}{l}
\rlap{-} V_0 = \left( L1_0 + L2 + L3_0 \right) A_{Siphon}
\\
\rlap{-} V_0 = \left( H_2 - H_3 - HL_{Siphon} + L2 + H_2 - H_3 \right) A_{Siphon}
\\
\rlap{-} V_0 = \left( 2 H_2 - 2 H_3 - HL_{Siphon} + L2 \right) A_{Siphon}
\\
\rlap{-} V_1 = \left( H_1 - H_3 + L2 + H_1 + H_2 - H_3 \right) A_{Siphon}
\\
\rlap{-} V_1 = \left( 2 H_1 - 2 H_3 + L2 + H_2 \right) A_{Siphon}
\end{array}$$

$$\rlap{-} V_1 = \frac{P_0 \rlap{-} V_0}{P_1}$$

$$P_0 = 1 \, {\rm atm} $$

$$P_1 = P_{atm} + \rho g H_1$$

$$\left( 2 H_1 - 2 H_3 + L2 + H_2 \right) =
\frac{P_{atm} \left(2 H_2 - 2 H_3 - HL_{Siphon} + L2 \right)}{P_{atm} + \rho g H_1}$$

**Off-slide**
$$H_1 - L1_1 + L3_1 - H_1 = H_2$$

$$ - L1_1 + L3_1 = H_2$$

$$L3_1 = H_2 + L1_1$$


### Maximum water level that can be held by siphon
$$\left( L2 + H_2 \right) =
\frac{P_{atm} \left( 2 H_2 - 2 H_3 - HL_{Siphon} + L2 \right)}{P_{atm} + \rho g H_3}$$

$$H_3 = \frac{\left( H_2 - HL_{Siphon} \right) P_{atm}}{\rho g \left( L2 + H_2 \right) + 2 P_{atm}}$$

**Off-slide**
$$\begin{array}{l}
\left( L2 + H_2 \right) \left( P_{atm} + \rho g H_3 \right) =
P_{atm} \left( 2 H_2 - 2 H_3 - HL_{Siphon} + L2 \right)
\\
L2 \, P_{atm} + H_2 P_{atm} + \rho g H_3 L2 + \rho g H_3 H_2 = 2 H_2 P_{atm} - 2 H_3 P_{atm} - HL_{Siphon} P_{atm} + L2 \, P_{atm}
\\
\rho g H_3 L2 + \rho g H_3 H_2 + 2 H_3 P_{atm} = 2 H_2 P_{atm} - HL_{Siphon} P_{atm} + L2 \, P_{atm} - L2 \, P_{atm} - H_2 P_{atm}
\\
H_3 = \frac{\left( H_2 - HL_{Siphon} \right) P_{atm}}
{\rho g \left( L2 + H_2 \right) + 2 P_{atm}}
\end{array}$$

$$H_3 = \frac{\left( H_2 - HL_{Siphon} \right)}{\frac{\rho g \left( L2 + H_2 \right)}{P_{atm}} + 2} = \frac{\left( H_2 - HL_{Siphon} \right) P_{atm}} {\rho g \left( L2 + H_2 \right) + 2 P_{atm}}$$
