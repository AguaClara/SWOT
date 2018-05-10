```python
# %% importing
from aide_design.play import*

from aguaclara_research.play import*

```

# Rapid Mix
Rapid mix is where the process of changing the surface properties of both suspended particles and dissolved substances begins. Rapid mix includes multiple steps that occur after a liquid coagulant is injected into the raw water stream that is on its way to the flocculator. Let's begin by describing the injection point for a 60 L/s plant. We will use a linear flow orifice meter with 20 cm of head loss.

```python
Q_plant = 60 * u.L/u.s
HL_LFOM = 20 * u.cm
Pi_LFOM_safety = 1.2
SDR_LFOM = 26
from aide_design.unit_process_design.prefab import lfom_prefab_functional as lfom
ND_LFOM = lfom.nom_diam_lfom_pipe(Q_plant,HL_LFOM,Pi_LFOM_safety,SDR_LFOM)
print(ND_LFOM)
```
The LFOM requires a 16 inch diameter pipe. Next we will determine a typical flow rate of coagulant. Aluminum concentrations for polyaluminum chloride (PACl) typically range from 1 to 10 mg/L. The maximum PACl stock solution concentration is about 70 g/L.

```python
C_PACl_stock = 70 *u.g/u.L
C_PACl_dose = 5 * u.mg/u.L
Q_PACl = (Q_plant*C_PACl_dose/C_PACl_stock).to(u.mL/u.s)
print(Q_PACl)
```

* Turbulent eddies distort the fluid such that the coagulant is mixed with the raw water down to a scale of perhaps 10 times the Kolmogorov length scale.
* Diffusion blends the coagulant with the raw water sufficiently so that the coagulant precipitates and forms nanoparticles.
* Dissolved organic molecules diffuse to the coagulant nanoparticles and adhere to the nanoparticle surface.
* The coagulant nanoparticles are transported to suspended particle surfaces by a combination of diffusion and fluid shear.

### Coagulant attachment mechanism
* Surface charge neutralization hypothesis
  * coagulant nanoparticles attach to each other
  *
* Polar bonds
  * Electronegativity reveals that the aluminum - oxygen bond is more polar than the hydrogen - oxygen bond
  * The bond between a coagulant nanoparticle and a clay surface can potentially be stronger than the bond between a water molecule and the clay surface.



### Transport steps
* Einstein's diffusion equation
* Estimate diffusion time scale
* Kolmogorov length scale
* Possibly introduce model for shear-diffusion transport of coagulant nanoparticles to clay
* Provide estimates of the time scales for each of the processes
