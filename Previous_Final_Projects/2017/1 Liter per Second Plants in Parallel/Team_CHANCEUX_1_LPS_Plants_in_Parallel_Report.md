

```python
from aide_design.play import*
from aide_design import floc_model as floc
from aide_design import cdc_functions as cdc
from aide_design.unit_process_design.prefab import lfom_prefab_functional as lfom
from pytexit import py2tex
import math
```

# 1 L/s Plants in Parallel

# CHANCEUX
## Priya Aggarwal, Sung Min Kim, Felix Yang



AguaClara has been designing and building water treatment plants since 2005 in Honduras, 2013 in India, and 2017 in Nicaragua. It has been providing gravity powered water treatment systems to thousands of people in rural communities. However, there were populations that could not be targeted due to the technology only being scaled up from 6 L/s. For towns and rural areas with populations with smaller needs, AguaClara technologies were out of their reach.

Recently a one liter per second (1 LPS) plant was developed based on traditional AguaClara technology, to bring sustainable water treatment to towns with populations of 300 people per plant.

The first 1 LPS plant fabricated was sent to Cuatro Comunidades in Honduras, where a built in place plant already exists, and is currently operating without the filter attachment, also known as Enclosed Stacked Rapid Sand Filter (EStaRS). EStaRS is the last step in the 1 LPS plant processes before chlorination and completes the 4 step water treatment process: flocculation, sedimentation, filtration, and chlorination.
Having water treatment plants for smaller flow rates would increase AguaClara’s reach and allow it to help more people. Despite being in its initial stages, the demand for this technology is increasing. Three 1 LPS plants were recently ordered for a town that did not have water treatment. However, the implementation of 1 LPS plants is a problem that has not yet been solved.

This project has stemmed from the possibility of implementing AguaClara technologies to be helpful in Puerto Rico’s post hurricane rebuild effort. The goal of this project is to assess whether the portable 1 L/s plant could be a viable option to help rural communities have safe drinking water. The project models multiple 1 L/s plants working in parallel to provide for the community and plans for the future when communities would need to add capacity. For this project, the team has set 6 L/s as the design constraint. We need experience building and deploying 1 LPS plants to determine the economics and ease of operation to compare to those of built in place plants. For example, if we need 12 L/s, it could still be reasonable to use the 1 LPS plants in parallel or select a 16 L/s built in place plant if more than 12 L/s is needed. Because the dividing line between the modular prefabricated 1 LPS plants and the build in place plants is unknown, the team chose 6 L/s because it is the smallest built in place plant capacity.

Our model is based on the following:
* Standardization modular designs for each plant (1 plant has one EStaRs and Flocculator)
* One entrance tank and chemical dosing controller
* Entrance Tank accomodates to 6 L/s flow
* Coagulant/ Chlorine dosing according to flow by operator
* Parallel Layout for convenience
* Extendable shelter walls to add capacity using chain-link fencing
* Manifolds connecting up to 3 plants (accounting for 3 L/s) from the sedimentation tank to the ESTaRS and after filtration for chlorination (using Ts and fernco caps)
* Manifolds to prevent flow to other filters being cut off if filters need to be backwashed and lacks enough flow
* Equal flow to the filters and chlorination from the manifolds


Calculations follow below.

### Chemical Dosing Flow Rates

Below the functions for calculating the flow rate of the coagulant and chlorine based on the target plant flow rate are shown. The Q_Plant and concentrations of PACL and Cl can be set by the engineer and is set to 3 L/s in this sample calculation.

Chlorine would be ideally done at the end of the filtration where flow recombines so that the operator would only have to administer chlorine at one point. However our drafts did not account for that and instead lack piping that unites the top and bottom 1 L/s plants. Only the 6 L/s draft reflects this optimal design for chlorination.


```python
#using Q_plant as the target variable, sample values of what a plant conditions might be are included below
Temperature = u.Quantity(20,u.degC)
Desired_PACl_Concentration=3*u.mg/u.L
Desired_Cl_Concentration=3*u.mg/u.L
C_stock_PACl=70*u.gram/u.L
C_stock_Cl=51.4*u.gram/u.L
NuPaCl = cdc.viscosity_kinematic_pacl(C_stock_PACl,Temperature)
RatioError = 0.1
KMinor = 2

Q_Plant= 3*u.L/u.s

def CDC(Q_Plant, DesiredCl_Concentration,C_stock_PACl):
    Q_CDC=(Q_Plant*Desired_PACl_Concentration/C_stock_PACl).to(u.mL/u.s)
    return (Q_CDC)
def Chlorine_Dosing(Q_Plant,Desired_Cl_Concentration,C_stock_Cl):
    Q_Chlorine=(Q_Plant*Desired_Cl_Concentration/C_stock_Cl).to(u.mL/u.s)
    return (Q_Chlorine)

print('The flow rate of coagulant is ',CDC(Q_Plant, Desired_PACl_Concentration, C_stock_PACl).to(u.L/u.hour))
print('The flow rate of chlorine is ',Chlorine_Dosing(Q_Plant, Desired_Cl_Concentration, C_stock_Cl).to(u.L/u.hour))
```

    The flow rate of coagulant is  0.4629 liter / hour
    The flow rate of chlorine is  0.6304 liter / hour


### SPACE CONSTRAINTS

In the code below the team is calculating the floor plan area. The X distance and Y distance are the length and width of the floor plan respectively. The dimensions of the sedimentation tank, flocculator, and entrance tank are accounted for in this calculation.


```python
#Claculting the Y distance For the Sed Tank

#properties of sedimentation tank
Sed_Tank_Diameter=0.965*u.m
Length_Top_Half=1.546*u.m #See image for clearer understanding

Y_Sed_Top_Half=Length_Top_Half*math.cos(60*u.degrees)
print(Y_Sed_Top_Half)
Y_Sed_Total=Sed_Tank_Diameter+Y_Sed_Top_Half
print(Y_Sed_Total)
```

    0.773 meter
    1.738 meter


SED TANK: Based on the calculation above, the space the Sedimentation tank would take on the floor plant is found to be 1.738 m.   

![Image of Sed Tank](https://lh3.googleusercontent.com/p1raanocowKirq5nuu7_R9j0QmrkL-ZwmXQDB14wbfIGYeLaCbObV6iNNueZ1jES-VAhtrglIQpijE-3NXkhAaf7QPtTA8-ZCnRwVS6KrUppkWc1fRt1o3i9St7kPAHEO6GfJLZ5MOQwFQ7_LVAZvPZgqBjYFNb_Z2uLJcNLPx1tU7U-lldvox8AlYMOBSN7OWYe1BmtJT22DjcVUJP5DpFWR8qqSjYq1TsKp-x7h8OCUXAPsgKq9qxD53wT1nSAi3mlLjpgQiDWWmybrcYl-Rn_2VW1vKiea5JeKxwFvslweNbWVXRw9CSccDQl1gus2v85EUV9KXvdXxYs1CDwA7BoYpHJ63Ke5wrCl0uxTt30yukV4eIQUxROVphnkclJZmmkB9IrGPOTdbJV-xUt8LEHWXMMw8aPcHFr8Jwx066n4w3K75lIpqPpY2t05KAxIoAhA_lYo38H40EQdRwdo1Bt-5EdLG0d8sov8SaQFeCokNPaNBSmg1OfXaLSwcfeq7U9Y73mf_viFSNPI1yX-A-VvhvakJi_KYQu3HLm6fD8NKtGapcdnO2ZazRWsegzb6Guv8_8w2hStHPuPxuk21IBs978RkZrYdd87q5qfZh8CEE2z7gBjkr-68vpDRCHqEqEAk3asCDMLlXcDZFsrv_U9Uyi09iDmxw=w798-h660-no)

This is a picture of the sedimentation tank with dimensions showing the distance jutting out from the sedimentation tank. This distance of 0.773 m is added to the sedimentation tank diameter totalling 1.738 meters.

ESTaRS: The dimensions of the ESTaRS are set and did not need to be calculated. A single manifold can collect water from the sed tanks and send it to the EStaRS. There will be valves on the manifold system installed before the entrance to the ESTaRS to allow for backwashing. These valves can be shut to allow for enough flow to provide backwashing capacity. There will be a manifold connecting flow after filtration to equate the flow for chlorination.  

FLOCCULATOR: We want symmetrical piping systems coming out of the flocculator. There is a flocculator for each plant so that available head going into the parallel sedimentation tanks will be the same. We will have an asymmetrical exit lauder system coming out of the sedimentation tanks going into the ESTaRS (diagram).

ENTRANCE TANK: The entrance tank is set to be at the front of the plant. The focus of this project is to calculate the dimensions and design the plant. The entrance tank dimensions should be left to be designed in the future. An estimated dimension was set in the drawing included in this project. There will be a grit chamber included after the entrance tank. The traditional design for rapid mix that is used in AguaClara plants will be included in the entrance tank.

CONTACT CHAMBER: A contact chamber is included after the entrance tank to ensure that the coagulant is mixed with all of the water before it separates into the multiple treatment trains. Like the entrance tank, contact chamber dimensions should be left to be designed in the future. An estimated dimension was set in the drawing included in this project.   

WOODEN PLATFORM: The wooden platform is 4m long, 0.8m wide, and is 1.4 meters high allowing for the operator to be able to access the top of the sedimentation tank, flocculator, and ESTaRS. It would be placed in between every sedimentation tank. In the case of only a single sedimentation tank it would go on the right of the tank because the plant expands to the right.


```python
#Spacing due to Entrance Tank and contact chamber #estimated values
Space_ET=0.5*u.m
CC_Diameter=0.4*u.m
Space_Between_ET_CC=0.1*u.m
Space_CC_ET=1*u.m

#Spacing due to Manifold between contact chamber and flocculators
Space_CC_Floc=1.116*u.m

#Spacing due to Flocculator
Space_Flocc_Sed=.1*u.m
Space_Flocculator=0.972*u.m

#Spacing due to the Manifold
Space_Manifold=0.40*u.m

#Spacing due to ESTaRS
Space_ESTaRS=0.607*u.m

#Spacing for ESTaRS Manifold to the wall
Space_ESTaRS_Wall=0.962*u.m

```

The Y distance below 3 L/s is set to be as a sum of the total Y distance of the flocculator, sedimentation tank, and ESTaRS. An additional 2 meters of Y distance is added for operator access around the plant. The lengths between the sedimentation tank, flocculator and ESTarS were kept minimal but additional Y distance can be taken off between the sedimentation tank and ESTaRS. This is because the ESTaRS can hide under the sloping half of the sedimentation tank but this orientation would not account for the manifold drawn in the picture.

The total Y distance is calculated below.


```python
Y_Length_Top=(Space_CC_ET+Space_CC_Floc+Space_Flocc_Sed
                +Space_Flocculator+Y_Sed_Total+Space_Manifold+Space_ESTaRS+
               Space_ESTaRS_Wall)

Y_Length_Bottom=Y_Length_Top-0.488*u.m
```

Below are functions that can be used to design a plant based on the desired flow rate


```python
def X(Q):
    if Q>3*u.L/u.s:
        X_Distance_Bottom=X(Q-3*u.L/u.s)
        X_Distance_Top=6.9*u.m
        return(X_Distance_Top,X_Distance_Bottom)

    else:
        Q_Plant=Q.to(u.L/u.s)
        Extra_Space=2*u.m
        X_Distance=(Q_Plant.magnitude-1)*1*u.m+(Q_Plant.magnitude)*.965*u.m+Extra_Space
    return(X_Distance.to(u.m))

def Y(Q):
    if Q>3*u.L/u.s:
        return(Y_Length_Top+Y_Length_Bottom)
    else:
        return(Y_Length_Top)


def Area_Plant(Q):
    if Q>3*u.L/u.s:
        X_Distance_Bottom=X(Q-3*u.L/u.s)
        Area_Bottom=X_Distance_Bottom*Y_Length_Bottom*((Q/u.L*u.s-3))
        Area_Top=X(3*u.L/u.s)*Y_Length_Top
        Area_Total=Area_Top+Area_Bottom
        return(Area_Total)
    else:
        H_Distance=X(Q_Plant)
        Y_Distance=Y_Length_Top
        Area_Total=H_Distance*Y_Distance
    return(Area.to(u.m**2))

```

![Image of Sample 3L/s Plant](https://lh3.googleusercontent.com/V-YxrMCMg9_wiKeqH9gQ4EtY4nMhrIReoT_mRcyQ9MP-E2SBRwHoEHz55j_dOMjecPnmn3PmLlWadpa0eDVQdmpDdZX84Z0UaWprMG4Yx72_OlK1oBUFyUQTIjCvhZAMbhQst_67I-QBewCbw3U4udEvq9jg6X-v1kQ7HxMmdBz6U1sR8fkmLaLw28YRFf1DBNGg8Xay9QoMV4THIRQ68_N_UQjlfwKxohvU01u2ezVRPDHv6vCkO5J7LQ1doC_x5zEipy6xF6opSgBY2F3m9U3xYS6ivIkicvq4EpaT7P3dYuxUJ8QLgzxrR-IIzWouJFBXaqIKM83bqvlzdqJAvY9iIp9dvzkNLQwtlMJBzm-fleR2KFL88BWhH5Airzcpy40MZhUoI5hGL-u6vd3QLMGnqn4FrwWMhcy_ijQrTwdGPftokr5UAHxpliaPeCiWawKUeBmAR1sgf_TVb_PB70k9Zrx2nmwDvVZSxYiSeqW0oQJYPLRTZvOhNeTYikLbtSbK-6JuH4H0fZxDahCXFvzhMpbsj3VKi1QrBQVWF9uqqEiE3I1tBH6aelC4TZVA_kb_pXtxHzhIHQQ4_ScsISiqvHIP6ju7S4hXeioQXpKGXvjSs7vHzBH9tvR5DauC1qqlMWGQEP64HRbcO-Y0vQl2faImCoQxBuU=w693-h748-no)


This is a layout of a sample plant for three 1 L/s tanks running in parallel. Check bottom of document for additional drafts.

A platform will be in between sedimentation tanks as a way for the operators to have access to the sedimentation tanks. The platform height will be 1.4m to allow the plant operators 0.5m to view the sedimentation tanks just as in the built in place plants. The operator access requirements influence the optimal plant layout because the operators movements and safety have to be considered. The manifold will be built underneath the platform for space efficiency. The image below shows the wooden platform with 4m of length but could be truncated or extended to depending on the situation. The last image shows the platform in between the sedimentation tanks in the 3 L/s sample plant.

![Image of Wooden Platform](https://lh3.googleusercontent.com/1z5hX0-m1B3zu8efVM1sCZ4_IkL-zZpqJFyW8wcMnI4FnQNVpA-cC57XayAvhaNqeX5fpH7H31KV0E46_h9XWuKrct8dYFw1YcdQRzLuJQRzB9uYBqm7cJ8E1Cwsk2dtqlASuEu9SrVeaRRwKz6ttEpko4woo5tCJDY-744e6CsGU_Ss4fQb-Xc8SOIHl86VBWaTv5R6IRGxKMrU58pstrsaYvxzd0LG2epTFfYkEgBi2StSJVqlYlvyXniLC9UMYbTOqgfRQlKM6drWkyxH4zkIZK3YuMOkXjQjvdlBvdyViBQQEKGue9at4hg2gM6-_VarCpPgWKeg9WLX7d2BkguIu6hsqnfdElIlnnODLRNS7lDPMeX6OK0D1s2DrpBrAGIILWwT1vswlHxDBvz7JGK5a4NacDJANWJr9WUyImCx5lyQa5Shw4Y02yVH1KwfVLzq_JmcmchdRKY12eI6VIa-PRP777ntAiwB-aU94swZ63lghoL6ELIQ1jjycXs8QogpKqL_cXOve79vlZrf1eDaOFSH5094i7_RdfLGKkKpsKOUJv_5W2gWfmGk15NL0u0lscmNT71ICL60iogp_6SWpLpaQL750Q3cb7dIPcnoiQoDDnLOSmHXRgI_3YPHacvHp-ZPL-ITJD7L2mIjpSXJDepvpbOnZms=w833-h702-no)

Wooden platforms would fill up the space in between sedimentation tanks to allow for operator access to the top of sedimentation tanks, ESTaRS and flocculators.

![Image of Wooden Platform in Sample 3 L/s Plant](https://lh3.googleusercontent.com/qJuHz_JPzzyHVT-PpmQDcB6xCt_v-iqY4ADhb3MMK7mCJLTLaW41OtpqxTsNYosQGst_COv1K6ojb0HuNCJy87puD8GbvgmAK6qk31jAZE-B5lZrt4cIilgY2taCjjmT5YrDO35204mTgYIVkFGOnqoONidU4TqVZXyMX6qAzh3Yz8gqHfLGzZCWf1IGPGn2io9NSeK31OPaehKmWOKKZEQ0whzr0LcN8qDvq8gbiP1ms5Z8YljsJYj6k0GPkInNAAxs_4uKk41O9bGZuV7HeeUifv0u3oLGMqcAJI8fc12fd2BWROfeT9MadiXsDLXdMsyXG6PI0DVfhG_TDjL3QTMt5WVY89q_Gy24bMAlzAPhqoot6WtSGfzpxic3ioT6zCZQT9_y3stvWZPZfAXZqw6wjNiLJKh9MqaG9J_nbzfssNr45diqTxGFavwMLB9tJ_jNKHVrfQLv6vBZXx4fAUsfqiLUC0rsSfgx0KRvFjvR8LHFCvf5L7ncpFOzdSGrQnFS9IumBSw_0r1H4R9zF6_3hxw2wIh-s-JE6l1jyDfaWzS3WL_xtn8kuyy1Q0ds1UQCArtXX2VJ8J9cKkLgrPHy_WapMyKWtgEJs9B0JnpdKGsQX2BFJ6ZYcUV_Tcrri2hyVjkAisn7q7CfJOhgE75qqM1dPnbTJ9k=w1275-h742-no)


### Adding Capacity
When adding capacity up to plant flow rates of 3 L/s, vertical distance will be constant so adding capacity will only change the horizontal distance of the plant. We define a set of flocculator, sedimentation tank, and EStARS as a 1 L/s plant.

After the capacity of the plant reaches 3 L/s, additional 1 L/s plants will be added to the bottom half of the building, using a mirrored layout as the top half of the building. The only difference between the spacing is that the additions no longer need another entrance tank so the width of the bottom half of the plant is shorter than the width of the top half. This was done instead of simply increasing the length of the plant each time capacity was added because the length of the pipe between the contact chamber and the farthest flocculator would become increasingly large. This addition of major losses would cause different flow rates between the farther 1LPS plant and the closest one.

The following function will only account for adding 1 L/s plants one at at a time



```python
def Additional_Area(Q_Plant,Q_Extra):
    if (Q_Plant+Q_Extra>3*u.L/u.s):
        X_Distance_Extra=X(Q_Extra)
        Y_Distance_Extra=Y_Length_Bottom
        Area=(X_Distance_Extra*Y_Distance_Extra).to(u.m**2)
        return(Area)
    else:
        Q=Q_Extra.to(u.L/u.s)
        Horizontal=(Q_Extra.magnitude)*.965*u.m+(Q_Extra.magnitude)*1*u.m
        Vertical=5.512*u.m
        Extra_Area=Vertical*Horizontal
        print('Extra length that has to be added is '+ut.sig(Horizontal,4))
    return(ut.sig(Extra_Area,2))
```

### ESTaRS
The total surface area required for the ESTaRS filter is simply a product of the area one ESTaRS requires and the flow rate coming into the plant. The surface area required for an ESTaRS was measured in the DeFrees lab. It is approximately a square meter.


```python
ESTaRS_SA=1*u.m**2/u.L
def Area_ESTaRS(Q):
    Q_Plant=Q.to(u.L/u.s)
    Surface_Area_ESTaRS=(ESTaRS_SA.magnitude)*Q_Plant.magnitude
    return(Surface_Area_ESTaRS*u.m**2)

print('Surface area required for the ESTaR(s) is',Area_ESTaRS(Q_Plant))
```

    Surface area required for the ESTaR(s) is 3 meter ** 2


### Flocculators
The total surface area required for the ESTaRS filter is simply a product of the area one ESTaRS requires and the flow rate coming into the plant. The surface area required for an ESTaRS was measured in the DeFrees lab. It is approximately a square meter.


```python
Flocc_SA=0.972*u.m*0.536*u.m*u.L/u.s
def Area_Flocc(Q):
    Q_Plant=Q.to(u.L/u.s)
    Surface_Area_Flocc=(Flocc_SA.magnitude)*Q_Plant.magnitude
    return(Surface_Area_Flocc*u.m**2)
print('Surface area required for the flocculator(s) is',Area_Flocc(Q_Plant))

```

    Surface area required for the flocculator(s) is 1.563 meter ** 2


### Manifold Headloss Calculations

The amount of headloss has to be minimal so that the amount of head availible coming out of the exit launder is enough to drive water fast enough to fluidize the sand bed in ESTaRS. This fluidization is required for backwashing the filter. Since the calculation for 4 inch pipe has a headloss for less than 1mm we conclude that the manifold is economically feasible. Any futher increase in the diameter of the manifold would become increasingly expensive.



```python
SDR = 26
SF=1.33
Q_Manifold = 1 * u.L/u.s #max flowrate for a manifold
Q_UpperBound=SF*Q_Manifold
L_pipe = 5*u.m #Length sed tank to it’s ESTaRS
K_minor_bend=0.3
K_minor_branch=1
K_minor_contractions=1
K_minor_total= 2*(K_minor_bend+K_minor_branch+K_minor_contractions) # (two bends, two dividing branch, and two contractions)
# The maximum viscosity will occur at the lowest temperature.
T_crit = u.Quantity(10,u.degC)
nu = pc.viscosity_kinematic(T_crit)
e = 0.1 * u.mm
Manifold_1LPS_ID=4*u.inch
Headloss_Max=10*u.mm

Manifold_Diam=pc.diam_pipe(Q_Manifold,Headloss_Max,L_pipe,nu,e,K_minor_total).to(u.inch)
print(Manifold_Diam.to(u.inch))
print('The minimum pipe inner diameter is '+ ut.sig(Manifold_Diam,2)+'.')
Manifold_ND = pipe.ND_SDR_available(Manifold_Diam,SDR)
print('The nominal diameter of the manifold is '+ut.sig(Manifold_ND,2)+' ('+ut.sig(Manifold_ND.to(u.inch),2)+').')

HLCheck = pc.headloss(Q_UpperBound,Manifold_1LPS_ID,L_pipe,nu,e,K_minor_total)
print('The head loss is',HLCheck.to(u.mm))
```

    3.34 inch
    The minimum pipe inner diameter is 3.3 in.
    The nominal diameter of the manifold is 4.0 in (4.0 in).
    The head loss is 8.393 millimeter


# Drafts of 1 L/s Plant to 6 L/s Plant

![Image of Sample 1 L/s Plant](https://lh3.googleusercontent.com/vOmHWVvkOfpIfaNClasDE0f0aB0mTcMdVX020OsMH476zHjly2ZctM0Izli8-2TR5K4XsMdtVjhlgBtj5lQx_RksotACGf2EoBNn_h0cVoaiY79hoXAN3y6CFv9a9zTb0FKIXCImh0rX4AKczHK_39JXx0kwTgovXm1bwFo6PgOav8nLfJbCqgIrpgyrsnyF_uNM_kms6HEHf1iwW9x_XF0PXNErB7mpPRNWY_jSGQnLiQUaIUlATBo3TM8o18zYzN9WczPHEX1htXUcZAt3ccJqC3hGn5gbOHSZ_e8XjhlFB03PhuLuB7EOQZqsIU-g9lLKN3fzqS7eQFD8Igp819JlojZhiJAbKh4yAitheuqShzduiEzyKKSrakq1GLdUnvjV69uM8Y3RZMpTJllNzWRjQVX1m6a8ntGwfDLjMu1DMvIWUMFfASwIUXnChOpgBPJfHO32shzW5aPIFtwHC3labmdho_RiWLaSspgNE-mdiuTVS_OinrzD92BZ3uNNh2YaXXwPCFdVhdUIBKB2wqq1daHB_FckbUSaRUZRO3TivHpyI_QZ4x9u2oRN15y8GcPyva6hulgG3Sdswebi44uKUraNeOKWLfQbZhYVUCSfPx5IH2iVHHTqHaA4nxWLi__lQhY9mfVH3EJ_0jqrXcsxXXjSSfSSi6o=w366-h722-no)

A sample 1 L/s plant. The red t's indicate where the piping system can be expanded to include more 1 L/s systems. Additionally the t would be covered by a fernco cap so that the pipe can be removed when the plant is adding capacity. See cell below for pictures of manifolds with caps.  

![Image of Sample 2 L/s Plant](https://lh3.googleusercontent.com/680lSRhg_LyDPOdNU8rphmoZi8-uOlX-FyMNOYBDfAGUSdkLUfmyxHBtwzlk9P8osyvCKmsD5J53_wwjL2sJQ99d0s-o41ONMhG5Sg6rRgX-nVY2mL4_a7OPrVYcM7NILp16NOVLnutWSDSZC_eXVHqfZjCQPRdKTN5L4j76-vl58QsKJnf_kYJXzmVuNlDTj2sKC53uRsQXrmJFVgBdYjrGn7usUqR6VEB4_1u5wCm4fpzbTnmH7O6KdwkKn7xaaEUvwx-qqCEsStbxG7UgB2lvv9xqd5Kd9r7jr83mu4If-qZB0ZfycvAFOwGfvrRi8r-ZaAefnSX59TkxehfAA6qgCnSsCoXWi1L0crTP2B4XYCdsvG4DD8Gvp6A5G34JOSsnMj56WqVJ1e-NH8qPqv7uF0X5_C23LuE1258E8ig4bBPSbrxc-PVnB_i0PjXxwDofplAS4EYflwkUaCdD8pzDORSokk1RwP4KPRaFBmSJwnuW8xRJJCVVJ_l7UL1ioHGpYHvUBCvOrYVCxGNzmot0OKPWkoefK23XzEMRkkoGOQXSf_CuM7S9vADNr2J9UZoO3CF-hLUNvyEtJbPFYCMGMLEe4x_ZMAEDcOmYtcXPPVtUtxcvEMZnL5vYPHqS3y_qGrkoNAx1h8fMtN7Q9JKHKLQj8gzHJuE=w524-h746-no)

The sample 2 L/s plant. The red t's indicate where the piping system can be expanded to include more 1 L/s plants. Additionally the t exit that isn't connected to any piping would be covered by a fernco cap so that the pipe can be removed when the plant is adding capacity.

![Image of Sample 3L/s Plant](https://lh3.googleusercontent.com/V-YxrMCMg9_wiKeqH9gQ4EtY4nMhrIReoT_mRcyQ9MP-E2SBRwHoEHz55j_dOMjecPnmn3PmLlWadpa0eDVQdmpDdZX84Z0UaWprMG4Yx72_OlK1oBUFyUQTIjCvhZAMbhQst_67I-QBewCbw3U4udEvq9jg6X-v1kQ7HxMmdBz6U1sR8fkmLaLw28YRFf1DBNGg8Xay9QoMV4THIRQ68_N_UQjlfwKxohvU01u2ezVRPDHv6vCkO5J7LQ1doC_x5zEipy6xF6opSgBY2F3m9U3xYS6ivIkicvq4EpaT7P3dYuxUJ8QLgzxrR-IIzWouJFBXaqIKM83bqvlzdqJAvY9iIp9dvzkNLQwtlMJBzm-fleR2KFL88BWhH5Airzcpy40MZhUoI5hGL-u6vd3QLMGnqn4FrwWMhcy_ijQrTwdGPftokr5UAHxpliaPeCiWawKUeBmAR1sgf_TVb_PB70k9Zrx2nmwDvVZSxYiSeqW0oQJYPLRTZvOhNeTYikLbtSbK-6JuH4H0fZxDahCXFvzhMpbsj3VKi1QrBQVWF9uqqEiE3I1tBH6aelC4TZVA_kb_pXtxHzhIHQQ4_ScsISiqvHIP6ju7S4hXeioQXpKGXvjSs7vHzBH9tvR5DauC1qqlMWGQEP64HRbcO-Y0vQl2faImCoQxBuU=w693-h748-no)

The sample 3 L/s plant. There are now no more t's that can be extended because the manifold was designed for up to 3 1 L/s plants. Further capacities are added on the bottom half of the plant like in the next 3 pictures.

![Image of Sample 4 L/s Plant](https://lh3.googleusercontent.com/jLNinHPmzV-U2WmrbAJlOgoR4SUHmjdG4spKciUZpJIk504L8JARaH2PUQAipqltrbjce1zGXlsO8ag9jctcR4seel6p9HdexnkrANXt0NO4gMGZAL04xMKl1EWDDiKTrwNr1Om-3VglxvAyS07Mz8cH37FD9MbRTaJzYaH--t2xC7Qk6BbyV_kaspNQIvaohz5Ce39HTBvfqm2mvJXvX9aTZpiJ5tEbSWDOFBm9wfLMUIlqWjjOG5awFN3TTx05H8ifQA6A4f8GUoWUpONKZweWX-LT04nWI_nwZZ0phYZ76P59g6yVsBSTKQP8aMrQ6LN32jx5JCB2tnpJTLe9LBDw5m_g03F4VaXUWAG0xNeCjNK3D_QpZdBK5jI2VIf2GeQYX-udo_NOTKbqVm_dsACQiK4-k5qlu2GwiRehMr33L0RYLhyQ_j2pKablJ15yZkmxdYEvinjiV-fmTVMUdcSQVwPBRnUd5PmXZNsTQ9TY7oG2NJQ93VPen6XTj_ntP93QbtrRkM5Ido4Y9dS9PcN7gtnYRygF7AOFcYF_PZ_lQ6er2fwZGIabYNKGPTO9SYKW4bj4Azf0kDJVCWilaYgyAc1JSqYbeGSziqO4nbztYHebUhbnBm7Afd4fb-D_-Y4ixOn_02imeI10V39fN4TPGdwXLo1RWkY=w443-h753-no)

The sample 4 L/s plant. Like in the 1 L/s plant the red t's indicate the start of the 2nd manifold system.

![Image of Sample 5 L/s Plant](https://lh3.googleusercontent.com/s9mGAe84mRq88k-YgrdpcIdBlsmHjJWG963OY5eRWHZJFD6vHgkXqqILnqltZTaZ7DaVCGke-8MuVgI5w6ACJFfJPII27ZqWm7SN5K6JuvazJk5wjWJ8F5EI1vZKiTvG5iGL13TJOjWcyN-k1Bqa0H05SnXakpP46Cx4bk3TvTBBSKwfLe2Vz_a6dOpwAWq_YXdXtJb0UZ7LKviJQrGTCWmmarRdiJE54ojmVmd5y0x-0Fdo2XbgTOk3x1BvDCQEMjgof16jFgM-mKyzOB8jBsNx4vJHNr_uikZt2viZ_hLiPG3OAJjt5ARDR7DrLPbvrWrpAfSAb2yb-bKIoZnr8rd5VEXPDDtQfZX1FYiKEgcgwYzbiV5npkt_1Wtdlh6i1Rbs24stxSWIhp_KCxb3g7soCQ5TbyS5kKjcR0Rctxq-_7K1eTz_LZ6gt7Zg1c3oYzf3eZM0UQvcbwpsSnSqXwCR3XMOySWJpmpAYRS74qpLN0-UpLJsK8A4_I_6cKn-5vDW2ppNbn-NlwoAP0CtA3ArWFd00IGFypk9Tqj-SFwx7q3LYoZi3CzdXHz0kLC5Fu-4oJxkTQVxV01HitC2tym4N730Bq9ucAPvMjSQ-nBqp74IInh8klJ8hDdKj9ibkeb87xDScKOOJaAP1d10BE__6DST00aUmCM=w476-h816-no)

The sample 5 L/s plant. The length (x-direction) is extended by the diameter of a sedimentation tank and one meter like in the top half of the plant. However the width of the bottom half is slightly lower because it can use the already built entrance tank used for the first 3 L/s systems.

![Image of Sample 6 L/s Plant](https://lh3.googleusercontent.com/gZmKRSfcJqXeg5z8neBhowTt9uldRwsMmXfMRdP0RwobzmrpCgnU0ZQP8yBecykp-dJzJvziPApaYK0IgQDHY3ZGRfin-e_5S6CjD09Ur0IEzSJvAHsB1Nh3Df9OwN11aIPR7qcbNr7PP9-DLK0p66GZlaqYtC1xpB-Nm7e964ph-p2koh6Gx6A5_waWGPtwGPn3D1Zj23llXZY8dS9h6d8obv3pvtfHYdhtXm9_XQtcU8vPVPwLiycqsn1YRuJ1Es0VBroD1flT_vKR3SX4rhkCvBCpibOpw7Yd2FSG5WndORJ7emOx0hSgcsihHelSh_8qx_IONfa_p63TsOqz69LgtuO4Vw1Yc7kzW4MEfpEIaD23oL7G4hARl-MctaXZHbFQbz7cj7EpWO0HBSfe2w-xXecyQCYWfBU76JVQp4j0nIz_fVj7q7wmes-tx9H1cZS573zSE6qMmv4B_hS5x5ChcdlrrWXgmMliWmhAGj7nILc5jL1nONxysZ5pZJ6NI6WZHHgnOA15_jF8AZpVc0VZ1PP-hHppZ2Ti7H3X4A7ioRrgayQoEbnYeZnbJybN73cDDvv7T9cAARdc2lQyVXVrWsraI7RbWHRzXWoHe5URBEzZh9YwE_etDyoY20B12dl6JyfianC31YeHJpiafo5EteQkCZ2U2GA=w543-h814-no)

The sample 6 L/s plant. The building is now at full capacity with an area of 91.74 m^2. The flow reunites to allow for chlorination to be administered at one point.




# Manifold Drafts

![Sample Manifold with 1 L/s](https://lh3.googleusercontent.com/RsMmKy_4KN5gcDDGpQtLyy4DU08QMxCoa55mIlPH5sNCzlE5lbuBLXeiNG-D8eWGqPx7aQuHewRx8iyIg07FZxUl_CPBQo8oDxFkqwK_5dbitdD6ZpyDqLALo6w_XqtnwcJ8YFjkLjiY30cGOTRMpkvdLv3fPbbsUOrKq3PnU7w8AtG-iwwAqX6Y_biCx_unSFe6DrAJHKYSa9kF0E13ysErqHZ5F252uaT6rm_EHOM7_LDsjMQnvh69bTn7jYacVkoVI6TPNRyMXuH9s9-n97VvgVIiZrrhUMedfjERZbs5Vnq9SD4h-xXfiHsNXWFa0qMd1gHTSGggZhkc3881d9TLfPSe09Fj5M_rDaPoOnfdeYHSTWSeMwVvpukVVAj04bENymvrmlv096DQyh2-CSClvaoSSPpezWHQUhpv-1cqZMla1PEJxcLOK5lkVg1crnb0lLs8FOxerstXBIo6LgNgHlqSNodcnemaMJcNkQDgFfoTAv1oILlIpitDM9thDsw27zD2pLkxzHGWG9TTa8A8G40lT1ZZ4EZ4KBkD-DcKRkR7LanbbUnEO7Uxn97Wigca9h_yfflzxt1x16Yf39ZtwbxjL8s5X6_MuMBAR6WFT-TPkg4tPztkkLSyCoLhtEcSqGDTCFEt5-9f-Rs6Jog-TtIUEHTN_dU=w692-h724-no)

The manifold with 1 L/s. The elbow at the top is connected to the exit launder of the sedimentation tank. The flow goes from the exit launder into the reducer which is not yet connected in the draft to the ESTaRS. The removeable fernco cap that allows for further expansions of the manifold pipe system can be seen in the picture.

![Sample Manifold with 2 L/s](https://lh3.googleusercontent.com/OvySUVwaHjK581j2MFYvGfqTaz-ixQVdzZEk3Y7kxpsnl6EBxxhdckYc74NOiP6h_CKETRMY6gUuYnMz1BEWQtpWRHw3GZQXJ1BVriyIkite0n9qml6h3Z-gv6cyhtfCGqFHKUsOjKvQaMnmkn0PePuyQnmtRc-fozf8HzVTbvyQszkKp_MX16noVLBk8hHa2e-W1tCWYDJhjOrV2Mf8B3br2MEQvfFZ4t4BJZ7wrqIXAES2RwWAJjDf1fRSXbzSiaWAfgpGurip1rDzje2KthNzTaYPMqQrkwASF6K12i1KRnmasSrxkLquQLYuKcWfIw-X1ZafWt5NMQFBrbRE6KV1RnYT0czOLXLCrWREs21g0nPBLAxd-Z37muaSxkoI3M14cYQp96KDHpUHGSlLCRxewpOPkixNDs1OrvivKa7khHQEO08EijTakXfxGGuzZQIIgdbA-HruRrHslWdxE6T_Idw8auDxv555-FjJEaA0RH_8miInQ1g0-vthxgREWLTu4T1cgpXW92YdQRQJ5vLoUtIUo_QU8XsCZC2VUe3x32rFVOBm6--cchodCuUyHLvsszR1QFV_sXMg1yn7N6Czezaqev6OEa7ox8J69LaoWLSNZtlHicjD-o2Z2Su1d-S7EoLvObU7baGg9dAbu_WR9d2ZeJgaknc=w873-h765-no)

The manifold with 2 L/s. Again a fernco cap is used to allow for future expansions up to 3 L/s.


![Sample Manifold with 3 L/s](https://lh3.googleusercontent.com/15gWXhAqF-rKkFNxKsdT2Vv7HzsEg4jrewnjyNCiOw0qhEa66_wmgNYj7apCWUyZuNO_M841Enx9KVYAO8F73EX_QvwhcRgodkKeCVU_H9xDcrhO9w38irozRd8bSm_oiJeB_Q3FIBRIHVcyqm1g0g1qGi28_MP0DGBs6Boi9Qy7aSP96tSrnnR1jNvq8aNRIzEUUp6vgmHIQ4pWvG3utB7S2cMhqztagFBP1WRJ21-cK6E6lkuhtIzMu-uAMQVZkHMJlrAN8nZEc4Jroyk_qa56qkPQQs4wXgvOgmzYySRJlwHk8bEiT-1xMxqdM3Cd4hNzpnIAVwsWutuf0gmqSyS9jqflYnGKVVMYLAJZtgP7oOBWogwiReiH1q_LCPXorHAJyXjqePX-ojDn1QUuFWOHOuDvvmCqsqo_dmpCFSAToJYXOitX2FOPVNInu4eBsud9zV0DXRNWqKMd07lQneEJStoeDxqNGTjhEjCn4fWc0kbgybwgAcgpotTGCdYiibIjKCPAB1peb5E5wnUawTUkoUy18tZe5pIxcZUwAXp-tftufN8xIsO6VUtQVb5yODx2cOz_xJvg6T6JqawEeoJFMSRUBKl7lTaSrnv2M9PqVK8RjLtDX1jByobJ1BJEDlUCGw6Vjr_VqzWLyTozr3AJ0xacVb55KxY=w1063-h749-no)

The manifold with 3 L/s. Here there are no fernco caps because the manifold is designed for up to connections with three 1 L/s plants.
