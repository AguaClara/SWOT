# Equations from CEE 4540 slides
This file is a temporary storage place for the LaTeX equations used in 4540 slides. Once some progress is made and the equations can be divided into groups, a well-designed file structure will be made.

**Notes for LaTeX math in Atom text editor**
1. Differentiating velocity ($V$) from volume ($\rlap{-} V$) is done with the `rlap{-}` function before the `V`. Using two dashes inside `\rlap{}`, which is how MathType translates volume,  results in the text losing its color coding in atom.
2. Using an asterisk (I will refrain from using one here) in LaTeX equations causes the text coloring to become a bit wonky and quite purple. Instead, use `\ast` when working within the dollar signs that denote math equations.


# **Rapid Mix**
### Gravity separation is awesome, but we need help
$$V_t = \frac{d^2 g}{18 \nu} \frac{\rho_p - \rho_w}{\rho_w}$$


### Coagulation slides
$$Basicity = \left( \frac{m}{3n} \right)$$

$$Al \left( OH \right)^{+2}$$


### This is the traditional approach: Power, Height, and G
$$G = \sqrt{ \frac{\varepsilon}{\nu}} $$

$$G = \left( \frac{P}{\rlap{-}V \rho \nu} \right)^{\frac{1}{2}}$$

$$P = G^2 \nu Q \theta \rho $$

$$P = Q \rho g \Delta h$$

$$\Delta h = \frac{P}{Q \rho g}$$

$$\Delta h = \frac{G^2 \nu \theta}{g}$$


### Rapid Mix: From macro to nano scale (in a few seconds?)
$$\begin{array}{l}
\lambda_v \approx \Pi_{kv} \eta_K
\\
\Pi_{kv} \approx 50
\end{array}$$

$$ \eta_K = \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$


### Turbulence -Mixing -Energy Dissipation
$$\varepsilon = \left[ \frac{W}{Kg} \right]
= \left[ \frac{J}{s \cdot Kg} \right]
= \left[ \frac{N \cdot m}{s \cdot Kg} \right]
= \left[ \frac{kg \cdot m \cdot m}{s^2 \cdot s \cdot Kg} \right]
= \left[ \frac{m^2}{s^3} \right]$$


### How far can turbulence mix? (Viscous inner length scale)
$$\eta_K = \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$

$$\lambda_v \approx \Pi_{kv} \eta_K$$

$$\Pi_{kv} \approx 50 $$

**Off-slide**
$${\rm Re}  
= \frac{V L}{\nu}
= \frac{L^2}{t\nu}
= \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{2}} \frac{1}{{\left( \frac{\nu}{\varepsilon} \right)}^{\frac{1}{2}} \nu}$$

$$L^2 = {\rm Re}_{transition} t \nu $$

$$L^2 = {\rm Re}_{transition} \left( \frac{\nu}{\varepsilon} \right)^{\frac{1}{2}}\nu$$

$$L^2 = {\rm Re}_{transition} \frac{\nu^{\frac{3}{2}}}{\varepsilon^{\frac{1}{2}}}$$

$$L_{transition} = \sqrt{\rm Re_{transition}} \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$


### The Reynolds Number requirement may be a challenge for lab scale flows and irrelevant above 0.1 L/s
$${\rm Re}_{Mixing} = \frac{V_{Jet} D_{Jet}}{\nu}$$

$${\rm Re}_{Mixing} = \frac{\pi Q_{Jet}}{4 D_{Jet}\nu}$$

$$D_{Jet} = \frac{\pi Q_{Jet}}{4 \nu {\rm Re}_{Mixing}}$$

$$V_{Jet} = \frac{Q_{Jet}}{\frac{\pi}{4} D_{Jet}^2}$$

$$h_{Jet} = \frac{V_{Jet}^2}{2g}$$


### Flow Expansion
$$h_e = \frac{V_{in}^2}{2g} \left( 1 - \frac{A_{in}}{A_{out}} \right)^2$$


### Jet Mixing
$$ \varepsilon_{Centerline} \cong \frac{50 D_{Jet}^3 V_{Jet}^3}{ \left( x - 2 D_{Jet} \right)^4}$$

$$ \varepsilon_{Max} \cong \frac{\left( \frac{50}{\left( 5 \right)^4} \right) V_{Jet}^3}{D_{Jet}}$$

$$ \varepsilon_{Max} \cong \frac{\left( \Pi_{RoundJet} V_{Jet} \right)^3}{D_{Jet}}$$

$$\Pi_{RoundJet} \cong 0.5$$


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


### How fast can diffusion mix?
$$D_{Diffusion} \propto V_{Diffusion} L_{Diffusion}$$

$$D_{Diffusion} \propto \frac{L_{Diffusion}}{t_{Diffusion}} L_{Diffusion}$$

$$t_{Diffusion} \propto \frac{L_{Diffusion}^2}{D_{Diffusion}}$$


### Molecular diffusion quantified
$$D_{Diffusion} = \frac{k_B T}{3 \pi \mu  d_P}$$

$$M W = \rho_P N_A \frac{\pi d_P^3}{6}$$

$$d_P = \left( \frac{6MW}{\pi \rho_P N_A} \right)^{\frac{1}{3}}$$

$$D_{Diffusion} = \frac{k_B T}{3 \pi \mu} \left( \frac{\pi \rho_P N_A}{6 M W} \right)^{\frac{1}{3}}$$

$$M W = \rho_P \rlap{-}V_P N_A$$


### Turbulent Mixing so that Molecular Diffusion can finish the job
$$\eta_K = \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$

$$L_D \approx \sqrt{D_{Diffusion} t_{Diffusion}}$$

$$\eta_K = L_D$$

$$\left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}} = \sqrt{D_M t_{Diffusion}}$$

$$t_{Diffusion} = \sqrt{ \frac{\nu^3}{\varepsilon D_M^2}} $$

**Off-slide**
$$t_{Diffusion} \approx \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{2}}\frac{1}{D_M}$$

$$\Pi_{D_{mix}} = \left( \frac{\varepsilon D_M^2 \, t_{Diffuion}^2}{\nu^3} \right)^{\frac{1}{4}}$$


### Kolmogorov Length scale may be smaller than what can be achieved by eddies
$$ \frac{\lambda_K}{\delta} < \frac{\lambda_v}{\delta} < \frac{\lambda}{\delta} <
\frac{\lambda_L}{\delta} < 1$$

$$ {\rm{Re}}^{-\frac{3}{4}} < \frac{\lambda_v}{\delta} \approx 50 \cdot {\rm{Re}}^{-\frac{3}{4}} < \frac{\lambda}{\delta} < \frac{\lambda_L}{\delta} \approx 5.0 \cdot {\rm{Re}}^{-\frac{1}{2}} < 1$$


### Viscous Energy Dissipation
$$\begin{array}{l}
\lambda_v \approx \frac{2 \pi}{k_v}
\\
k_v \eta_K = 0.125
\\
\lambda_v \approx \frac{2 \pi}{0.125} \eta_K = \Pi_{kv} \, \eta_K
\\
\lambda_v \approx \Pi_{kv} \, \eta_K
\\
\Pi_{kv} \approx 50
\end{array}$$


### Average distance between particles is the cube root of the volume occupied (L)
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


### Hypothesis: Energy Dissipation Rate for Micromixing
$$\eta_v = \Pi_{kv} \eta_K = \Pi_{kv} \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$

$$\Lambda  = D_P \left( \frac{\pi}{6} \frac{\rho_P}{C_P} \right)^{\frac{1}{3}}$$

$$\varepsilon = \nu^3 \left( \frac{\Pi_{kv}}{D_P} \right)^4 \left( \frac{6}{\pi} \frac{C_P}{\rho_P} \right)^{\frac{4}{3}}$$

**Half-off-slide**
$$D_P \left( \frac{\pi}{6} \frac{\rho_P}{C_P} \right)^{\frac{1}{3}} = \eta_v = \Pi_{kv} \, \eta_K = \Pi_{kv} \left( \frac{\nu^3}{\varepsilon} \right)^{\frac{1}{4}}$$


### How much water is cleared of nanoparticles by a clay particle?
$$\propto \pi \, d_{Clay} \, L_{Diff_{NC}}$$

$$ \propto t$$

$$ \propto v_r$$

$$V_{\rm{Cleared}} \propto \pi \, d_{Clay} \, L_{Diff_{NC}} \, v_r \, t$$


### Use dimensional analysis to get a relative velocity
$$\Lambda  = \frac{1}{n_P^{\frac{1}{3}}}$$

$$v_r = f \left( \varepsilon ,\nu ,\Lambda_{Clay} \right)$$

$$v_r = \Lambda_{Clay} f \left( \varepsilon ,\nu \right)$$

$$v_r \approx \Lambda_{Clay} \sqrt{\frac{\varepsilon}{\nu}} $$

$$v_r \approx \Lambda_{Clay} G$$

$$\Lambda_{Clay} = \left[ {\rm{L}} \right]
\, \, \, \, \, \, \,
\varepsilon = \left[ \frac{{\rm{L}}^2}{{\rm{T}}^3} \right]
\, \, \, \, \, \, \,
\nu = \left[ \frac{{\rm{L}}^2}{{\rm{T}}} \right]$$


### Diffusion band thickness
$$D_{Diffusion} = \frac{k_B T}{3 \pi \, \nu \rho \, d_P}$$

$$L_D \approx \sqrt{D_{Diffusion} t_{Diffusion}} $$

$$t_{Diffusion} = \frac{ \frac{d_{Clay}}{2}} {G \frac{d_{Clay}}{2}} = \frac{1}{G}$$

$$L_{Diff_{NC}} \approx \sqrt{ \frac{k_B T}{3 \pi \,\nu \rho_{NC} \, d_{NC} G}} $$


### Collision Rates
$${\rlap{-} V_{\rm{Cleared}}} \propto \pi d_{Clay} L_{Diff_{NC}} v_r t$$

$$t_c = \frac{\Lambda_{NC}^3}{\pi d_{Clay} L_{Diff_{NC} v_r}}$$

$$v_r \approx \Lambda_{Clay} G$$

$$\rlap{-} V_{Occupied} = \Lambda_{NC}^3$$

$$t_c = \frac{\Lambda_{NC}^3}{\pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G}$$

 $$dN_c = \frac{\pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G}{\Lambda_{NC}^3} dt$$


### Collision Rate and Particle Removal
$$dN_c = \frac{\pi d_{Clay} L_{Diff_{NC}}{\Lambda_{Clay} G}}{\Lambda_{NC}^3}dt$$

$$\Lambda_{NC}^3 = \frac{1}{n_{NC}}$$

$$dN_c = \pi d_{Clay} L_{Diff_{NC}}{\Lambda_{Clay}} G \, n_{NC}dt$$

$$\frac{dn_{NC}}{ - k \, n_{Clay}} = dN_c$$

$$\frac{dn_{NC}}{ - k \, n_{Clay}} = \pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G \, n_{NC} dt$$


### Integrate
$$\frac{dn_{NC}}{ - k \, n_{Clay}} = \pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G \, n_{NC} dt$$

$$\int \limits_{n_{NC_0}}^{n_{NC}} n_{NC}^{- 1} \, dn_{NC}  =  - \pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G \, k \, n_{Clay} \int \limits_0^t {dt} $$

$$2.3 p C_{NC} = \pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G k n_{Clay} t$$

$$t = \frac{2.3p C_{NC} \Lambda_{Clay}^2}{\pi d_{Clay} L_{Diff_{NC}} G k}$$

**Off-slide**
$$C_P^\frac{- 2}{3} = \frac{k \Gamma t}{\frac{3}{2 \pi G} \left( \rho_P \frac{\pi}{6} \right)^\frac{2}{3}} + C_{P_0}^\frac{- 2}{3}$$

$$\left( \frac{C_P}{C_{P_0}} \right)^\frac{- 2}{3} = \frac{2 \pi G k \Gamma \phi_0^\frac{2}{3} t}{3 \left( \frac{\pi}{6} \right)^\frac{2}{3}} + 1$$
