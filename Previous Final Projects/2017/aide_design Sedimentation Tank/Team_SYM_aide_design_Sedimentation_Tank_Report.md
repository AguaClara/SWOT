
# Capstone Design: Sedimentation Tank Remainder

### Team SYM

### Shiyao Sun and Melanie Lim


```python
from aide_design.play import*
from aide_design import floc_model as floc
from pytexit import py2tex
import math
from aide_design import expert_inputs as exp
```

<div class="alert alert-block alert-info">

# <u>Introduction</u>

The goal of this Capstone Design challenge is to design a sedimentation tank that can be used in multiple communities. According to given inputs focused on the remainder of the sedimentation tank, the tank dimensions can be calculated using flow equations and functions we have learned throughout this semester.


## Specify all the assumptions


```python
# The assumptions below are constraints we used to calculate dimensions of the sed tank.
# These assumptions can be adjusted based on various sedimentation tank design parameters and inputs.
# The sample calculations are calculated based on these assumptions, while the functions can be 
# applied to various designs.

# The PVC pipe used to make the inlet manifold determines the length of the sedimentation tank
L_sed = 6 * u.m

# The diffuser pipes used in the sedimentation tank have an SDR of 26.
# The manifold used in the sedimentation tank has an SDR of 41.
SDR_diffuser = 26
SDR_manifold = 41

# Upflow velocity at the top of the floc blanket:
V_sed_up = 1 * u.mm/u.s

# The corrugated plastic sheets used to make the plate settlers:
# The width of the sedimentation tank is determined by the plastic sheets
W_sed = (42 * u.inch).to(u.m)
thickness_sed_plate = 2 * u.mm

# The plate settlers are angled 60° from the horizontal:
angle_sed_plate = 60 * u.deg

# Assume the metal plates used to mold the diffusers to have 1/16" increments of thickness
increments_metal = 1/16 

# The plate setters are spaced 2.5cm apart (this is the perpendicular
# distance between plates, not the horizontal distance between plates):
s_sed_plate = 2.5 * u.cm

# Plate settler capture velocity:
V_sed_capture = 0.12 * u.mm/u.s

# The minimum port flow (from the first port) divided by the maximum port 
# flow (from the last port) for flow division between sedimentation tanks 
# and for flow distribution from the inlet manifold should be at least:
Q_ratio = 0.8

# Assumed stretch of the PVC pipes as they are heated and molded:
Pi_PVC_stretch = 1.2

# Nominal diameter of the sed tank diffuser
ND_sed_diffuser = 1 * u.inch

# Assume the minor loss coefficient to be 1
K = 1

# Assume the inlet manifold of this sedimentation tank has a head loss of 1 cm
headloss_sed_inlet_max = 1 * u.cm

# Assume headloss exiting the tank is 5 cm
headloss_exit = 5 * u.cm

# Assume Vena contract (VC) is 0.63
VC = exp.RATIO_VC_ORIFICE

# Assume spacing between orifices in outlet manifold is 10cm
spacing_orifices = 10 * u.cm

g = pc.gravity
```

## Inlet Diffusers

Diffusers are created by deforming the PVC pipe. The inner width of the rectangle is created by forcing the pipe over a rectangular wedge, which is the thickness calculated as the minimum inner width. During the molding process, PVC pipe wall cross-sectional area is conserved. The pipe wall is stretched in total length approximately 20%. Another way to think about this is that the thickness of the wall is reduced by a factor of 1/1.2 because the mass of PVC is conserved and the density is unchanged. Thus, volume and cross-sectional area are conserved.  
The PVC cross-sectional area is given using the following equation: 
$$Area_{PVC}=2\left (B_{diffuser}+W_{diffuser} \right )thickness_{wall}$$

The maximum diffuser velocity is given using the following equation: 
$$Vel_{Diffuser,Max}=\left(\frac{2\,Headloss_{SedInlet,Max}\,g}{K_{Minor}}\right)^{\frac{1}{2}}$$


```python
# Find the pipe's outer diameter according to its nominal diameter
OD_sed_diffuser = pipe.OD(ND_sed_diffuser)

# Find the pipe's inner diameter
ID_sed_diffuser = pipe.ID_SDR(ND_sed_diffuser,SDR_diffuser)

# Find the area of the PVC
Area_pvc = np.pi * (OD_sed_diffuser/2)**2 - np.pi * (ID_sed_diffuser/2)**2

# Find the thickness of the diffuser
thickness_wall = 1 / Pi_PVC_stretch * (OD_sed_diffuser - ID_sed_diffuser) /2 

def Width_diffuser (W_sed, V_sed_up, max_headloss, minorloss_coefficient,increments_metal):
    MaxV_diffuser = np.sqrt (2 * g * max_headloss / minorloss_coefficient)
    MinInnerW_diffuser = (V_sed_up * W_sed / MaxV_diffuser).to(u.inch)
    Available_thickness = np.arange(increments_metal, MinInnerW_diffuser.magnitude + increments_metal,increments_metal)
    Width_diffuser = (ut.ceil_nearest(MinInnerW_diffuser.magnitude,Available_thickness))*u.inch
    return (Width_diffuser)

Width_diffuser = Width_diffuser (W_sed, V_sed_up, headloss_sed_inlet_max,K,increments_metal)
print('The width of the diffuser is ' + ut.sig(Width_diffuser.to(u.cm),4) +'.')

# Find the outer length of the rectangular diffuser slot
B_diffuser = Area_pvc / thickness_wall / 2 - Width_diffuser

# Find the inner length of the rectangular diffuser slot
S_diffuser = B_diffuser - 2 * thickness_wall
Q_diffuser = V_sed_up * W_sed * B_diffuser
V_diffuser = Q_diffuser / Width_diffuser / S_diffuser
```

    The width of the diffuser is 0.3175 cm.
    

## Inlet Manifold

We want to distribute flow uniformly among the diffusers of the inlet manifold.
* The first equation is:
$$\left(\frac{1 - {\Pi_{DiffuserFlow}}^{2}}{{\Pi_{DiffuserFlow}}^{2} + 1} \right) {hl}_{ParallelPath} = \frac{{{Velocity}_{Manifold}}^{2}}{4g}$$
Where pi_diffuserFlow represents the ratio of minimum (first diffuser port) to maximum (last diffuser port) flow.
* The second equation calculates the diameter of the inlet manifold pipe:
$$ Inner Diameter of Manifold =\sqrt{ \frac{\left( {{Q_{sed}}} \right) *4}{{Velocity}_{Manifold} {\pi}} }$$


```python
def ND_inlet_manifold(L_sed, W_sed, V_Upflow, V_diffuser, SDR_manifold, Q_ratio):
    hl = V_diffuser **2 / 2 / pc.gravity
    max_velocity =  ((1-Q_ratio **2)/(Q_ratio**2+1) * hl * 4 * pc.gravity) ** (1/2) 
    Q_sed = L_sed * W_sed * V_Upflow
    Min_ID_manifold =((Q_sed / max_velocity) / math.pi * 4) ** (1/2)
    return (pipe.ND_SDR_available(Min_ID_manifold, SDR_manifold))

ND_inlet_manifold = ND_inlet_manifold(L_sed, W_sed, V_sed_up, V_diffuser, SDR_manifold, Q_ratio)
print('The nominal diameter of the inlet manifold is ' + ut.sig(ND_inlet_manifold.to(u.cm),4) +'.')
```

    The nominal diameter of the inlet manifold is 20.32 cm.
    

## Plate Settlers

![Screen%20Shot%202017-12-11%20at%204.16.06%20PM.png](attachment:Screen%20Shot%202017-12-11%20at%204.16.06%20PM.png)

* S: Distance between plate settlers
* B: Center to center distance
* T: Plate settler thickness
* V_Active: Vertical velocity component beneath the plate settlers
* V_plate: Vertical velocity component between the plate settlers
* The equation used to calculate the length of the plate settlers:
$$L = \frac{{S\left( {\frac{{{V_{Plate \uparrow }}}}{{{V_c}}} - 1} \right)+ T \frac{V_{Plate \uparrow }}{V_C} }} {{\sin \alpha \cos \alpha }}$$

Net vertical velocity is equal to the difference between the vertical velocity component between plate settlers and the capture velocity. The equation is established by equating the time a particle needs to travel distance h and h_c. 
* We used this middle-step to reach the final equation:
$$\frac{h_c}{V_c} = \frac{h} {{V_{Plate \uparrow}}-{V_c}}$$

$$\frac{S}{V_c cos(\alpha)} = \frac{L sin(\alpha)} {{V_{Plate \uparrow }}-{V_c}}$$

* The equation used to calculate the vertical height of the plate settlers:
$$ Vertical Height = length \times sin (\alpha)$$


```python
def Len_sed_plate(V_Upflow, V_Capture, Spacing_Settlers, Angle_sed_plate, Thickness_sed_plate):
    # Return the length of the plate settlers
    Top = Spacing_Settlers * (V_Upflow / V_Capture -1) + Thickness_sed_plate * (V_Upflow / V_Capture)
    Bottom = math.cos(Angle_sed_plate) * math.sin(Angle_sed_plate)
    Len_sed_plate = Top / Bottom
    return Len_sed_plate.to(u.cm)

def Vertical_Height_plate(V_Upflow, V_Capture, Spacing_Settlers, Angle_sed_plate, Thickness_sed_plate):
    # Return the vertical length of the plate settlers
    len_sed_plate = Len_sed_plate(V_Upflow, V_Capture, Spacing_Settlers, Angle_sed_plate, Thickness_sed_plate)
    return len_sed_plate * math.sin(Angle_sed_plate)

sed_plate_length = Len_sed_plate(V_sed_up, V_sed_capture, s_sed_plate, angle_sed_plate, thickness_sed_plate)
sed_plate_vertical_height = Vertical_Height_plate(V_sed_up, V_sed_capture, s_sed_plate, angle_sed_plate, thickness_sed_plate)

print('The required length of the plate settlers is ' + ut.sig(sed_plate_length.to(u.cm),4) +'.')
print('The vertical height of the plate settlers is ' + ut.sig(sed_plate_vertical_height.to(u.cm),4) + '.')
```

    The required length of the plate settlers is 46.19 cm.
    The vertical height of the plate settlers is 40.00 cm.
    

## Outlet Manifold (Effluent Launder) (Leave for Future Work)


```python
# Attempts to apply inlet manifold equations to outlet manifold, but probably incorrect

def ND_outlet_manifold(L_sed, W_sed, V_Upflow, SDR_manifold, Q_ratio, headloss_exit):
    max_velocity =  ((1-Q_ratio **2)/(Q_ratio**2+1) * headloss_exit * 4 * pc.gravity) ** (1/2) 
    Q_sed = L_sed * W_sed * V_Upflow
    Min_ID_manifold =((Q_sed / max_velocity) / math.pi * 4) ** (1/2)
    return (pipe.ND_SDR_available(Min_ID_manifold, SDR_manifold))

ND_outlet_manifold = ND_outlet_manifold(L_sed, W_sed, V_sed_up, SDR_manifold, Q_ratio,headloss_exit)
print('The nominal diameter of the outlet manifold is ' + ut.sig(ND_outlet_manifold.to(u.cm),4) +'.')
    
```

    The nominal diameter of the outlet manifold is 15.24 cm.
    

## Orifices 

We applied the function head_orifice from aide_design/physchem to solve for the diameter of each orifice. We then used the total length of the pipe and the spacing of the orifices to calculate the number of orifices required. The head loss from the orifice equals the difference between the total head loss and the inlet head loss. We divided the total flow rate of the plant and the total head loss of all the orifices combined by the number of orifices to determine the head loss per orifice and flow rate through a single orifice respectively. 
* The equation is:
$$ {hl}_{Orifice} = \left(\frac{{{Flow Rate}}}{{Ratio}_{VC Orifice}\times {Area}_{Orifice}}\right)^{2}\frac{1} {2g}$$



```python
def Diam_Orifices (L_sed, W_sed, V_Upflow, spacing_orifices, headloss_exit, headloss_sed_inlet_max, RatioVCorifice):
    headloss_orifice = headloss_exit - headloss_sed_inlet_max
    num_orifices = L_sed / spacing_orifices
    headloss_perorifice = headloss_orifice
    Q_sed = L_sed * W_sed * V_Upflow
    Q_orifice = Q_sed / num_orifices
    Area_orifice = Q_orifice / (RatioVCorifice * (headloss_perorifice* 2* g)**(1/2))
    return (4 / math.pi * Area_orifice) **(1/2)

Diam_Orifices = Diam_Orifices (L_sed, W_sed, V_sed_up,spacing_orifices, headloss_exit, headloss_sed_inlet_max, VC)
print('The diameter of the orifice is '+ut.sig(Diam_Orifices.to(u.cm),4)+'.')
    
```

    The diameter of the orifice is 1.560 cm.
    
