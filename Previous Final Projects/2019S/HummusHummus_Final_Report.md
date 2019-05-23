# TuBe Or Not TuBe: A Comparison of Alternative Plate and Tube Settler Geometries
### Team HummusHummus (Ananya Gangadhar, Jacqueline Wong, Justin Conneely)
#### Final Report
#### May 18, 2019

## 1. Introduction

### 1.1 Background

Sedimentation is a gravity-driven unit process in which suspended flocs are settled out from water. Large flocs made up of many primary particles and coagulant will settle if given enough time. In AguaClara plants, plate settlers are used to settle out flocs that were not captured in the floc blanket. Plate settlers are sloped surfaces that provide additional settling area for flocs, increasing the effective settling area of the sedimentation unit without increasing the plan view area (Weber-Shirk 2019).

![Diagram](https://aguaclara.github.io/Textbook/_images/sed_tank_overview.png)
Figure 1: Diagram of an AguaClara sedimentation tank

The current AguaClara plant design utilizes plate settlers, which are surfaces that provide additional settling area for flocs. This increases the effective settling area of the sedimentation unit without increasing the plan view area. Optimizing sedimentation is important because the more particles that sedimentation can remove, the fewer particles the filter will have to remove. This is good because filters can only handle a small amount of solids, and cleaning the filters with backwash uses a lot of water. In addition to this, sedimentation is by far the largest unit process in terms of plan view area because it is the slowest process. The large plan view area required makes sedimentation the most expensive unit process; therefore, exploring different plate and tube setter geometries and determining the optimal one is very important.

### 1.2 The Plan

This report is divided into three sections. In the first, we will try to optimize the current plate settler design to minimize the spacing between plates. Since the plate spacing is directly proportional to the length of the plate settlers, minimizing spacing allows for more room in the sedimentation tank for the floc blanket to form. The floc blanket plays an integral role in the removal of small flocs within the sedimentation tank, and is thus desired for better treatment efficiency.

In the second section, we will investigate the feasibility of using tube settlers instead of plate settlers in the AguaClara sedimentation tanks. Two kinds of tube settlers will be considered—Plascore and PP Aquatech Tube Settlers—and their treatment efficiencies will be evaluated.

![Plascore](https://www.plascore.com/wp-content/uploads/2013/07/cores-polycarbonate1.jpg)
Figure 2: Plascore polycarbonate honeycomb

![PPAquatech](https://cms.esi.info/Media/productImages/156328_1414755794566_PF.jpg)
Figure 3: PP Aquatech polypropylene tube settlers

In the third section, a comparative study will be performed between the three alternatives: Plascore tube settlers, PP Aquatech tube settlers, and the conventional AguaClara plate settlers. Various parameters such as ease of fabrication, cost, and availability will be evaluated and presented on a decision matrix.

### 1.3 Constraints

Below are some of the primary constraints that need to be considered in order to properly address all aspects of the above problem:

* Based on current AguaClara designs, the overall height of the sedimentation tank should not expand more than its current height. That is, the sum of the height of the settlers and the floc blanket needs to be constant for the sake of comparison.

* Floc blankets are necessary to ensure dampening of flow out of the diffuser and jet reverser. The floc blanket depth should be sufficient to ensure required particle removal efficiency. We are not currently sure of this value.

* The plate settler spacing and tube settler diameter need to be large enough such that there is no floc rollup. Flocs containing humic acid have a different density and size than clay flocs and may tend to rollup sooner with a reduction in plate spacing.

## 2. Optimal Plate Settler Spacing
### 2.1 Current Floc Rollup Model

The current floc rollup model calculates minimum plate spacing $S$ based on the following equation:

$$S\approx\frac{3}{\text{sin}^2\alpha}\frac{v_{P,V}}{v_t}d_0(\frac{18v_t\Phi\nu_{H_2O}}{gd_0^2}\frac{\rho_{H_2O}}{\rho_{Floc_0}-\rho_{H_2O}})^{\frac{1}{D_{Fractal}-1}}$$

where
$\alpha$ is plate settler angle
$v_{P,V}$ is vertical component of floc velocity
$v_t$ is terminal velocity of flocs
$\Phi$ is shape factor for drag on flocs
$\nu_{H2O}$ is kinematic viscosity of water
$g$ is gravitational acceleration on Earth
$d_0$ is floc diameter
$\rho_{H2O}$ is density of water
$\rho_{Floc_0}$ is density of floc
$D_{Fractal}$ is fractal dimension for flocs

This model results in a minimum plate settler spacing of 2.5 mm. However, AguaClara plants are currently using separations of 2.5 cm. This large safety factor is due to the fact that there are also flocs comprised of dissolved organic matter, also known as humic acid, which are a lot less dense than clay. Thus, the actual minimum spacing required is actually greater than 2.5 mm (Weber-Shirk 2019).

### 2.2 Accounting for Humic Acid

Similar to the current floc rollup model, $\alpha$ was taken as 60 degrees based on current AguaClara plate angle, $g$ as gravitational acceleration on Earth, and it was also assumed that $\Phi$ and the fractal dimension for flocs $D_{Fractal}$ remain the same as well. For a more conservative estimation, the kinematic viscosity $v_{H2O}$ and density $\rho_{H2O}$ of water were calculated based on a temperature of 10˚C. The terminal velocity of the floc particle $v_t$ is taken to be the designed capture velocity at 0.12 mm/s, and the vertical component of floc velocity $v_pv$ is taken to be 1 mm/s based on experiments with floc blankets.

To account for humic acid, our first model replaces the floc diameter $d_0$ with the diameter of one humic acid molecule $d_{HA}$ as 72 nm, based on the material specifications in the AguaClara Floc Model package. This package also has the density of humic acid as 1780 kg/m^3^. The textbook *Advances in Soil Science* claims that the density of soil organic matter is within the range 1.6 to 2.8 g/cm^3^ (Stewart, 1992). Since the plate settler spacing will be inversely proportional to the density of humic acid, we will use a more conservative design estimate and set the density of floc, $\rho_{Floc_0}$ to be the lower end of the density of humic acid, $\rho_{HA}$, as 1.6 g/cm^3^ (or 1600 kg/m^3^).

Based on this model, in order to capture humic acid flocs, the required plate settler spacing using the assumption that the floc is the size of a molecule of humic acid is 36.79 cm.

```python
import aguaclara
import aguaclara.core.physchem as pc
import aguaclara.core.head_loss as minorloss
import aguaclara.core.pipes as pipes
import aguaclara.design.human_access as ha
from aguaclara.core.units import unit_registry as u
from aguaclara.core import utility as ut
import numpy as np
import aguaclara.research.floc_model as floc
import aguaclara.core.constants as con

# Defining our constants
floc.HumicAcid.Density = 1600 * u.kg/u.m**3
Temp = 10 * u.degC # Lowest temperature for safety
nu_H2O = pc.viscosity_kinematic(Temp)
rho_H2O = pc.density_water(Temp)
v_c = 0.12 * u.mm/u.s
LS_ratio = 6
alpha = 60 * u.degree

# Assume upflow velocity is 1 mm/s based on experiments with floc blankets
v_PV = 1 * u.mm/u.s

# Terminal velocity is designed capture velocity of plate settlers
v_t = v_c

# Minimum spacing to prevent floc rollup of an humic acid molecule
dHA = floc.HumicAcid.Diameter * u.m
S_dHA = 3/((np.sin(alpha))**2) * (v_PV/v_t) * dHA * ((18*v_t*floc.PHI_FLOC*nu_H2O)/(u.gravity*dHA**2))*(rho_H2O/(floc.HumicAcid.Density - rho_H2O))**(1/(floc.DIM_FRACTAL-1))
S_dHA = S_dHA.to(u.cm)

print("In order to capture humic acid flocs, the required plate settler spacing using the assumption that the floc is the size of a molecule of humic acid is", ut.round_sf(S_dHA, 4))
```

However, the floc is made of both coagulant nanoparticles and humic acid. The coagulant nanoparticle is bigger than the humic acid molecule. Thus it would be better to start with a primary particle that is a coagulant nanoparticle that is covered with humic acid nanoparticles.

To account for this, our second model replaces the floc diameter $d_0$ with the diameter of a coagulant molecule $d_{PACl}$ as 90 nm, based on the material specifications in the AguaClara Floc Model package. The density of floc, $\rho_{Floc_0}$ was taken to be the density of coagulant, $\rho_{PACl}$, as 1138 kg/m^3^, again based on the material specifications in the AguaClara Floc Model package.

Based on this second model, in order to capture humic acid flocs, the required plate settler spacing using the assumption that the floc is the size of a molecule of coagulant is 91.05 cm.

```python
# Minimum spacing to prevent floc rollup of a coagulant nanoparticle
dPACl = floc.PACl.Diameter * u.m
S_dPACl = 3/((np.sin(alpha))**2) * (v_PV/v_t) * dPACl * ((18*v_t*floc.PHI_FLOC*nu_H2O)/(u.gravity*dPACl**2))*(rho_H2O/(floc.PACl.Density * u.kg/u.m**3 - rho_H2O))**(1/(floc.DIM_FRACTAL-1))
S_dPACl = S_dPACl.to(u.cm)

print("In order to capture humic acid flocs, the required plate settler spacing using the assumption that the floc is the size of a molecule of coagulant is", ut.round_sf(S_dPACl, 4))
```

Both spacings of 36.79 cm and 91.05 cm are much greater than the current AguaClara plate settler spacing of 2.5 cm (and even greater than the calculated minimum of 2.5 mm). This strongly suggests that humic acid flocs are not captured, even with the larger industry standard of 5 cm spacing for plate settlers.

It can be hypothesized that for the case of negligible clay concentration, humic acid and coagulant nanoparticle flocs will need to be captured with Stacked Rapid Sand Filters (StaRS). Furthermore, since the concentration of humic acid is measured in a few milligrams per liter, it is likely that filters can handle this particle loading and still maintain a reasonable fraction of water lost to backwash. Thus, for the scope of this project, the plate settler model will not be further modified to capture these low density flocs.

## 3. Tube Settlers

### 3.1 Material Specifications

#### 3.1.1 Plascore Honeycombs

The idea of using Plascore Honeycombs (PH) as potential tube settlers in a sedimentation tank was initially proposed by Dr. Weber-Shirk. A block of PH tube settlers will not only have a smaller diameter which would imply a shorter tube settler, it will also be self-supporting.

Table 1: Design specifications for the Plascore Honeycomb tube settlers
| Product | Length (inches) | Width (inches) | Height (inches) | Honeycomb Diameter (inches) | Tube Length (inches) | Angle (degrees) | Cost per Unit (USD) |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| A | 48 | 48 | 12 | 3/8 | 13.86 | 60 | 575 |
| B | 48 | 48 | 12 | 1/4 | 13.86 | 60 | 775 |

#### 3.1.2 PP Aquatech Tube Settlers

While conducting research for industrial tube settlers, the team came upon an Indian company PP Aquatech that manufactures tube settlers. While there exist several other companies in the US that manufacture tube settlers (such as Brentwood, Enexio, Suez and Muerer Research), PP Aquatech was chosen because the the team obtained the most design specs from this company. More research needs to be done to look into whether this company also supplies to Honduras and what the price markup will be. Some design specs can be seen below in Table 2 (PP Aquatech, 2019).

Table 2: Design specifications for PP Aquatech tube settlers
| Model | Plan Settling Area ($m^2/m^3$) | Height (cm) | Hydraulic Diameter (cm) | Angle (degrees) | Cost per unit (USD)|
| ---- |  ---- | ---- | ---- | ---- | ---- |
| TSM-50 | 12 | 100 | 3 | 60 | 86.11 |
| PP TSM-79 | 12 | 100 | 6 | 60 | 83.33 |

### 3.2 Availability

After conducting preliminary research on the availability of tube settlers in the countries of interest for AguaClara, it was found that conventional tube settlers are available in India as they are manufactured there (PP Aquatech, 2019). There is a good chance that Plascore tube settlers are also available in India but since confirming this would require making international calls, the team was unable to contact any potential suppliers in India. However, the import records strongly suggest that tube settlers of any kind can be imported to India due to the extensive trade relations the country has with other industrialized countries.

Checking for availability in Honduras is a bigger challenge with the amount of time at hand and therefore the team is moving forward by assuming that availability in India alone is sufficient to warrant a change in the sedimentation tank design. This is not a bad assumption since AguaClara has significant interest in building more water treatment facilities in India, and is currently in contact with several partners in the country.

## 4. Comparison of Plate and Tube Settlers

### 4.1 Removal Efficiency

The first step is to calculate the increased floc blanket depth for the different tube settler brands relative to the floc blanket depth associated with plate settlers. First, we used the current plate settler spacing of 2.5 cm, because making the spacing any smaller would present fabrication complications. However, we were not held to this limitation with tube settlers, as explained in the Humic Acid Model section above. In order to determine the corresponding required length, $L$, for the given spacings, we used the following equation:

$$L=\frac{S}{cos\alpha} (\frac{v_{\alpha}}{v_{c}}-\frac{1}{sin\alpha})$$

where
$S$ is settler spacing
$v_\alpha$ is floc velocity
$v_c$ is capture velocity
$\alpha$ is settler angle

In the above equation, we used the diameter (or hydraulic radius) as the spacing in addition to all the other same parameter values from the Humic Acid Model. This yielded the required tube settler length. Then, we assumed that the floc blanket depth for plate settlers was a constant one meter. For the sake of comparison, we held the sedimentation tank height constant. As such, we were then able to assume that the floc blanket depth would increase by the difference in the plate settler heights.

```python
# The current floc blanket depth for the plate settler system is 1 m
FB_depth_plate = 1 * u.m

# Calculating plate and tube settler lengths using the equation above
def settler_L(S, alpha):
  L = (S/np.cos(alpha.to(u.radian))*((v_PV/np.sin(alpha.to(u.radian))/v_c)-1/(np.sin(alpha.to(u.radian))))).to(u.cm)
  return L

H_plate = settler_L(2.5*u.cm, alpha)
H_plascoreA = settler_L(3/8*u.inch, alpha)
H_plascoreB = settler_L(1/4*u.inch, alpha)
H_PPAq_A = settler_L(3*u.cm, alpha)
H_PPAq_B = settler_L(6*u.cm, alpha)

# Tube settler floc blanket depth is FB_depth_plate plus the difference between the plate and tube settler heights.
FB_depth_plascoreA = FB_depth_plate + (H_plate * np.sin(alpha.to(u.radian)) - H_plascoreA * np.sin(alpha.to(u.radian)))
FB_depth_plascoreB = FB_depth_plate + (H_plate * np.sin(alpha.to(u.radian)) - H_plascoreB * np.sin(alpha.to(u.radian)))
FB_depth_PPAq_A = FB_depth_plate + (H_plate * np.sin(alpha.to(u.radian)) - H_PPAq_A * np.sin(alpha.to(u.radian)))
FB_depth_PPAq_B = FB_depth_plate + (H_plate * np.sin(alpha.to(u.radian)) - H_PPAq_B * np.sin(alpha.to(u.radian)))

print("The floc blanket depth for plate settlers is currently", FB_depth_plate, ". The floc blanket depths for both Plascore tube settlers are", ut.round_sf(FB_depth_plascoreA, 4), "and", ut.round_sf(FB_depth_plascoreB, 4), "and the floc blanket depth for the industry tube settlers are", ut.round_sf(FB_depth_PPAq_A, 4), "and", ut.round_sf(FB_depth_PPAq_B, 4))
```

Then, once we were able to figure out the corresponding floc blanket depths for each tube or plate settler model, we were then able to find out how much more efficient the sedimentation system would be. It is hypothesized that the log of removal is first order with respect to floc blanket depth. To estimate the rate constant, we used the equation below from the AguaClara Textbook "Sedimentation Future Work and Theory" section (Weber-Shirk 2019). Then, knowing that the floc blanket residence time is equal to the floc blanket height divided by the upflow velocity, we were able to get the following expression for the rate constant, $k_{fb}$ with respect to floc blanket depth:

$$ k_{fb} = -\frac{v_{P,V}}{h_{fb}}ln{\frac{C_{P}}{C_{P_0}}}$$

where
$v_{P,V}$ is vertical component of floc velocity
$h_{fb}$ is floc blanket height
$C_P$ is effluent particle concentration
$C_{P_0}$ is influent particle concentration

Once an estimate for the rate constant was determined, we then solved the differential equation for the effluent turbidity with respect to depth. In order to find the constant, we applied the boundary condition that at a floc blanket depth of 0 m, the floc blanket effluent is the same as the influent. This yielded this expression:

$$C_{p}(h_{fb})=Ce^{-k_{fb}\frac{h_{fb}}{v_{P,V}}}$$

We were then able to use the floc blanket depths determined above in this equation in order to determine particle removal efficiency.

![Slide14](https://raw.githubusercontent.com/JustinConneely/Personal/master/Images/Sed%20tank.png)
Figure 4: Graph from experiment in slide 14 of Sedimentation powerpoint

```python
# Equations taken from Sedimentation Future Work textbook section
effluent_NTU_exp = 1 * u.NTU # Slide 14 of Sedimentation.pptx
influent_NTU_exp = 100 * u.NTU # Slide 14 of Sedimentation.pptx
FB_depth_exp = 0.85 * u.m # Depth measured from AguaClara lab
k_fb = (-(v_PV/FB_depth_exp) * np.log(effluent_NTU_exp/influent_NTU_exp)).to(u.sec**(-1))

def effluent_NTU(influent_NTU, h_fb):
  effluent_NTU = (influent_NTU*np.exp(-k_fb*h_fb/v_PV)).to(u.NTU)
  return effluent_NTU

effluent_plate = effluent_NTU(100 * u.NTU, 1 * u.m)
effluent_plascoreA = effluent_NTU(100 * u.NTU, FB_depth_plascoreA)
effluent_plascoreB = effluent_NTU(100 * u.NTU, FB_depth_plascoreB)
effluent_PPAq_A = effluent_NTU(100 * u.NTU, FB_depth_PPAq_A)
effluent_PPAq_B = effluent_NTU(100 * u.NTU, FB_depth_PPAq_B)

print("The effluent turbidity for the plate settlers is", ut.round_sf(effluent_plate, 4), ". The effluent turbidity for the two Plascore tube settlers and the two industry tube settlers respectively are", ut.round_sf(effluent_plascoreA, 4),"and", ut.round_sf(effluent_plascoreB, 4), ", and", ut.round_sf(effluent_PPAq_A, 4), "and", ut.round_sf(effluent_PPAq_B, 4))
```

Given a constant sedimentation tank height and an influent turbidity of 100 NTU, the current plate settler system yields an effluent turbidity of 0.44 NTU. The Plascore tube settlers yield and effluent of 0.13 NTU or 0.1 NTU, depending on the model. The PP Aquatech tube settlers yield an effluent of 0.66 NTU or 7.16 NTU, also depending on the model. These results can be seen below in Table 3.

Table 3: Summary
| Product | Spacing (cm) | Floc Blanket Depth (m) | Effluent Turbidity (NTU) |
| ---- | ---- | ---- | ---- |
| Plascore A | 0.9525 (3/8 inch) | 1.227 | 0.1297 |
| Plascore B | 0.635 (1/4 inch) | 1.274 | 0.1008 |
| PPAq TSM-50 | 3 | 0.9267 | 0.6601 |
| PPAq TSM-79 | 6 | 0.4867 | 7.16 |
| AguaClara Plate Settlers | 2.5 | 1 | 0.4437 |

These results shows that Plascore tube settlers are more efficient. This means they may allow for the filters to be backwashed less frequently, thereby decreasing the amount of water that is wasted. However, it is important to note that for these increased floc blanket depths, a new design for the floc weir may be required.

### 4.2 Fabrication and Maintenance

The traditional plate settler model requires many different plates must be cut from large corrugated sheets. After this, holes to be drilled evenly through all the plate settlers in order to keep them evenly spaced. Doing this can be tedious and time consuming, especially for cases like Gracias, Honduras where there are 20 sedimentation tanks with many plates each. According to Antonio Elvir, it took 526 labor hours to make the plate settlers for 22 sedimentation tanks (about 24 hours per tank). Once in place the plates require supports to prevent them from sagging, as the material is flexible and will fold in on itself if left unsupported. As for maintenance, the plates can be lifted in units from the top of the sedimentation tank to allow access to the lower half of the sedimentation tank. This makes maintenance relatively easy, assuming proper care is taken in doing so.

By comparison, the tube settlers for both designs require significantly less fabrication. The tube setter unit must be cut into the shape of the sedimentation tank. In addition to this, a small ledge would need to be implemented during the making of the sedimentation tank. Because the tube settler unit is more rigid, it would require no additional supports. However, because tube settlers are one large unit of polycarbonate (Plascore) or polypropylene and PVC (PP Aquatech), they would be much more difficult to remove. It would be possible to potentially divide the tube settler brick into several smaller pieces for easier removal. In addition, at least for Plascore tube settlers, increasing the floc blanket depth could potentially make it more difficult to reach the floc weir.

As is evident, the plate settler approach requires significantly more fabrication. Because of this, even if the tube settlers are more expensive, it may be worth exploring this option for application in full-size AguaClara plants. However, both the tube settler designs pose more complications with respect to maintenance. More options for making maintenance easier for tube settlers will need to be explored in the future.

### 4.3 Techno-Economic Analysis

For the purposes of developing a coarse economic model to compare the cost-efficiency of the three design alternatives, the associated costs considered are material costs (quantitative) and fabrication / labor costs. The reason why the team decided not to include shipping costs in our model is because we could not find the shipping address in Florida in order to get a shipping cost per unit weight estimate from any international mailing service.

The following **assumptions** were made by the team for the economic model:
1) Flow rates across all three designs will be the same.
2) All three designs will have the same capture velocity of 0.12 mm/s.
3) Plan view area and depth of sedimentation tanks will be constant across all three designs.
4) The life span of the polycarbonate plate settlers is 50 years. This number was given to us by Dr. Weber-Shirk. Since Plascore tube settlers are also made of polycarbonate, their life span is also assumed to be 50 years. The lifespan of the Brentwood tube settlers is 25 years according to the sales representative; we will use this value for the PP Aquatech tube settlers.

Once again, it is important to note that this economic analysis only takes into account the costs that will vary between the three designs — the material costs, and the cost of construction. All other plant costs that will remain constant across the designs (such as cost of chemicals, land costs, plant operator wages, et cetera) are not included in this model. However, developing an exact model for construction time (and shipping costs) goes beyond the scope of this project and hence, cost of construction will only be spoken of in relative terms in this report.

```python
L_sed_tank = 5.5 * u.m
W_sed_tank = 42 * u.inch
Q_per_sed_tank = 6 * u.L/u.s # typical flow rate according to Juan
Q_plant = 30 * u.L / u.s # arbitrary value, can be changed
n_sed_tanks = np.ceil(Q_plant / Q_per_sed_tank) # number of sed tanks

# Calculating labor hours per sed tank
hrs_Gracias = 526 * u.hour # info from Antonio for Gracias plant
num_sed_tanks_Gracias = 22
hrs_per_sed_tank = hrs_Gracias / num_sed_tanks_Gracias
print('Number of labor hours required to build one sedimentation tank is', ut.round_sf(hrs_per_sed_tank,2))

# FIXED COSTS - MATERIALS
# PP Aquatech (PPAq) tube settlers with square holes from India
cost_PPAq_per_unit = (6200/72) * u.USD # converting INR to USD
spacing_PPAq = 1.5 * u.cm
L_PPAq_unit = 1 * u.m
W_PPAq_unit = 1 * u.m
H_PPAq_unit = 1 * u.m
cost_PPAq_per_m3 = (cost_PPAq_per_unit / (L_PPAq_unit * W_PPAq_unit * H_PPAq_unit)).to(u.USD / u.m**3)
cost_PPAq = (cost_PPAq_per_m3 * L_sed_tank * W_sed_tank * H_PPAq_unit).to(u.USD)
print('Cost per m3 of PP Aquatech tube settlers is',cost_PPAq_per_m3)
print('Cost per sed tank of using PP Auatech tube settlers is',cost_PPAq)

# Plascore tubing from the US
cost_plascore_per_unit = 575 * u.USD
spacing_plascore = (3/8) * u.inch
L_plascore_unit = 48 * u.inch
W_plascore_unit = 48 * u.inch
H_plascore_unit = 12 * u.inch
cost_plascore_per_m3 = (cost_plascore_per_unit / (L_plascore_unit * W_plascore_unit * H_plascore_unit)).to(u.USD/u.m**3) # cost per unit length of sed tank
cost_plascore = (cost_plascore_per_m3 * L_sed_tank * W_sed_tank * H_plascore_unit).to(u.USD)
print('Cost per m3 of plascore tube settlers is',cost_plascore_per_m3)
print('Cost for one sed tank with plascore tube settlers is',cost_plascore)

# Polycarbonate plate settlers
cost_PS_per_unit = 112.25 * u.USD # from McMaster website
spacing_PS = 2.5 * u.cm
L_PS_per_unit = 96 * u.inch
W_PS_per_unit = 48 * u.inch
thickness_PS = (3/32) * u.inch # only necessary to determine pricing from McMaster, used the value closest to existing plate settler thickness
n_PS = np.floor(1 * u.m/ (spacing_PS.to(u.m) + thickness_PS.to(u.m))) # number of plate settlers in one sed tank
cost_per_PS = (cost_PS_per_unit / (L_PS_per_unit * W_PS_per_unit) * W_sed_tank * H_plate).to(u.USD)
cost_PS = n_PS * cost_per_PS # for one sed tank
print('Cost per sed tank for polycarbonate plate settlers is',cost_PS)


```
Table 4: Summary of results of Python analysis on cost
| Product     | Spacing (cm) | Spacing (in) | Height (cm) | Cost per sed tank (USD) |
| ----------- | ------------ | ------------ | ----------- | ----------------------- |
| Plascore A  |        0.95      | 3/8          | 16.1      |    1201.0                     |
| Plascore B  |  0.635            | 1/4          |   10.8          |         800.8                |
| PPAq TSM-50 | 3            |   -           |         50.8    | 256.7                   |
| PPAq TSM-79 | 6            |     -         |         101.6    |      513.4                   |
|      Polycarbonate Plate Settlers       |   2.5           |      -        |        42.3     |            613.9             |

## 5. Conclusions

Based on the new model that takes into account humic acid while calculating optimal plate settler spacing, it can be concluded that current AguaClara plate settler spacing of 2.5 cm and industry standard settler spacing of 5 cm are both too small to capture humic acid flocs. This is because the first model with a humic acid molecule gives a minimum required spacing of 36.79 cm, and the second model with a coagulant particle also gives a large minimum required spacing of 91.05 cm. Thus, for the scope of this project, the plate settler model was not further modified to capture these low density humic acid flocs.

In terms of fabrication, traditional plate settlers take a comparatively longer time to construct as they have to be cut from large sheets and have holes drilled evenly throughout. Whereas for tube settlers, each unit only needs to be cut into the shape of the sedimentation tank. It also does not require additional support. However, plate settlers are easier to maintain as they can be lifted in units from the top of the sedimentation tank to allow access to the lower half of the sedimentation tank. On the other hand, tube settlers are much more difficult to remove as it first needs to be divided into several pieces, unless they are constructed in removable block units. Plascore tube settlers would be the easiest to install and maintain since they already come in blocks.

In terms of removal efficiency, based on the model in Section 4.1, the Plascore tube settlers achieve the highest removal efficiency based on the increased floc blanket depth, followed by the plate settlers, and lastly by the PP Aquatech tube settlers. Respectively, these options yielded effluent turbidities of 0.1 NTU, 0.13 NTU, 0.44 NTU, 0.66 NTU, and 7.16 NTU. For the Plascore tube settlers, this would allow for the filter to be backwashed less frequently. This would lead to less water being wasted, increasing the overall efficiency of the plant.

Overall, this analysis leads to a few distinct observations and conclusions. Firstly, these results clearly show that tube settlers, regardless of the brand, are a viable option for AguaClara plants moving forward. While their feasibility depends largely on the shipping costs of the tube settler units themselves, which in turn depends upon the proposed AguaClara plant's location, it is definitely worth considering. Out of the tube settler models that were analyzed in this report, the smaller diameter Plascore model and the smaller diameter PP Aquatech model are the most promising. The Plascore model is the most promising because not only does it yield a similar cost per sedimentation tank to our current plate settler model, but it also yields the lowest effluent turbidity. This is optimal because this would mean the filter system would need to be backwashed less frequently, which could significantly decrease costs in the long run by wasting less water. As for the PP Aquatech tube settlers, these (based on an admittedly coarse economic analysis), yielded by far the lowest cost out of any of the systems analyzed. This is important to bear in mind because the efficiency of these tube settlers can be improved with deeper sedimentation tanks should that prove to be cost-effective. While it is important to conduct a more in-depth cost-benefit analysis of these tube settlers prior to purchasing, this lower cost could make AguaClara plants more affordable for communities. Both Plascore and PP Aquatech tube settlers could be viable alternatives to our current plate settler model. A summary of all the parameters that were used to compare all the different settler geometries can be found below in Table 4.

Table 4: A summary of the parameters that were used to compare between different settler geometries
| Product | Spacing (cm) | Height of unit (cm) | Height of floc blanket (m) | Effluent Turbidity (NTU) | Cost per sed tank (USD) | Relative Installation Time |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| Plascore A | 0.9525 | 16.1 | 1.227 | 0.13 | 1202 | Low |
| Plascore B | 0.635 | 10.8 | 1.274 | 0.101 | 800.8 | Low |
| PPAq TSM-50 | 3 | 50.8 | 0.927 | 0.66 | 256.7 |  Medium|
| PPAq TSM-79 | 6 | 101.6 | 0.487 | 7.16 | 513.4 | Medium |
| AguaClara Plate Settlers | 2.5 | 42.3 | 1 | 0.444 | 613.9 |  High |

As the results from this investigation suggest that AguaClara should deeply consider the option of replacing plate settlers with tube settlers, we also have several suggestions for future work. In addition to preliminary research, we suggest conducting experimental research with the tube settlers too.

Furthermore, while conducting this investigation, several issues were encountered that have potential for future work as well. First of all, better documentation for the cost estimates for building plants would be helpful, as it was quite difficult for us to get this initial information. Secondly, there were some issues encountered with trying to get the plan view area of different plants, in particular issues with unit consistency for OnShape. Perhaps this could be a small project that the CAD team on AIDE-Template could work on.

Finally, based on our findings in the optimal plate spacing model, which suggests that the current AguaClara plate settler spacing of 2.5 cm (as well as industry standard of 5 cm) are not sufficient in preventing floc rollup of humic acid flocs. While we hypothesized that these humic acid flocs are later captured in a STaRS filter, we suggest future experimental research to confirm that humic acid cannot be removed in floc-sed, and that the STaRS filter is sufficient for its removal.

## 6. Acknowledgements

We would like to thank Antonio Elvir and Juan Guzman for their help in estimating labor hours and other associated costs. Additionally, we would like to thank Nicolette Ocasio for her help in navigating the AguaClara investment tool. Finally, we would like to thank Monroe Weber-Shirk, Jillian Whiting and Matthew Cimini for their support and guidance throughout this course.

## Bibliography

Balwan, K. (2016). Study of the effect of length and inclination of tube settler on the effluent quality. Journal (International Journal of Innovative Research and Advanced Engineering).

Hurst, M. (2010). Evaluation Of Parameters Affecting Steady-State Floc Blanket Performance. Thesis (Cornell University).

PP Aquatech. "Tube Settling Media". Website. Retrieved from https://www.exportersindia.com/ppaquatech/category-20236.htm

Stewart, B. (1992). Advances in Soil Science. Book (Springer-Verlag New York).

Swetland, K., Weber-Shirk, M., Lion, L. (2014). Flocculation-sedimentation performance model for laminar flow hydraulic flocculation with polyaluminum chloride and aluminum sulfate coagulants. Journal (Journal of Environmental Engineering).

Weber-Shirk, M., Guzman, J., O'Connor, C., Pennock, W., Lion, L., Du, Y., & Maisel, Z. (2019) "AguaClara Cornell Textbook."
