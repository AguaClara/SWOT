## Rapid Mix Design

## Length and time scales for each of the processes
Let's begin by describing the coagulant injection for a 60 L/s plant. We will use a [linear flow orifice meter](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Flow%20Control%20and%20Measurement/FCM_Design.md#linear-flow-orifice-meter-lfom) with 20 cm of head loss.

```python
""" importing """
from aide_design.play import*
from aguaclara_research.play import*
import aguaclara_research.floc_model as fm
import matplotlib.pyplot as plt
from matplotlib.ticker import FormatStrFormatter
imagepath = 'AguaClara Water Treatment Plant Design/Rapid Mix/Images/'

Q_plant = 60 * u.L/u.s
HL_LFOM = 20 * u.cm
Pi_LFOM_safety = 1.2
SDR_LFOM = 26
from aide_design.unit_process_design import lfom as lfom
ND_LFOM = lfom.nom_diam_lfom_pipe(Q_plant,HL_LFOM)
print(ND_LFOM, '(',ND_LFOM.to(u.cm), ')')

L_flow = pipe.ID_SDR(ND_LFOM,SDR_LFOM)
L_flow
v_lfom = (Q_plant/pc.area_circle(pipe.ID_SDR(ND_LFOM,SDR_LFOM))).to_base_units()
print(v_lfom)
```

The LFOM requires a 16 inch diameter pipe.

10% velocity rule
```python

v_lfom = (Q_plant/pc.area_circle(pipe.ID_SDR(ND_LFOM,SDR_LFOM))).to_base_units()
print(v_lfom)
t_large_scale_mix = (pipe.ID_SDR(ND_LFOM,SDR_LFOM)/(0.1*v_lfom)).to_base_units()
print(t_large_scale_mix)
```


##### Example problem: Energy dissipation rate in a straight pipe
A water treatment plant that is treating 120 L/s of water injects the coagulant into the middle of the pipe that delivers the raw water to the plant and then splits the flow into 2 parallel treatment trains for subsequent flocculation. The pipe is PVC 16 inch nominal pipe diameter SDR 26. The water temperature is $0^{\circ}C$. Estimate the minimum distance between the injection point and the flow split.

Solution scheme
1) Calculate the friction factor

```python
T_water=0*u.degC
Pipe_roughness = mat.PIPE_ROUGH_PVC
Pipe_roughness
Nu_water = pc.viscosity_kinematic(T_water)
Q_pipe = 120 * u.L/u.s
ND_pipe = 16*u.inch
SDR_pipe = 26
ID_pipe = pipe.ID_SDR(ND_pipe,SDR_pipe)
f_pipe = pc.fric(Q_pipe,ID_pipe,Nu_water,Pipe_roughness)
N_pipe_diameters = (2/f_pipe)**(1/3)
N_pipe_diameters
"""The minimum length for mixing is thus"""
L_mixing = ID_pipe*N_pipe_diameters
print('The minimum distance required for mixing across the diameter of the pipe is ',L_mixing.to_base_units())
```
The previous analysis provides a minimum distance for sufficient mixing so that equal mass flux of coagulant will end up in both treatment trains. This assumes that the coagulant was injected in the pipe centerline. Injection at the wall of the pipe is a poor practice and would require many more pipe diameters because it takes significant time for the coagulant to be mixed out of the slower fluid at the wall.
The time required for mixing at the scale of the flow in the plant is thus accomplished in a few seconds. This ends up being the fastest part of the transport of the coagulant nanoparticles on their way to attachment to the clay particles.

Next we will determine a typical flow rate of coagulant. **Aluminum** concentrations for polyaluminum chloride (PACl) typically range from 1 to 10 mg/L. The maximum PACl stock solution concentration is about 70 g/L as **Al**.

```python
C_PACl_stock = 70 *u.g/u.L
C_PACl_dose_max = 10 * u.mg/u.L
Q_PACl_max = (Q_plant*C_PACl_dose_max/C_PACl_stock).to(u.mL/u.s)
print(Q_PACl_max)
```
We can estimate the diameter of the injection port by setting the kinetic energy loss where the coagulant is injected into the main flow to be 10 cm. The amount of energy we invest in injecting the coagulant into the raw water is a compromise between having to raise the entire chemical feed system including the stock tanks to increase the potential energy and a goal of not having pressure fluctuations inside the LFOM pipe cause flow oscillations in the chemical dosing tube. Thus our goal is to have the kinetic energy at the injection point be large compared with the expected pressure fluctuations in the LFOM.

```python
HL_Coag_injection = 10 * u.cm
v_Coag_injection = ((2 * u.gravity * HL_Coag_injection)**0.5).to(u.m/u.s)
print(v_Coag_injection)
D_Coag_injection_min = pc.diam_circle(Q_PACl_max/v_Coag_injection)
print(D_Coag_injection_min.to(u.mm))
```   
