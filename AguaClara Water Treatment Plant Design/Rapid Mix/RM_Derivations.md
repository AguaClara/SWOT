# Rapid Mix Derivations

## $t_{eddy}$

Eddy turnover time, $t_{eddy}$, is the time it takes for the eddy to travel a distance equal to its length-scale. We assume that the energy of the large eddy is dissipated into smaller length scales in the time $t_{eddy}$:

$$t_{eddy} \sim \frac{L_{eddy}}{v_{eddy}}$$

The rate of energy loss to smaller scales is
$$ \varepsilon \sim\frac{v_{eddy}^2}{t_{eddy}} $$

Combining the two equations
$$ \varepsilon \sim\frac{v_{eddy}^3}{L_{eddy}} $$

We can use this equation to estimate the eddy velocity given an energy dissipation rate.
$$v_{eddy} \sim \left( \varepsilon \, L_{eddy} \right)^\frac{1}{3} $$
Now we can solve for the eddy turnover time which is a measure of the mixing time at the eddy scale.

$$\color{purple}{
  t_{eddy} \sim \frac{L_{eddy}}{\left( \varepsilon \, L_{eddy} \right)^\frac{1}{3}} \sim \left( \frac{L_{eddy}^2}{ \varepsilon }\right)^\frac{1}{3}
}$$

## $t_{coagulant, \, application}$
## Collision Rates
$${\rlap{-} V_{\rm{Cleared}}} \approx \pi d_{Clay} L_{Diff_{NC}} v_r t_c$$

Where $\rlap{-} V_{Occupied} = \Lambda_{Clay}^3$. Solve for $t_c$:

$$t_c = \frac{\Lambda_{NC}^3}{\pi d_{Clay} L_{Diff_{NC}} v_r}$$


This is the average time for a clay particle to have the entire volume of water that it occupies sweep past the clay particle. $v_r \approx \Lambda_{Clay} G$

$$t_c = \frac{\Lambda_{Clay}^3}{\pi d_{Clay} L_{Diff_{NC}} \Lambda_{Clay} G}$$

Where $t_c = \frac{dN_c}{dt}$:

$$dN_c = \pi d_{Clay} L_{Diff_{NC}}{\Lambda^{-2}_{Clay}} G dt$$


### Collision Rate and Particle Removal
A fraction of the remaining coagulant nanoparticles are removed during the time required for one sweep past the clay particle.

$$\frac{dn_{NC}}{ - k \, n_{NC}} = dN_c$$

$$\frac{dn_{NC}}{ - k \, n_{NC}} = \pi d_{Clay} L_{Diff_{NC}}{\Lambda^{-2}_{Clay}} G dt$$

### Integrate the coagulant transport model
Integrate from the initial coagulant nanoparticle concentration to the concentration at time t.
$$\int \limits_{n_{NC_0}}^{n_{NC}} n_{NC}^{- 1} \, dn_{NC}  =  - \pi d_{Clay} L_{Diff_{NC}} \Lambda^{-2}_{Clay} G \, k  \int \limits_0^t {dt} $$

Use pC notation to be consistent with how we describe removal efficiency of other contaminants.

$$2.3 p C_{NC} = \pi d_{Clay}\,  L_{Diff_{NC}}\,  \Lambda^{-2}_{Clay}\,  G k  t $$


Solve for the time required to reach a target efficiency of application of coagulant nanoparticles to clay.

$$\color{purple}{
  t_{coagulant, \, application} = \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} }
}$$

## $G_{coagulant, \, application}$

$$  \Delta h =   \frac{G^2 \nu \theta}{g} $$

Replace $\theta$ with t.

$$  \Delta h =  \frac{G^2 \nu}{g} \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}\,  L_{Diff_{NC}} } $$

$$L_{Diff} \approx \left( \frac{2k_B T d_{Clay}}{3 \pi \,\mu  \, d_{NC} G}\right)^\frac{1}{3} $$

$$  \Delta h =  \frac{G^2 \nu}{g} \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi G k \, d_{Clay}} \left( \frac{3 \pi \,\mu  \, d_{NC} G}{2k_B T d_{Clay}}\right)^\frac{1}{3}$$


Solve for the velocity gradient.
$$  \Delta h =  \frac{G^\frac{4}{3} \nu}{g} \frac{2.3p C_{NC} \, \Lambda_{Clay}^2}{\pi k \, d_{Clay}} \left( \frac{3 \pi \,\mu  \, d_{NC} }{2k_B T d_{Clay}}\right)^\frac{1}{3}$$

$$\color{purple}{
  G_{coagulant, \, application} =  d_{Clay}\left(\frac{\pi k \,g\Delta h }{2.3p C_{NC} \, \Lambda_{Clay}^2 \nu} \right)^\frac{3}{4} \left( \frac{2k_B T }{3 \pi \,\mu  \, d_{NC} }\right)^\frac{1}{4}
}$$
