# Membranes Design Challenge


```python
import aguaclara
import aguaclara.core.physchem as pc
import aguaclara.core.head_loss as minorloss
import aguaclara.core.pipes as pipes
import aguaclara.design.human_access as ha
import aguaclara.core.constants as con
from aguaclara.core.units import unit_registry as u
import aguaclara.core.utility as ut
import numpy as np
import matplotlib.pyplot as plt

Membrane_v = (30 * u.L/u.m**2/u.hr).to(u.um/u.s)
Membrane_v.to(u.m/u.hr)
((0.2*u.bar)/(1000*u.kg/u.m**3 * u.standard_gravity)).to(u.m)
(15*u.m/u.hr).to(u.mm/u.s)

params = {'legend.fontsize': 'x-large',
          'figure.figsize': (15, 5),
         'axes.labelsize': 'xx-large',
         'axes.titlesize':'x-large',
         'xtick.labelsize':'x-large',
         'ytick.labelsize':'x-large'}
plt.rcParams.update(params)
plt.figure(figsize = (10,6))
plt.xlabel('Particle diameter (nm)');
plt.ylabel('Rejection (%)');
plt.xscale("log")
plt.xlim(1,1000);
plt.ylim(1,100);
plt.grid(axis="both")
plt.savefig('junk')
plt.show()


```

MemCOR XS system
https://www.evoqua.com/en/brands/Memcor/Pages/memcor-xs.aspx

```python
(120*u.gal/u.min/(2.4 * u.m * 4.4 * u.m)).to(u.mm/u.s)
(90*u.m**3/u.hr).to(u.L/u.s)
```

100 nm pore diameter
Porosity of 0.2 (I can’t find any data!)
Pore length of 100 x diameter
Approach velocity of 10 um/s
What is the head loss?
Pore velocity = va/porosity
$$ h_{\rm{f}} = \frac{32\mu LV}{\rho gD^2} = \frac{128\mu LQ}{\rho g\pi D^4}$$


```python
d=100 * u.nm  
L = 1000*d
V_a = 8 * u.um/u.s  
porosity = 0.15
Temp=15*u.degC
headloss =( 32*pc.viscosity_dynamic(Temp)*L*V_a/(porosity*pc.density_water(Temp)*u.standard_gravity*d**2)).to(u.cm)
headloss

(14800000*u.USD/(15*u.Mgal/u.day)).to(u.USD/(u.L/u.s))
```
# what
