# Flocculation
Flocculation is gravity-powered
says Monroe Weber-Shirk
```python
# %%
from aide_design.play import*
from aide_design import floc_model as floc
from pytexit import py2tex
from sympy import*
from scipy.optimize import root
from scipy.optimize import brentq
import pandas as pd
```



```python
# %%
#Assumptions
Pi_VC = .62 #Vena contracta coefficient of an orifice
Ke = ((1/Pi_VC**2)-1)**2 #expansion coefficient

#Functions to calculate key parameters

def Gave(G_theta,h_floc,Temp):
    """Calculates average G given target minimum collision potential, total headloss, and design temperature
    equation from flocculation slides"""
    G_ave = (pc.gravity*h_floc/(G_theta*pc.viscosity_kinematic(Temp))).to(1/u.s)
    return G_ave

def restime(G_theta,G_ave):
    """Calculates residence time given collision potential and average G
    equation from flocculation slides"""
    theta = G_theta/G_ave
    return theta


def Dpipe(Ke,Pi_HS,Q,G_ave,Temp,SDR):
    """Calculates the actual inner diameter of the pipe
    equation from flocculation slides"""
    D_pipe = ((Ke/(2*Pi_HS*pc.viscosity_kinematic(Temp)*G_ave**2))*(4*Q.to(u.m**3/u.s)/np.pi)**3)**(1/7)
    return D_pipe

def Keactual(ID_pipe,G_ave,Temp,Pi_HS,Q):
    """estimates actual expansion coefficient given the actual inner diameter and other relevant inputs
    equation from flocculation slides"""
    Ke_actual = np.pi**3*ID_pipe**7*G_ave**2*pc.viscosity_kinematic(Temp)*Pi_HS/(32*Q.to(u.m**3/u.s)**3)
    return Ke_actual



def Aorifice(ID_pipe,Ke_actual,Temp,Q):
    """Calculates the orifice area given pipe inner diameter, expansion coefficient, Temperature, and flow"""
    A1 = (pc.area_circle(ID_pipe)).to(u.cm**2).magnitude #Pipe area
    Nu = pc.viscosity_kinematic(Temp) #kinematic viscocity
    Re = pc.re_pipe(Q,ID_pipe,Nu) #reynolds number

    def f_orif(A2,A1,Ke_actual,Re): #root of this function is the orifice area
        return (2.72+(A2/A1)*(4000/Re))*(1-A2/A1)*((A1/A2)**2-1)-Ke_actual

    A_orifice = (brentq(lambda A2: f_orif(A2,A1,Ke_actual,Re), -1, 2*A1))*u.cm**2 #numerical optimization

    return A_orifice


def eave(G_ave,Temp):
    """Calculates the average energy dissipation rate"""
    e_ave = (pc.viscosity_kinematic(Temp)*G_ave**2).to(u.mW/u.kg)
    return e_ave

def Hchip(A_orifice,ID_pipe):
    """This function calculates the height of the chip based on the orifice area and pipe diameter
    The function uses numerical optimization to solve the transcendental equation"""
    A_flow = A_orifice.magnitude #orifice area stripped of units
    r=(ID_pipe/2).magnitude #radius stripped of units
    c = A_flow/r**2 #left hand side of equation

    def f(a,c): #roots of this function are theta
        return a-sin(a)*cos(a)-c

    theta = brentq(lambda a: f(a,c), 0, 13) #numerical optimization
    r_u = r*u.cm #radius with units
    y = r_u - r_u*np.cos(theta) #height of orifice

    H_chip = ID_pipe-y #height of chip
    return H_chip

def Cost_Length(L_pipe,ND_pipe):
    """This function calculates the total cost of the system and the total length of the system"""
    #Length of pipe and number of fittings needed
    OD_pipe = pipe.OD(ND_pipe)
    Total_Pipe = L_pipe + .5*u.m
    Number_T = np.ceil(Total_Pipe.magnitude)
    Number_Elbow = np.ceil(Total_Pipe.magnitude)

    if ND_pipe.magnitude == 3:
        Cost_T = 3.94*u.dollar
        Cost_Elbow = 3.53*u.dollar
        Cost_Pipe = (17.14/10*(u.dollar/u.foot)).to(u.dollar/u.m)
        Cost_Valve = 10*u.dollar
        Width_T = (3.99*u.inch).to(u.cm)
        Width_Elbow = (3.97*u.inch).to(u.cm)


    if ND_pipe.magnitude ==4:
        Cost_T = 7.16*u.dollar
        Cost_Elbow = 5.40*u.dollar
        Cost_Pipe = (21.5/10*(u.dollar/u.foot)).to(u.dollar/u.m)
        Cost_Valve = 10*u.dollar
        Width_T = (5.06*u.inch).to(u.cm)
        Width_Elbow = (5.06*u.inch).to(u.cm)

    if ND_pipe.magnitude ==6:
        Cost_T = 7.16*u.dollar
        Cost_Elbow = 5.40*u.dollar
        Cost_Pipe = (21.5/10*(u.dollar/u.foot)).to(u.dollar/u.m)
        Cost_Valve = 10*u.dollar
        Width_T = (5.06*u.inch).to(u.cm)
        Width_Elbow = (5.06*u.inch).to(u.cm)


    Total_Cost = Cost_Pipe*Total_Pipe + Cost_T*Number_T + Cost_Elbow*Number_Elbow + Cost_Valve*Number_Elbow
    Floor_Length = Number_T*(Width_T+Width_Elbow-OD_pipe).to(u.m)
    Output=[Total_Cost,Floor_Length]
    return Output
```



```python
#Inputs
D_Sed = 2.5*u.cm
A_Sed = pc.area_circle(D_Sed)
V_Sed = 2*u.mm/u.s
Q = (V_Sed*A_Sed).to(u.mL/u.s)
print('The flow rate is',Q)

Temp = 15*u.degC
h_floc = 50*u.cm #standard for Aguaclara plants
G_theta = 20000 #standard for Aguaclara plants
Pi_HS = 6  ##3-6 is a good range, more research needed
SDR = 41 #Standard ratio
```

```python
#Calculate G average using functions listed above and given inputs
G_ave = Gave(G_theta,h_floc,Temp)
theta = restime(G_theta,G_ave)
e_ave = eave(G_ave,Temp)
print('The average G value is ',G_ave)
print('The residence time in the flocculator is ',theta)
print('The average energy dissipation rate is ', e_ave)
```


```python
#Calculate the pipe diameter, both inner and nominal and determine area of pipe using inner diameter output
D_pipe = (Dpipe(Ke,Pi_HS,Q,G_ave,Temp,SDR)).to(u.cm)
#Calculate nominal diameter of pipe
ND_pipe = pipe.ND_SDR_available(D_pipe,SDR)
#Calculate nominal diameter of pipe
ID_pipe = pipe.ID_SDR(ND_pipe,SDR).to(u.cm)

ID_pipe = 5*u.mm
#Calculate inner diameter of pipe
A_pipe = (pc.area_circle(ID_pipe)).to(u.cm**2)

print('The ideal inner diameter of the pipe would be ',D_pipe)
print('The nominal diameter of the pipe is ',ND_pipe, ', and the inner diameter is ', ID_pipe)
print('The area of the pipe is ', A_pipe)
```


```python
#Calculate the actual Ke as a result of the calculated inner pipe diameter
Ke_actual = (Keactual(ID_pipe,G_ave,Temp,Pi_HS,Q)).to(u.dimensionless)
print('The initial expansion minor loss coefficient was ',Ke)
print('The actual expansion minor loss coefficient is ',Ke_actual)
```


```python
#Calculate the orifice area
A_orifice = Aorifice(ID_pipe,Ke_actual,Temp,Q)
print('The orifice area is ',A_orifice)
```

```python
# The following line of code needs to be removed once the orifice area equation is corrected.

H_chip = Hchip(A_orifice,ID_pipe)
print('The height of the chip is ', H_chip)
```
```python
#Calculate average velocity
V_avg = (Q/pc.area_circle(ID_pipe)).to(u.m/u.s) #first calculate average velocity
print('The average velocity is ',V_avg)

#Calculate pipe length
L_pipe = (V_avg*theta).to(u.m) #then multiply velocity by residence time to get the required length of pipe
print('The length of the pipe is ',L_pipe)
