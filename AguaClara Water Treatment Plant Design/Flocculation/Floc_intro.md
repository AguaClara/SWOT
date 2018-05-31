```python
# %%
from aide_design.play import*
from aguaclara_research.play import*
from pytexit import py2tex
from sympy import*
from scipy.optimize import root
from scipy.optimize import brentq
import pandas as pd
```
# Flocculation
Flocculation transform inorganic (clays such as [kaolinite, smectite, etc. and metallic oxy-hydroxides such as goethite and gibbsite](https://www.sciencedirect.com/science/article/pii/S0048969708010103) ) and organic (viruses, bacteria and protozoa) primary particles into flocs (particle aggregates). Flocculation doesn't remove any particles from suspension. Instead it causes particle aggregation and then floc blankets, lamellar sedimentation, and sand filtration will be used to separate those flocs from the water. Sedimentation can remove flocs more easily than it can remove primary particles because flocs have a higher terminal sedimentation velocity. Floc blankets and sand filtration rely primarily on capture based on interception and interception is much more efficient when the particles are larger. Thus the purpose of flocculation is to join **all** of the primary particles together into flocs.

It is also possible that a difference in a physical property between primary particles and flocs plays a role in enhanced removal of flocs in floc blankets and filters. For example, the many relatively weak connection points between the primary particles in the flocs enables the flocs to deform. It is possible that deformation plays an important role right at the moment of collision. Presumably the bond strength required to lock the colliding particles together is less if the particles can deform as they are colliding.

## Primary particles can't attach to large flocs
One of the mysteries of flocculation has been why it is such a slow process and yet it appears to be a very rapid process. Plant operators observe that with high raw water turbidities that they can see flocculation progressing after about 0.5 minutes of flocculation. We can estimate the collision potential, $G\theta$ that corresponds to making visible flocs.
$$\bar G = \sqrt{ \frac{g h_e}{\theta \nu}}$$

```python
HL_floc = 43*u.cm
HRT = 8 * u.min
Temperature =20 * u.degC
G_floc = ((pc.gravity*HL_floc/(HRT*pc.viscosity_kinematic(Temperature)))**0.5).to_base_units()
print(G_floc)
Gt_floc = G_floc*HRT
HRT_floc_visible = 0.5*u.min
Gt_floc_visible = (G_floc*HRT_floc_visible).to_base_units()
print(Gt_floc_visible)
```
Here initial flocculation is visible at a $Gl/theta$ of less than 3000. Given that flocculation is visible at this low collision potential, it is unclear why recommended $Gl/theta$ are as high as 100,000. This is one of the great mysteries that motivated the search for a flocculation model that was based on hypotheses that were consistent with laboratory and field observations.
## History
The mechanism of particle-particle aggregation was thought to be controlled by an average surface charge. Apparently no one was able to develop a model of how that mechanism would influence particle attachment efficiency and the result was that no predictive models for flocculation were developed. There were several observations that were at odds with conventional explanations of flocculation.
1. Efficient flocculation at coagulant dosages that led to positive surface charge. This led to a second flocculation mechanism that was called "sweep floc" and that was used to describe any observations that didn't fit the charge neutralization flocculation hypotheses
1. Flocculation time for highly turbid suspensions was expected to proceed very rapidly and produce very low turbidity settled water. This expectation was not observed and led to the hypothesis that flocs were continually breaking up and producing primary particles or at least very small flocs.
1. The floc break up hypotheses led to the expectation that high turbidity suspensions would have significantly higher settled water turbidity than low turbidity suspensions. This expectation was also not observed.

Evidence that the charge neutralization hypothesis doesn't explain flocculation of surface waters has been accumulating for decades. *Sweep* flocculation has been proposed as an alternative category that described common observations that didn't fit the charge neutralization hypothesis. However, similar to the charge neutralization hypothesis, the *sweep* hypothesis didn't result in the development of predictive equations to describe the process.


For example, in 1992 Ching, Tanaka, and Elimelech published their research on [Dynamics of coagulation of kaolin particles with ferric chloride](https://doi.org/10.1016/0043-1354(94)90007-8). They found that the electrophoretic mobility which is a measure of the clay particle surface charge was never neutralized at pH 7.8 and was neutralized at $10\mu M$ at pH 6.0. The results were interpreted by the authors to mean that some combination of sweep floc and charge patchiness was responsible for the observed results.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Ching_Electrophoretic_Mobility_vs_Ferric_Chloride" width="400">

[Figure x. Electrophoretic_Mobility for final pH (after coagulant addition) of 6.0 and 7.8 as a function of $FeCl_3$ dose](https://doi.org/10.1016/0043-1354(94)90007-8)

The settled water turbidity was almost independent of pH even though the electrophoretic mobility was quite different for the two pH values tested.

[At pH 6.0 the ferric hydroxide precipitates are positively charged and at pH 7.8 they are close to neutral](https://doi.org/10.1016/0043-1354(94)90007-8). Thus it is apparent that neutralization of the clay surface charge can not explain these results.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%203_Rapid%20Mix/Images/Ching Residual_Turbidity_vs_Ferric_Chloride.png" width="400">

[Figure x. Settled water turbidity (jar tests) for final pH (after coagulant addition) of 6.0 and 7.8.](https://doi.org/10.1016/0043-1354(94)90007-8)

Electrostatic charge neutralization hypothesis
* The coagulant precipitate self aggregates – this is inconsistent with the positive charge that the electrostatic hypothesis asserts will prevent aggregation
* Electrostatic repulsion extends only a few nm from the surface of a particle – and the coagulant adhesive nanoparticles are many times larger than the reach of the repulsive electrostatic force
* The hypothesis that London van der Waals forces result in attachment neglects to account for the presence of water in the system. Water molecules will also be attracted to surfaces by London van der Waals forces and thus there will be competition between the coagulant and water. Thus eliminating repulsion is NOT sufficient to produce a bond between the particles. (see [hydration repulsion, page 21](https://vtechworks.lib.vt.edu/bitstream/handle/10919/30137/Chapter1.pdf?sequence=9))
* [“The theory of DLP was a great step forward in that it appeared to circumvent the whole intractable problem of many body forces through its use of measured bulk dielectric response functions. However, it must be stressed again that it is a perturbation theory. That is, it depends on the assumption that an intervening liquid between interacting surfaces has bulk liquid properties up to a molecular distance from the surfaces. This is thermodynamically inconsistent, being equivalent to the statement that surface energies (or alternatively, the positions of the Gibbs dividing surfaces) are changed infinitesimally with distance of separation. This limits the theory to `large' distances (Young–Laplace vs. Poisson again) where `large' is undefined.”](https://doi.org/10.1016/S0001-8686(99)00008-1)


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
v_Sed = 2*u.mm/u.s
Q = (v_Sed*A_Sed).to(u.mL/u.s)
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
v_avg = (Q/pc.area_circle(ID_pipe)).to(u.m/u.s) #first calculate average velocity
print('The average velocity is ',v_avg)

#Calculate pipe length
L_pipe = (v_avg*theta).to(u.m) #then multiply velocity by residence time to get the required length of pipe
print('The length of the pipe is ',L_pipe)

```

#references
[Coagulation and Flocculation in Water and Wastewater Treatment](https://www.iwapublishing.com/news/coagulation-and-flocculation-water-and-wastewater-treatment), iwapublishing
