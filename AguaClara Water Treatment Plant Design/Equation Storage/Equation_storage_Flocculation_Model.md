# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


### Change Font color on: `Overview`, `Use dimensional analysis to get a relative velocity`, `We can test the collision models with laboratory data`, `Floc model for viscous dominated collisions`, `Fractal Floc Conclusions`, and `Review`


# **Flocculation Model**
### Overview
$$pC^\ast = \frac{3}{2} \log \left( \frac{2}{3} \pi k \frac{d_P^2}{\Lambda_0^2} Gt \alpha + 1 \right)$$


### Recommended G and Gq values: Turbidity or Color Removal (Mechanical flocculators)
$$\varepsilon  = \nu {G^2}$$

$$\left[ \frac{mW}{kg} \right]$$

$$G = \sqrt{ \frac{\varepsilon}{\nu} }$$


### Mechanical Design: Mixing with Paddles
$$G = \sqrt \frac{C_D A_P a^3 V_{pa}^3}{2 \rlap{-} V \nu} $$

$$C_D \approx 1.9$$


### Mechaical Flocculators and Energy Dissipation Rate
$$\varepsilon_{Max} \cong \frac{ \left( \Pi_{Plate} V \right)^3}{W_{Plate}}$$


### CFD Analysis
$$\Pi_{Plate} = \frac{ \left( \varepsilon_{Max} W_{Plate} \right)^\frac{1}{3}}{V}$$


### Schulz and Okun (Hydraulic flocculators)
**Off-slide**
$$0.45 \, {\rm m} \cdot 0.45 \, {\rm m} \cdot 0.3 {\rm \frac{m}{s}} = 60.75 \, {\rm \frac{L}{s}}$$


### It requires many sequential doubling collisions to make a big floc
$$\log (1,000,000,000) = n \log(2)$$

$$n = \frac{\log(1,000,000,000)}{\log(2)}$$


### Fractals capture the idea that volume isn't conserved
$$d = d_0 i^\frac{1}{D_{Fractal}}$$

$$\rlap{-} V = \rlap{-} V_0 i^\frac{3}{D_{Fractal}}$$


### Buoyant Density of Flocs
$$\rho_{Floc} - \rho_{H_2O} = \left( \rho_{Floc_0} - \rho_{H_2O} \right) \left( \frac{d_0}{d} \right)^{3 - D_{Fractal}}$$


### Fractal Terminal Velocity Equations
$$V_t = \frac{g d^2}{18 \nu_{H_2O}}
\frac{\rho_{Floc} - \rho_{H_2O}}{\rho_{H_2O}}$$

$$V_t = \frac{g d^2}{18 \nu_{H_2O}}
\frac{ \left( \rho_{Floc_0} - \rho_{H_2O} \right) }{\rho_{H_2O}}
\left( \frac{d_0}{d} \right)^{3 - D_{Fractal}}$$

$$V_t = \frac{g d^2}{18 \nu_{H_2O}}
\left( \frac{d_0}{d} \right)^2
\frac{ \left( \rho_{Floc} - \rho_{H_2O} \right) }{\rho_{H_2O}}
\left( \frac{d}{d_0} \right)^2
\left( \frac{d}{d_0} \right)^{D_{Fractal} -3 }$$


$$V_t = \frac{g d_0}{18 \nu_{H_2O}}
\frac{ \left( \rho_{Floc_0} - \rho_{H_2O} \right)}{\rho_{H_2O}}
\left( \frac{d}{d_0} \right)^{D_{Fractal} - 1}$$


### Floc Terminal Velocity
$$V_t = \frac{g d_0}{18 \Phi \nu_{H_2O}}
\frac{ \rho_{Floc_0} - \rho_{H_2O}}{\rho_{H_2O}}
\left( \frac{d}{d_0} \right)^{D_{Fractal} - 1}$$


### Average distance between particles is the cube root of the volume occupied ($\Lambda$)
$$\rlap{-} V_P = \frac{\pi}{6} d_P^3$$

$$n_P = \frac{C_P}{\rlap{-} V_P \rho_P} = \frac{6}{\pi d_P^3} \frac{C_P}{\rho_P}$$

$$\Lambda  = \frac{1}{n_P^{\frac{1}{3}}}$$

$$\Lambda  = d_P \left( \frac{\pi }{6} \frac{\rho_P}{C_P} \right)^{\frac{1}{3}}$$

$$n_P = n_{P_0} \left( \frac{d_0}{d_P} \right)^{D_{Fractal}}$$

**Off-slide**
$$\phi_{Floc} = \phi_{Floc_0} \left( \frac{d}{d_0} \right)^{3 - D_{Fractal}}$$

$$\begin{array}{l}
n_{Floc} = \frac{C_{Floc}}{\rlap{-} V_{Floc} \rho_{Floc}} = \frac{\phi_{Floc}}{\rlap{-} V_{Floc}}
\\
n_{Floc_0} = \frac{\phi_{Floc_0}}{\rlap{-} V_{Floc_0}}
\\
n_{Floc} = \frac{\phi_{Floc}}{\rlap{-} V_{Floc}} = \frac{\phi_{Floc_0} \left( \frac{d_{Floc}}{d_0} \right)^{3 - D_{Fractal}}}{\rlap{-} V_{Floc}}
\\
= n_{Floc_0} \frac{\rlap{-} V_{Floc_0} \left( \frac{d_{Floc}}{d_0} \right)^{3 - D_{Fractal}}}{ \rlap{-} V_{Floc}}
\\
= n_{Floc_0} \left( \frac{d_0}{d_{Floc}} \right)^3 \left( \frac{d_{Floc}}{d_0} \right)^{3 - {D_{Fractal}}}
\\
n_{Floc} = n_{Floc_0} \left( \frac{d_0}{d_{Floc}} \right)^{D_{Fractal}}
\end{array}$$


### Comparison of classic and hypothesized collision models
$$v_r \approx d_P \bar G$$

$$v_r \approx \Lambda \bar G$$


### Proposed ($\Lambda$) Long Range Transport Hypothesis*
$$\frac{\Lambda}{d_{Floc} G} - \frac{dt}{2}$$

$$\frac{\Lambda}{d_{Floc} G} + \frac{dt}{2}$$

$$\frac{\Lambda}{d_{Floc} G}$$


### How much water is cleared (filtered) from a floc’s perspective?
$$ \propto \pi d_P^2$$

$$ \propto t$$

$$ \propto v_r$$

$$v_r t$$

$$\pi d_P^2$$

$$\rlap{-} V_{\rm{Cleared}} \propto \pi d_P^2 v_r t$$


### Use dimensional analysis to get a relative velocity
$$\Lambda  = \frac{1}{n_P^{\frac{1}{3}}}$$

$$v_r = f \left( \varepsilon ,\nu ,\Lambda \right)$$

$$v_r = f \left( \varepsilon ,\nu ,d_p \right)$$

$$v_r = \Lambda f \left( \varepsilon ,\nu \right)$$

$$v_r = d_p f \left( \varepsilon ,\nu \right)$$

$$v_r \approx \Lambda \sqrt{ \frac{\varepsilon}{\nu} }$$

$$v_r \approx d_p \sqrt{ \frac{\varepsilon}{\nu} }$$

$$v_r \approx \Lambda G$$

$$v_r \approx d_p G$$

$$\Lambda = \rm{ \left[ L \right]
\, \, \, \, \,
\varepsilon = \left[ \frac{L^2}{T^3} \right]
\, \, \, \, \,
\nu  = \left[ \frac{L^2}{T} \right] }$$

**Off-slide**
$$\lambda_v = \Pi_{kv} \eta_K$$

$$\Pi_{kv} = 50$$


### Collision rates for the two assumptions
$$\rlap{-} V_{Occupied} = \Lambda^3$$

$$t_c = \frac{\Lambda^2}{{\pi d_P^2G}}$$

$$t_c = \frac{\Lambda^3}{\pi d_P^3 G}$$

$$dN_c = \frac{\alpha}{t_c} dt$$

$$dN_c = \pi \frac{d_P^2}{\Lambda^2} G \alpha dt$$

$$dN_c = \pi \frac{d_P^3}{\Lambda^3} G \alpha dt$$


### Collision Rate and Particle Removal
$$v_r \approx \Lambda \bar G$$

$$v_r \approx d_p \bar G$$

$$dN_c = \pi d_P^2 n_P^\frac{2}{3} \bar G \alpha dt$$

$$dN_c = \pi d_P^3 n_P \bar G \alpha dt$$

$$\frac{dn_P}{dN_c} =  - k n_P$$

$$\frac{dn_P}{- kn_P} = \pi d_P^2 n_P^\frac{2}{3} \bar G \alpha dt$$

$$\frac{dn_P}{- kn_P} = \pi d_P^3 n_P \bar G \alpha dt$$

**Off-slide**
$$dN_c = \pi d_T^2n_T^\frac{1}{3} G \Gamma dt$$

$$\frac{dn_S}{dN_c} =  - k n_T$$

$$dn_S =  - k n_T \pi d_T^2 n_T^\frac{2}{3} G \Gamma dt$$


### Integrate
$$n_P = \frac{6}{\pi d_P^3} \frac{C_P}{\rho_P}$$

$$\int \limits_{n_{P_0}}^{n_P} n_P^{- \frac{5}{3}} dn_P  
= - k \pi d_P^2 \bar G \alpha \int \limits_0^t dt $$

$$\int \limits_{n_{P_0}}^{n_P} n_P^{- 2} dn_P
= - \pi k d_P^3 \bar G \alpha \int \limits_0^t dt $$

$$- \frac{3}{2} \left( n_P^{- \frac{2}{3}} - n_{P_0}^{ - \frac{2}{3}} \right) =  - k \pi d_P^2 \bar Gt \alpha$$

$$\frac{1}{n_P} - \frac{1}{n_{P_0}} = \pi k d_P^3 \bar Gt \alpha$$

$$pC^\ast = p \left( \frac{n_P}{n_{P_0}} \right) = \frac{3}{2} \log \left( \frac{2}{3} \pi k d_P^2 n_{P_0}^\frac{2}{3} \bar Gt \alpha + 1 \right)$$

$$pC^\ast = p \left( \frac{n_P}{n_{P_0}} \right) = \log \left( \pi k d_P^3 n_{P_0} \bar Gt \alpha  + 1 \right)$$

$$n_{P_0} = \frac{6}{\pi d_P^3} \phi_0$$

**Off-slide: left**
$$\frac{3}{2} \left( \Lambda^2 - \Lambda_0^2 \right) = k \pi d_P^2 Gt \Gamma$$

$$1 = k \frac{2\pi}{3} \left( \frac{6}{\pi} \right)^\frac{2}{3} Gt \Gamma \left( \frac{C_P}{\rho_P} \right)^\frac{2}{3}$$

$$pC^\ast = \frac{3}{2} \log \left( \frac{2}{3} 6^\frac{2}{3} \pi ^\frac{1}{3} k \phi_0^\frac{2}{3} Gt \Gamma + 1 \right)$$

**Off-slide: right**
$$dn_S =  - k n_T \pi d_T^2 n_T^\frac{2}{3} G \Gamma dt$$

$$\int \limits_{n_{S_{in}}}^{n_{S_{out}}} dn_S  
= - k \pi d_T^2 n_T^\frac{5}{3}  G \Gamma \int \limits_0^t dt$$

$$n_{S_{out}} = n_{S_{in}} - k \pi d_T^2 n_T^\frac{5}{3} Gt \Gamma$$

$$\frac{n_{S_{out}}}{n_{S_{in}}} = 1 - \frac{n_T}{n_{S_{in}}} k \pi d_T^2 n_T^\frac{2}{3} Gt \Gamma$$

$$n_T = \frac{6}{\pi d_T^3} \frac{C_T}{\rho_T}$$

$$\frac{n_{S_{out}}}{n_{S_{in}}} = 1 - \frac{n_T}{n_{S_{in}}} k \pi \left( \frac{6}{\pi} \right)^\frac{2}{3} \left( \frac{C_T}{\rho_T} \right)^\frac{2}{3} Gt \Gamma$$

$$\begin{array}{l}
\left[ \frac{\left[ {\rm{\bar G}}\left( d_{P1} + d_{P2} \right) \right]_{Max}} {V_C} \right]^n
\\
\Delta V_{Surfac{e_{Max}}} = \left[ {\rm{\bar G}} \left( d_{P1} + d_{P2} \right) \right]_{Max}
\\
\alpha = \frac{\Delta V_{Surfac{e_{Max}}}} {\rm{\bar G} D_c}
\end{array}$$

**Off-slide: bottom**
$$\frac{n_{P_0}}{n_P} = \pi k d_P^3 n_{P_0} G \Gamma t + 1$$

$$\frac{G_{Max}}{\rm{\bar G}}$$


### We can test the collision models with laboratory data
$$pC^\ast = \frac{3}{2} \log \left( \frac{2}{3} \pi k \frac{d_P^2}{\Lambda_0^2} Gt \alpha + 1 \right)$$

$$pC^\ast = \frac{3}{2} \log \left( \frac{2}{3} \pi k \frac{d_P^3}{\Lambda_0^3} Gt \alpha + 1 \right)$$

$$\Lambda  = \frac{1}{n_P^\frac{1}{3}}$$

$$pC^\ast = f \left( \frac{d_P^2}{\Lambda_0^2} \bar Gt \alpha \right)$$

$$pC^\ast = f \left( \frac{d_P^3}{\Lambda_0^3} \bar Gt \alpha \right)$$

$$\frac{d_P^2}{\Lambda_0^2} \bar Gt \alpha$$

$$\frac{d_P^3}{\Lambda_0^3} \bar Gt \alpha$$


### Floc model for viscous dominated collisions
$$pC^\ast = \frac{3}{2} \log \left( \frac{2}{3} \pi k \frac{d_P^2}{\Lambda_0^2} Gt \alpha + 1 \right)$$

$$\bar Gt = \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_{Clay}^2 \alpha}$$

$$\left( \frac{\varepsilon}{\nu} \right)^\frac{1}{2}$$


### Model predictions?
$$- \frac{3}{2} \left( \Lambda^2 - \Lambda_0^2 \right) = - k \pi d_P^2 \bar Gt \alpha$$

$$\Lambda^3 - \Lambda_0^3 = \pi k d_P^3 \bar Gt \alpha$$

$$\bar Gt = \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_P^2 \alpha}$$

$$\bar Gt = \frac{\left( \Lambda^3 - \Lambda_0^3 \right)}{k \pi d_P^3 \alpha}$$

$$\Lambda  \gg \Lambda_0$$

$$\bar Gt \approx \frac{3}{2} \frac{\Lambda^2}{k \pi d_P^2 \alpha}$$

$$\bar Gt \approx \frac{\Lambda^3}{k \pi d_P^3 \alpha}$$

**Off-slide**
$$\begin{array}{l}
Gt_{v_r \approx d_P G}
= \frac{\Lambda^3 - \Lambda_0^3}{k \pi d_P^3 \Gamma}
\\ \\
Gt_{v_r \approx \Lambda G}
= \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_P^2 \Gamma}
\\ \\
\frac{Gt_{v_r \approx d_P G}}{Gt_{v_r \approx \Lambda G}}
= \frac{2}{3d_P} \frac{\Lambda^3 - \Lambda_0^3}{\Lambda^2 - \Lambda_0^2}
\\ \\
\frac{Gt_{v_r \approx d_P G}}{Gt_{v_r \approx \Lambda G}}
= \frac{2}{3d_P} \frac{\Lambda^3 - \Lambda_0^3}{\Lambda ^2 - \Lambda_0^2}
\end{array}$$


### The classic: "Click to add a title"
$$\bar Gt \approx \frac{3}{2} \frac{\Lambda^2}{k \pi d_P^2 \alpha}$$

$$\Lambda  = \frac{1}{n_P^\frac{1}{3}}$$

$$\Lambda^2 = \frac{2}{3} \pi k \bar Gt d_P^2 \alpha$$

$$n_P = \frac{6}{\pi d_P^3} \frac{C_P}{\rho_P}$$

$$C_P = \frac{ \left( {\frac{\pi}{6}{\rho_P}} \right)}{\left( \frac{2}{3} \pi k \bar Gt \alpha \right)^\frac{3}{2}}$$

$$\Lambda = \left( \frac{\pi d_P^3}{6} \frac{\rho_P}{C_P} \right)^\frac{1}{3}$$


### Track surface area to assign probabilities to collisions
$$\Gamma_{CoagClay}$$

$$\Gamma_{HACoag}$$

$$1-\Gamma_{CoagClay}$$

$$\Gamma_{CoagClay}\left ( 1-\Gamma_{HACoag} \right )$$

$$\Gamma_{CoagClay}\Gamma_{HACoag}$$


### There are 3 possible initial points of contact that can lead to attachment
$$\alpha = \alpha_{ClayCoag}+\alpha_{CoagCoag}+\alpha_{CoagHA}$$

$$\alpha_{ClayCoag} =2\left(1-\Gamma_{CoagClay} \right)\left [\Gamma_{CoagClay}\left ( 1-\Gamma_{HACoag} \right )  \right ]$$

$$\alpha_{CoagCoag} =\left [\Gamma_{CoagClay}\left (1-\Gamma_{HACoag}\right )\right ]^{2}$$

$$\alpha_{CoagHA} =2\left [\Gamma_{CoagClay}\left (1-\Gamma_{HACoag}\right )\right ]\Gamma_{CoagClay}\Gamma_{HACoag}$$


### Particle collisions appears to be dominated by viscous shear
$$\begin{array}{l}
\lambda_v \approx \Pi_{kv} \eta_K
\\
\Pi_{kv} \approx 50
\end{array}$$

$$d_{Clay} = 4\mu m$$


### What does Gt mean?
$$\begin{array}{l}
G = \frac{du}{dy}
\\
\int \limits_0^\Lambda  {Gdy}  = \int \limits_0^{v_r} {du}
\\
\Lambda G = v_r
\\
L_{Deformation} = v_rt
\\
Gt = \frac{L_{Deformation}}{\Lambda}
\end{array}$$

**Off-slide**
$$\frac{L_{Deformation}}{S_{Floc}}$$


### Surface coverage ($\Gamma$) of clay by coagulant precipitate
$$dN_c = \frac{\Gamma}{t_c} dt$$


### Surface coverage ($\Gamma$) << 1 and small loss to reactor walls
$$\Gamma = \frac{n_{nc_0} \frac{\pi}{4} d_{nc}^2 }{n_{p_0}\pi d_p^2}$$

$$\Gamma = \frac{n_{nc_0} d_{nc}^2}{4 n_{p_0} d_p^2}$$

$$\Gamma = \frac{ \frac{6}{\pi d_{nc}^3} \frac{C_{nc_0}}{\rho_{nc}} \pi d_{nc}^2}{4 \frac{6}{\pi d_P^3} \frac{C_{P_0}}{\rho_P} \pi d_p^2}$$

$$n_P = \frac{C_P}{\rlap{-} V_P} \rho_P
= \frac{6}{\pi d_P^3}\frac{C_P}{\rho_P}$$

$$\Gamma = \frac{C_{nc_0}}{4 d_{nc}\rho_{nc}} \frac{d_P \rho_P}{C_{P_0}}$$

$$\Gamma = \frac{1}{4} \frac{C_{nc_0}}{C_{P_0}} \frac{\rho_P}{\rho_{nc}} \frac{d_P}{d_{nc}}$$

$$\Gamma = \frac{\phi_{Coag}}{\phi_{Clay}} \frac{D_{Clay}}{D_{Coag}} \frac{\Pi_{A_{Clay}A_{Total}}}{\pi \Pi_{ClaySphere}}$$

$$\frac{3}{2} \left( n_P^{- \frac{2}{3}} - n_{P_0}^{- \frac{2}{3}} \right) = k \pi d_P^2 Gt \Gamma$$

$$\frac{3}{2} \left( \frac{n_P^{- \frac{2}{3}}}{n_{P_0}^{- \frac{2}{3}}}
- \frac{n_{P_0}^{- \frac{2}{3}}}{n_{P_0}^{- \frac{2}{3}}} \right)
= k \pi d_P^2 Gt \frac{n_{nc_0} d_{nc}^2}{n_{P_0}^{- \frac{2}{3}} n_{p_0}d_p^2}$$

$$\bar Gt \approx \frac{3}{2} \frac{\Lambda^2}{k \pi d_P^2 \Gamma}$$

$$\Lambda^2 = \frac{2}{3} k \pi d_P^2 \Gamma \bar Gt$$

$$\Lambda^2 = \frac{2}{3} k \pi d_P^2 \bar Gt \frac{1}{4} \frac{C_{nc_0}}{C_{P_0}} \frac{\rho_P}{\rho_{nc}} \frac{d_P}{d_{nc}}$$

$$\Gamma = \frac{ \frac{6}{\pi d_{nc}^3} \frac{C_{nc_0}}{\rho_{nc}} \pi d_{nc}^2}{4\frac{6}{\pi d_P^3} \frac{C_{P_0}}{\rho_P}\pi d_p^2}$$


### Even with simplified assumptions, including G complicates the analysis
$$n_P = \frac{1}{\left( \frac{2}{3} k \pi Gt \frac{n_{nc_0} d_{nc}^2}{n_{p_0}} + \frac{1}{n_{P_0}^{\frac{2}{3}}} \right)^{\frac{3}{2}}}$$

$$\frac{6}{\pi d_P^3} \frac{C_P}{\rho_P}
= \frac{1}{
  \left( \frac{2}{3} k \pi Gt \frac{\frac{6}{\pi d_{nc}^3} \frac{C_{nc_0}}{\rho_{nc}} d_{nc}^2}{\frac{6}{\pi d_P^3} \frac{C_{P_0}}{\rho_P}} + \frac{1}{\left( \frac{6}{\pi d_P^3} \frac{C_{P_0}}{\rho_P} \right)^{\frac{2}{3}}} \right)^{\frac{3}{2}}
  }$$


### Solving for residual turbidity results in a complicated equation
$$C_P = \frac{\pi d_P^3 \rho_P}{6} \frac{1}{\left[ \frac{2}{3} k \pi Gt \frac{d_P^3}{d_{nc}} \frac{\rho_P C_{nc_0}}{\rho _{nc}C_{P_0}} + \left( \frac{\pi d_P^3}{6} \frac{\rho_P}{C_{P_0}} \right)^{\frac{2}{3}} \right]^{\frac{3}{2}}}$$


### Floc Model Equations for G
$$\Pi_{A_{Clay}A_{Total}} = \frac{SA_{ClayTotal}}{SA_{ClayTotal} + SA_{Wall}}$$

$$\Pi_{A_{Clay}A_{Total}} = \frac{1}{1 + \frac{SA_{Wall}}{SA_{ClayTotal}}}$$

$$SA_{Wall} = \pi D_{Tube} L_{Tube}$$

$$SA_{ClayTotal} = \frac{\pi}{4} D_{Tube}^2 L_{Tube} \frac{SA_{Clay}}{V_{Clay}} \phi_{Clay}$$

$$\Pi_{ClaySphere} = \frac{SA_{Clay}}{\rlap{-} V_{Clay}} \frac{ \frac{\pi}{6} D_{Clay}^3}{\pi D_{Clay}^2} = \frac{SA_{Clay}}{\rlap{-} V_{Clay}} \frac{D_{Clay}}{6}$$

$$\frac{SA_{Clay}}{\rlap{-} V_{Clay}} = \frac{6 \Pi_{ClaySphere}}{D_{Clay}}$$

$$SA_{ClayTotal} = \frac{3 \pi D_{Tube}^2 L_{Tube} \Pi_{ClaySphere}} {2D_{Clay}}{\phi_{Clay}}$$

$$R_{Clay} = \frac{1}{1 + \frac{4V_{Clay}} {D_{Tube} SA_{Clay} \phi_{Clay}}}$$


### Ratio of clay surface area to total surface area (including reactor walls)
$$\Pi_{A_{Clay} A_{Total}} = \frac{1}{
  1 + \frac{\pi D_{Tube} L_{Tube}}{
    \frac{3 \pi D_{Tube}^2 L_{Tube} \Pi_{ClaySphere}}{2D_{Clay}} \phi_{Clay}
  }
  }$$

$$\Pi_{A_{Clay} A_{Total}} = \frac{1}{
  1 + \frac{2D_{Clay}}{3D_{Tube} \Pi_{ClaySphere} \phi_{Clay}}
  }$$


### Poisson distribution and coagulant loss to walls combined to get surface coverage
$$\frac{N_{CoagPerClay}}{SA_{Clay}} = \frac{C_{Coag}}{\rho_{Coag}}\frac{1}{\frac{\pi}{6} D_{Coag}^3}
\frac{V_{Clay}}{SA_{Clay}}
\frac{\rho_{Clay}}{C_{Clay}}$$

$$\Pi_{A_{Clay} A_{Total}} = \frac{1}{1 + \frac{2D_{Clay}}{3D_{Tube} \Pi_{ClaySphere} \phi_{Clay}}}$$

$$\frac{D_{Coag}^2 N_{CoagPerClay}}{SA_{Clay}} =
\frac{\phi_{Coag}}{\phi_{Clay}}
\frac{D_{Clay}}{\pi D_{Coag} \Pi_{ClaySphere}}$$

$$\frac{SA_{Clay}}{\rlap{-} V_{Clay}} = \frac{6 \Pi_{ClaySphere}}{D_{Clay}}$$

$$\Gamma = 1 - e^{
 - \frac{D_{Coag}^2 N_{CoagPerClay}}{SA_{Clay}} \Pi_{A_{Clay} A_{Total}}
 }$$

$$\Gamma  = 1 - e^{
  - \frac{\phi_{Coag}}{\phi_{Clay}} \frac{D_{Clay}}{D_{Coag}} \frac{\Pi_{A_{Clay} A_{Total}}}{\pi \Pi_{ClaySphere}}
  }$$

$$\Gamma  = 1 - e^{
   - \frac{4D_{nc}^2 n_{nc}}{\pi D_P^2 n_P} \Pi_{A_{Clay} A_{Total}}
   }$$


### Clay platelet geometry
$$\Pi_{HD} = \frac{H_{ClayPlatelet}}{D_{ClayPlatelet}}$$

$$\rlap{-} V_{Platelet} = \frac{\pi}{4} D_{ClayPlatelet}^2 H_{ClayPlatelet}$$

$$\rlap{-} V_{Platelet} = \Pi_{HD} \frac{\pi}{4} D_{ClayPlatelet}^3$$

$$\rlap{-} V_{Platelet} = \frac{\pi}{6} D_{Clay}^3$$

$$\rlap{-} V_{Platelet} = \Pi_{HD} \frac{\pi}{4} D_{ClayPlatelet}^3 = \frac{\pi}{6} D_{Clay}^3$$

$$D_{ClayPlatelet} = \left( \frac{2}{3 \Pi_{HD}} \right)^{\frac{1}{3}} D_{Clay}$$

$$SA_{ClayPlatelet} = 2 \frac{\pi}{4} D_{ClayPlatelet}^2 + \pi D_{ClayPlatelet} H_{ClayPlatelet}$$

$$\Pi_{HD} = \frac{H_{ClayPlatelet}}{D_{ClayPlatelet}}$$

$$SA_{ClayPlatelet} = 2 \frac{\pi}{4} \left( \frac{2}{3 \Pi_{HD}} \right)^\frac{2}{3} D_{Clay}^2 + \Pi_{HD} \pi \left( \frac{2}{3\Pi_{HD}} \right)^\frac{2}{3} D_{Clay}^2$$

$$SA_{ClayPlatelet} = \left( \frac{1}{2} + \Pi_{HD} \right)
\left( \frac{2}{3{\Pi_{HD}}} \right)^\frac{2}{3} \pi D_{Clay}^2$$

$$\Pi_{ClaySphere} = \frac{SA_{ClayPlatelet}}{\pi D_{Clay}^2}$$

$$\Pi_{ClaySphere} = \left( \frac{1}{2} + \Pi_{HD} \right)
\left( \frac{2}{3 \Pi_{HD}} \right)^\frac{2}{3}$$


### Surface coverage of clay
$$\Pi_{A_{Clay} A_{Total}} = \frac{1}{1 + \frac{2D_{Clay}}{3D_{Tube} \Pi_{ClaySphere} \phi_{Clay}}}$$

$$\Gamma = 1 - e^{
  - \frac{\phi_{Coag}}{\phi_{Clay}} \frac{D_{Clay}}{D_{Coag}} \frac{1}{\pi} \frac{1}{\Pi_{ClaySphere} + \frac{2D_{Clay}}{3D_{Tube} \phi_{Clay}}}
  }$$

$$\Gamma = 1 - e^{
  - \frac{\phi_{Coag}}{\phi_{Clay}} \frac{D_{Clay}}{D_{Coag}} \frac{1}{\pi} \frac{1}{\left( \frac{1}{2} + \Pi_{HD} \right)
  \left( \frac{2}{3 \Pi_{HD}} \right)^\frac{2}{3} + \frac{2D_{Clay}}{3D_{Tube} \phi_{Clay}}}
  }$$

  $$\frac{\Pi_{A_{Clay} A_{Total}}}{\Pi_{ClaySphere}} = \frac{1}{\Pi_{ClaySphere} + \frac{2D_{Clay}}{3D_{Tube} \phi_{Clay}}}$$

  $$\Gamma = 1 - e^{
   - \frac{\phi_{Coag}}{\phi_{Clay}} \frac{D_{Clay}}{D_{Coag}} \frac{1}{\pi} \frac{1}{\left( \frac{1}{2} + \Pi_{HD} \right) \left( \frac{2}{3 \Pi_{HD}} \right)^\frac{2}{3}}   
   }$$


### Solving for Coagulant Dose
$$C_{Coag} = - \rho_{Coag} \left[ \left( \frac{1}{2} + \Pi_{HD} \right)
\left( \frac{2}{3 \Pi_{HD}} \right)^\frac{2}{3} + \frac{2D_{Clay}}{3D_{Tube} \phi_{Clay}} \right]
\frac{\pi D_{Coag} \phi_{Clay}}{D_{Clay}} \ln \left( 1 - \Gamma  \right)$$

$$Gt \approx \frac{3}{2} \frac{\Lambda^2}{k \pi d_P^2 \Gamma}$$

$$\Gamma \approx \frac{3}{2} \frac{\Lambda^2}{k \pi d_P^2 Gt}$$

$$C_D = \frac{24}{\rm Re}$$

$${\rm Re} = \frac{v_{r_{d_{Floc}}}}{d_{Floc}} \nu$$

$$F_D = C_D \left( \pi \frac{d_{Floc}^2}{4} \right) \rho \frac{v_{r_{d_{Floc}}}^2}{2}$$

**Off-slide**
$$C_{Coag} = - \phi_{Clay} \frac{\rho_{Coag} D_{Coag}}{D_{Clay}} \frac{\pi \Pi_{ClaySphere}}{\Pi_{A_{Clay} A_{Total}}} \ln \left( 1 - \Gamma \right)$$


### Slow velocity through the annulus,Fast velocity at separation $\Lambda$
$${\rm Re} = \frac{v_{r_{d_{Floc}}}}{d_{Floc}} \nu$$

$$F_D = C_D \left( \pi \frac{d_{Floc}^2}{4} \right) \rho \frac{v_{r_{d_{Floc}}}^2}{2}$$

$$F_\tau = 2 \tau_0 \left( \pi \frac{d_{Floc}^2}{4} \right)$$

$$\tau_0 = \nu \rho \frac{v_{r_{Clay}}}{\frac{d_{Clay}}{2}}$$

$$2 \nu \rho \frac{v_{r_{Clay}}}{\frac{d_{Clay}}{2}}
\left( \pi \frac{d_{Floc}^2}{4} \right) =
\frac{24}{\frac{v_{r_{d_{Floc}}}}{d_{Floc}}} \nu
\left( \pi \frac{d_{Floc}^2}{4} \right) \rho \frac{v_{r_{d_{Floc}}}^2}{2}$$

$$\frac{v_{r_{Clay}}}{v_{r_{d_{Floc}}}} = \frac{3d_{Clay}}{d_{Floc}}$$

$$v_{r_{Clay}} = 3v_{r_\Lambda} \frac{d_{Clay}}{d_{Floc}}$$

$$v_{r_{Clay}} = 3 \Lambda G \frac{d_{Clay}}{d_{Floc}}$$


### CMFR model
$$\forall_r \frac{dC}{dt} = \left( C_{in} - C \right) Q$$

$$\frac{dn_P}{- kn_P} = \pi d_P^2 n_P^\frac{2}{3} \bar G \Gamma dt$$

$$\frac{dn_P}{dt_{rxn}} = - k \pi d_P^2 n_P^\frac{5}{3} \bar G \Gamma$$

$$\frac{\partial n_p}{\partial t_{advection}} = \frac{n_{p_0} - n_p} \theta$$

$$\begin{array}{l}
\frac{dn_p}{dt} = \frac{\partial n_p}{\partial t_{advection}} + \frac{\partial n_P}{\partial t_{rxn}}
\\
\frac{\partial n_p}{\partial t_{advection}} = \frac{n_{p_0} - n_p}{\theta}
\\
\frac{\partial n_P}{\partial t_{rxn}} = - k \pi d_P^2 n_P^\frac{5}{3} \bar G \Gamma
\\
\frac{dn_p}{dt} = \frac{n_{p_0}}{\theta} - \frac{n_p}{\theta} - k \pi d_P^2 n_P^\frac{5}{3} \bar G \Gamma
\end{array}$$

$$ - \frac{3}{2} \left( n_P^{- \frac{2}{3}} - n_{P_0}^{- \frac{2}{3}} \right) = - k \pi d_P^2 \bar Gt \alpha$$

$$n_P = \frac{6}{\pi d_P^3} \frac{C_P}{\rho_P}$$

$$1 = k \frac{2\pi}{3} \left( \frac{6}{\pi} \right)^\frac{2}{3} \bar Gt \alpha \left( \frac{C_P}{\rho_P} \right)^\frac{2}{3}$$

$$C_P = \rho_P \frac{\pi}{6} \left( \frac{3}{2\pi} \frac{1}{k \bar Gt \alpha } \right)^\frac{3}{2}$$

$$\begin{array}{l}
0.1 \frac{C_P}{\rho_P} \frac{6}{\pi} =
\left( \frac{3}{2 \pi} \frac{1}{k x \bar Gt \alpha} \right)^\frac{3}{2}
\\
x = 0.1^\frac{- 2}{3} = 4.64
\end{array}$$


### Another "Click to add title!" These guys are the best
$$\bar Gt = \frac{3}{2} \frac{\left( \Lambda^2 - \Lambda_0^2 \right)}{k \pi d_{Clay}^2 \alpha}$$

$$\Lambda = n_{Clay}^\frac{- 1}{3}$$

$$n_{Clay} = \frac{6}{\pi d_{Clay}^3} \frac{C_{Clay}}{\rho_{Clay}}$$

$$\bar Gt = \frac{3}{2} \frac{\Lambda^2}{k \pi d_{Clay}^2 \alpha}$$

$$C_{Clay} = \frac{\pi \rho_{Clay}}{6} \frac{1}{
  \left( \frac{2}{3} k \pi \alpha \bar Gt \right)^\frac{3}{2}
  }$$


### Comparison with Karen’s model
$$pC^\ast = \log \left( \beta G \theta \Gamma \phi_0^\frac{2}{3} \right)$$

$$C^\ast = \frac{1}{\beta Gt \Gamma \phi_0^\frac{2}{3}}$$

$$\bar Gt = \frac{3}{2 k \pi \alpha}
\left( \frac{\pi}{6} \frac{\rho_{Clay}}{C_{Clay}} \right)^\frac{2}{3}$$

$$\bar Gt = \frac{3}{2 \pi}
\left( \frac{\pi}{6} \right)^\frac{2}{3} \frac{1}{k \alpha \phi^\frac{2}{3}}$$

$$\bar Gt = \frac{3}{2 \pi}
  \left( \frac{\pi}{6} \right)^\frac{2}{3} \frac{1}{k \alpha \phi^\frac{2}{3} \left( \frac{C_0}{C_0} \right)^\frac{2}{3}}$$

$$C^{\ast^\frac{2}{3}} = \frac{3}{2\pi}
\left( \frac{\pi}{6} \right)^\frac{2}{3} \frac{1}{k \bar Gt \alpha \phi_0^\frac{2}{3}}$$


### Collision of a small floc with a large floc
$$\begin{array}{l}
V_{r_1} =  - \frac{Gr_1}{2}
\\
V_{r_2} =  + \frac{Gr_2}{2}
\\
\Delta V_r = \frac{G}{2} \left( r_1 + r_2 \right)
\\
\left( r_1 + r_2 \right)_{Max} = \frac{2 \Delta V_{r_{Max}}}{G}
\end{array}$$

$$\begin{array}{l}
V_{r_1} = \frac{Gr_1}{2}
\\
V_{r_2} = - \frac{Gr_2}{2}
\\
V_{t_2} = G \left( r_1 + r_2 \right)
\\
\Delta V = V_{t_2} + V_{r_2} - V_{r_1}
\\
\Delta V = G \left( r_1 + r_2 \right) - \frac{Gr_2}{2} - \frac{Gr_1}{2}
\\
\Delta V = \frac{G}{2} \left( r_1 + r_2 \right)
\end{array}$$
