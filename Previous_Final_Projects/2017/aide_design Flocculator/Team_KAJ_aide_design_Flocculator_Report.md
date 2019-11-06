
### KAJ Capstone Project

Alyssa Kirsch, Ken Rivero-Rivera, Jillian Whiting

# Optimizing Flocculation Systems

Introduction: Our challenge is to create python functions (to incorporate into aide_design) which optimize design parameters to make a hydraulic flocculation system highly efficient with respect to energy. These parameters include headloss, residence time, baffle spacing, and number of baffles. We will be referencing the MathCAD code created by the AguaClara Design team. We improved the code by incorporating the H/S ratio and new method of determining energy dissipation and make the code more user-friendly by improving flow and variable naming.

<img src="Honduras_Vertical_Flocculator.PNG">



### Import Python Packages


```python
#Here we import all of the packages that we will be using for this design challenge

#import math

import math

#from scipy import constants, interpolate

import numpy as np

import aide_design.utility as ut

from aide_design import physchem as pc

from aide_design import expert_inputs as exp

from aide_design.units import unit_registry as u

from pytexit import py2tex
```

## Flocculator Code

### User Inputs

Change these inputs to reflect the parameters which define your system.


```python
#Flow_Plant can be between 10-100L/s.
FLOW_PLANT = 50 * u.L/u.s

#These values are typical for a AguaClara plant.
HEADLOSS = 40 * u.cm
HEIGHT_WATER_END = 2 * u.m
LENGTH_FLOC = 6 * u.m
LENGTH_ENTRANCE_TANK = 1 * u.m
THICKNESS_FLOC_DIVIDING_WALL = 15 * u.cm
WIDTH_SED_INLET_CHANNEL_PRE_WEIR = 30 * u.cm
COLL_POT_FLOC_BOD = 37000 * u.dimensionless
```

### Flocculator Efficiency

These H/S constraints allow one to construct an efficient flocculator which does not waste space between expansions.

$$\Pi_{VCBaffle}=\frac{1}{\sqrt{K_{Minor,FlocBaffle}}+1}$$


```python
RATIO_VC_BAFFLE = 1/(np.sqrt(exp.K_MINOR_FLOC_BAFFLE)+1)

RATIO_HS_MIN = 3
RATIO_HS_MAX = 6
```

### Volume Constraint -  Energy Dissipation with max headloss

Calculate the size the flocculator can be while meeting requirements for energy dissipation rate.

$$E_{DissAvg}=G_{Bar}^{2}\,\nu$$

$$V_{FlocBod}=Q_{Plant}\,t_{FlocBod}$$


```python
#Energy dissipation was calculated according to the method described in CEE 4540, Fall 2017.
G_BAR = (pc.gravity * HEADLOSS) / (COLL_POT_FLOC_BOD * exp.NU_WATER)
ENERGY_DIS_AVERAGE = G_BAR**2 * exp.NU_WATER
TIME_FLOC_BOD = COLL_POT_FLOC_BOD / G_BAR
VOLUME_FLOC_BOD = FLOW_PLANT * TIME_FLOC_BOD
```

### Channel Width and Number of Channels

<img src="Flocculator_Top_View.PNG">

Use volume and efficiency to calculate channel width and number of channels.

$$W_{Floc,MinEff}=\Pi_{HS,Min}\,\left(\frac{K_{Minor,FlocBaffle}}{2\,H_{WaterEnd}\,E_{DissAvg}}\right)^{\frac{1}{3}}\,\frac{Q}{H_{WaterEnd}}$$

$$W_{FlocChanHL}=\frac{V_{FlocBod}}{H_{WaterEnd}\,\left(N_{FlocChan}\,L_{Floc}-L_{EntTank}-T_{FlocDivWall}-2\,W_{SedInChan,PreWeir}\right)}$$

$$N_{FlocChannels}=\frac{\frac{V_{FlocBod}}{W_{MaxSheet}\,H_{WaterEnd}}+L_{EntTank}+T_{FlocDivWall}+2\,W_{SedInChannel,PreWeir}}{L_{Floc}}$$


```python
## Max channel width is the the width of one baffle sheet
WIDTH_MAX_SHEET = 1 * u.m

## Min width is based on the half the width of the baffle sheets
WIDTH_MIN_SHEET = WIDTH_MAX_SHEET / 2

WIDTH_FLOC_MINIMUM_EFFICIENT = RATIO_HS_MIN * (exp.K_MINOR_FLOC_BAFFLE / (2 * HEIGHT_WATER_END * ENERGY_DIS_AVERAGE)) \
    ** (1/3) * (FLOW_PLANT / HEIGHT_WATER_END)
WIDTH_FLOC_MIN = max(WIDTH_MIN_SHEET,WIDTH_FLOC_MINIMUM_EFFICIENT.to(u.m))

NUMBER_FLOC_CHANNELS = np.ceil((((VOLUME_FLOC_BOD)/(WIDTH_MAX_SHEET * HEIGHT_WATER_END) + \
    LENGTH_ENTRANCE_TANK + THICKNESS_FLOC_DIVIDING_WALL + 2 * WIDTH_SED_INLET_CHANNEL_PRE_WEIR) / LENGTH_FLOC)\
    .to(u.dimensionless))
WIDTH_FLOC_CHANNEL_HL = VOLUME_FLOC_BOD / (HEIGHT_WATER_END * (NUMBER_FLOC_CHANNELS * LENGTH_FLOC - LENGTH_ENTRANCE_TANK \
   - THICKNESS_FLOC_DIVIDING_WALL - 2 * WIDTH_SED_INLET_CHANNEL_PRE_WEIR))
WIDTH_FLOC_CHANNEL = max(WIDTH_FLOC_CHANNEL_HL,WIDTH_FLOC_MIN)
NUMBER_FLOC_CHANNELS
```




2.0 dimensionless



### Obstacles

Determine whether obstacles are needed and what spacing makes the flocculator efficient. The obstacles will be made to have the same VC as the 180 degree turn around the baffle to make calculations easy.

$$N_{FlocSpaceObst}=N_{FlocSpaceExpan}-1$$

$$H_{Floc,Obst}=\frac{H_{WaterEnd}}{N_{FlocSpaceExpan}}$$


```python
HEIGHT_FLOC_OBSTACLE_MAX = (exp.K_MINOR_FLOC_BAFFLE / (2 * ENERGY_DIS_AVERAGE))**(1/4) * (RATIO_HS_MAX * FLOW_PLANT / \
    WIDTH_FLOC_CHANNEL)**(3/4)
NUMBER_FLOC_SPACE_EXPANSIONS = np.ceil((HEIGHT_WATER_END / HEIGHT_FLOC_OBSTACLE_MAX).to(u.dimensionless))
NUMBER_FLOC_SPACE_OBSTACLES = NUMBER_FLOC_SPACE_EXPANSIONS - 1
HEIGHT_FLOC_OBSTACLES = HEIGHT_WATER_END / NUMBER_FLOC_SPACE_EXPANSIONS
```

### Baffle Spacing

<img src="Flocculator_CAD.PNG">

Use geometry of channels to determine baffle spacing in order to keep the flocculator efficient.

$$S_{FlocBaffle}=\frac{L_{Floc}-N_{FlocChanBaffles}\,T_{FlocBaffle}}{N_{FlocChanSpaces}}$$


```python
SPACING_FLOC_BAFFLE_MIN = (exp.K_MINOR_FLOC_BAFFLE / (2 * HEIGHT_FLOC_OBSTACLES * ENERGY_DIS_AVERAGE))**(1/3) * \
    (FLOW_PLANT / WIDTH_FLOC_CHANNEL)
NUMBER_FLOC_CHANNEL_SPACES = np.ceil((LENGTH_FLOC + exp.THICKNESS_FLOC_BAFFLE)/((SPACING_FLOC_BAFFLE_MIN + \
    exp.THICKNESS_FLOC_BAFFLE).to(u.m))).to(u.dimensionless)
NUMBER_FLOC_CHANNEL_BAFFLES = NUMBER_FLOC_CHANNEL_SPACES - 1
SPACING_FLOC_BAFFLE = (LENGTH_FLOC - NUMBER_FLOC_CHANNEL_BAFFLES * exp.THICKNESS_FLOC_BAFFLE) / \
    NUMBER_FLOC_CHANNEL_SPACES
```

### Number of baffles and expansions 

Based on spacing and geometry, one can calculate the number of baffles in a central channel. The first and last channels have different numbers of baffles due to the entrance tank and entrance into the sedimentation tank, respectively. After the total number of baffles is calculated, the total number of expansions can be determined.

$$N_{FlocBaffles}=N_{Floc,FirstChanBaffles}+N_{Floc,LastChanBaffles}+N_{FlocChanBaffles}\,\left(N_{FlocChan}-2\right)$$

$$N_{FlocExpan}=N_{FlocSpaces}\,N_{FlocSpaceExpan}$$


```python
## First channel must account for entrance tank being in the channel
NUMBER_FLOC_FIRST_CHANNEL_SPACES = np.floor((LENGTH_FLOC - LENGTH_ENTRANCE_TANK - THICKNESS_FLOC_DIVIDING_WALL + \
    exp.THICKNESS_FLOC_BAFFLE) / (SPACING_FLOC_BAFFLE + exp.THICKNESS_FLOC_BAFFLE))
NUMBER_FLOC_FIRST_CHANNEL_BAFFLES = NUMBER_FLOC_FIRST_CHANNEL_SPACES

## Last channel must accout for sed tank inlet
NUMBER_FLOC_LAST_CHANNEL_SPACES = np.floor((LENGTH_FLOC - WIDTH_SED_INLET_CHANNEL_PRE_WEIR + exp.THICKNESS_FLOC_BAFFLE) / \
    (SPACING_FLOC_BAFFLE + exp.THICKNESS_FLOC_BAFFLE))
NUMBER_FLOC_LAST_CHANNEL_BAFFLES = NUMBER_FLOC_LAST_CHANNEL_SPACES

## Total
NUMBER_FLOC_SPACES = NUMBER_FLOC_FIRST_CHANNEL_SPACES + NUMBER_FLOC_LAST_CHANNEL_SPACES + NUMBER_FLOC_CHANNEL_SPACES * \
    (NUMBER_FLOC_CHANNELS - 2)
NUMBER_FLOC_EXPANSIONS = NUMBER_FLOC_SPACES * NUMBER_FLOC_SPACE_EXPANSIONS
NUMBER_FLOC_BAFFLES = NUMBER_FLOC_FIRST_CHANNEL_BAFFLES + NUMBER_FLOC_LAST_CHANNEL_BAFFLES + NUMBER_FLOC_CHANNEL_BAFFLES \
    * (NUMBER_FLOC_CHANNELS - 2)
```

## Final Parameters

The actual plant parameters are determined below based on constraints for integer numbers of baffles, channels, etc.

### Collision Potential

$$G\,\theta_{Floc}=G\,\theta_{FlocExpan}\,N_{FlocExpan}$$


```python
CP_FLOC_EXPANSION = np.sqrt(HEIGHT_FLOC_OBSTACLES * exp.K_MINOR_FLOC_BAFFLE * FLOW_PLANT / (2 * exp.NU_WATER * 
      WIDTH_FLOC_CHANNEL * SPACING_FLOC_BAFFLE))
CP_FLOC = CP_FLOC_EXPANSION * NUMBER_FLOC_EXPANSIONS
```

### Fluid Velocity

$$V_{Floc}=\frac{Q_{Plant}}{S_{FlocBaffle}\,W_{FlocChan}}$$


```python
VELOCITY_FLOC = FLOW_PLANT / (SPACING_FLOC_BAFFLE * WIDTH_FLOC_CHANNEL)
```

### Headloss

$$Headloss_{Floc}=\frac{K_{Minor,FlocBaffle}\,v_{Floc}^{2}}{2\,g}\,N_{FlocExpan}$$


```python
HEADLOSS_FLOC = exp.K_MINOR_FLOC_BAFFLE * VELOCITY_FLOC **2 / (2 * pc.gravity) * NUMBER_FLOC_EXPANSIONS
```

### H/S Ratio

$$\Pi_{FlocHS,Min}=\frac{H_{FlocObst}}{S_{FlocBaffle}}$$

$$\Pi_{FlocHS,Max}=\frac{H_{FlocObst}+Headloss_{Floc}}{S_{FlocBaffle}}$$


```python
RATIO_FLOC_HS_MIN = HEIGHT_FLOC_OBSTACLES / SPACING_FLOC_BAFFLE
RATIO_FLOC_HS_MAX = (HEIGHT_FLOC_OBSTACLES + HEADLOSS_FLOC) / SPACING_FLOC_BAFFLE
```

### Energy Dissipation Rate

$$E_{DissFloc,Avg}=\frac{K_{Minor,FlocBaffle}}{2\,H_{FlocObst}}\,\left(\frac{Q_{Plant}}{W_{FlocChan}\,S_{FlocBaffle}}\right)^{3}$$

$$E_{DissFloc,Max}=\alpha_{\epsilon,Floc}\,E_{DissFloc,Avg}$$


```python
ENERGY_DIS_FLOC_AVERAGE = (exp.K_MINOR_FLOC_BAFFLE / (2 * HEIGHT_FLOC_OBSTACLES)) * (FLOW_PLANT/(WIDTH_FLOC_CHANNEL * 
    SPACING_FLOC_BAFFLE))**3
ENERGY_DIS_FLOC_MAX =2 * ENERGY_DIS_FLOC_AVERAGE
```

### Average Velocity Gradient

$$G_{Floc,Avg}=\sqrt{\frac{E_{DissFloc,Avg}}{\nu}}$$


```python
G_FLOC_AVERAGE = np.sqrt(ENERGY_DIS_FLOC_AVERAGE / exp.NU_WATER)
```

### Residence Time

$$t_{FlocActive}=\frac{\left(N_{FlocChan}\,L_{Floc}-L_{EntTank}-T_{FlocDivWall}-S_{FlocBaffle}\,\left(N_{FlocChanSpaces}-N_{Floc,LastChanSpaces}\right)\right)\,W_{FlocChan}\,H_{WaterEnd}}{Q_{Plant}}$$


```python
VOLUME_FLOC= (NUMBER_FLOC_CHANNELS * LENGTH_FLOC - LENGTH_ENTRANCE_TANK - THICKNESS_FLOC_DIVIDING_WALL) * WIDTH_FLOC_CHANNEL * \
    (HEIGHT_WATER_END + HEADLOSS_FLOC / 2)
TIME_FLOC = VOLUME_FLOC / FLOW_PLANT
TIME_FLOC_ACTIVE = (NUMBER_FLOC_CHANNELS * LENGTH_FLOC - LENGTH_ENTRANCE_TANK - THICKNESS_FLOC_DIVIDING_WALL - \
    (SPACING_FLOC_BAFFLE * (NUMBER_FLOC_CHANNEL_SPACES - NUMBER_FLOC_LAST_CHANNEL_SPACES)))* WIDTH_FLOC_CHANNEL * \
    HEIGHT_WATER_END / FLOW_PLANT 
```

### Alternative method for Collision Potential

$$G\,\theta=G_{FlocAvg}\,t_{FlocAct}$$


```python
G_THETA = G_FLOC_AVERAGE * TIME_FLOC_ACTIVE
```

### Baffle Heights

The baffle height must follow the constraints of no-overflow and accounting for the water level at the end of the flocculator.

$$H_{Floc,TopLowBaffle}=H_{WaterEnd}-S_{FlocBaffle}\,\Pi_{FlocBaffle}$$

$$H_{Floc,BottomTopBaffle}=H_{WaterEnd}+Headloss_{Floc}+H_{PlantFreeBoard}-S_{FlocBaffle}\,\Pi_{FlocBaffle}$$


```python
HEIGHT_FLOC_TOP_OF_LOW_BAFFLE = HEIGHT_WATER_END - SPACING_FLOC_BAFFLE * exp.RATIO_FLOC_BAFFLE
HEIGHT_FLOC_BOTTOM_OF_TOP_BAFFLE = HEIGHT_WATER_END + HEADLOSS_FLOC + exp.HEIGHT_PLANT_FREE_BOARD - \
    SPACING_FLOC_BAFFLE * exp.RATIO_FLOC_BAFFLE
```

### Obstacle Design

$$W_{FlocObst}=S_{FlocBaffle}\,\left(1-\Pi_{VCBaffle}\right)$$


```python
WIDTH_FLOC_OBST = SPACING_FLOC_BAFFLE*(1-RATIO_VC_BAFFLE)
```

## Final Output


```python
print('The user inputs were used to design the final flocculator. The collision potential for this flocculator \
is the dimensionless value, '+ut.sig(CP_FLOC.to(u.dimensionless),5)+'. The velocity is '+ut.sig(VELOCITY_FLOC.to(u.mm/u.s),3)+' \
and the headloss is '+ut.sig(HEADLOSS_FLOC.to(u.mm),4)+'. The geometry of the flocculator is confined to H/S ratio limits \
of '+ut.sig(RATIO_FLOC_HS_MIN.to(u.dimensionless),4)+' and '+ut.sig(RATIO_FLOC_HS_MAX.to(u.dimensionless),4)+'. The \
average velocity gradient is '+ut.sig(G_FLOC_AVERAGE.to(u.Hz),4)+', and the flocculator residence \
time is '+ut.sig(TIME_FLOC_ACTIVE.to(u.s),4)+'. The maximum energy dissipation rate for the flocculator \
is '+ut.sig(ENERGY_DIS_FLOC_MAX.to(u.mW/u.kg),4)+'. The height of the top of the lowest baffle \
is '+ut.sig(HEIGHT_FLOC_TOP_OF_LOW_BAFFLE.to(u.m),4)+' whereas the height of the bottom of the highest baffle \
is '+ut.sig(HEIGHT_FLOC_BOTTOM_OF_TOP_BAFFLE.to(u.m),4)+'. The width of the obstacles for this flocculator \
is '+ut.sig(WIDTH_FLOC_OBST.to(u.mm),4)+'. These parameters are necessary to design the flocculator geometry and flow \
requirements. Some parameters can be exported to AutoCAD Fusion to create a 3D drawing of the flocculator.')
```

    The user inputs were used to design the final flocculator. The collision potential for this flocculator is the dimensionless value, 38531. The velocity is 217 mm/s and the headloss is 443.7 mm. The geometry of the flocculator is confined to H/S ratio limits of 3.693 and 5.331. The average velocity gradient is 112.9 Hz, and the flocculator residence time is 351.0 s. The maximum energy dissipation rate for the flocculator is 25.51 mW/kg. The height of the top of the lowest baffle is 1.729 m whereas the height of the bottom of the highest baffle is 2.273 m. The width of the obstacles for this flocculator is 165.9 mm. These parameters are necessary to design the flocculator geometry and flow requirements. Some parameters can be exported to AutoCAD Fusion to create a 3D drawing of the flocculator.
    

## Conclusions

The code above can be used to design a flocculator based on efficiency and energy dissipation rate. This is congruous with the method taught by Professor Monroe Weber-Shirk in CEE 4540. While translating the MathCAD code, we removed non-essential functions to produce the most user-friendly and streamlined design code. Below, we provide suggestions for improving and expanding this design code.

## Suggestions for Future Work

We suggest expanding the flocculator code to include the entrance tank and horizontal flocculator design code. These designs can be integrated into AutoCAD to develop a drawing of the system. We also recommending developing Python code to predict the cost of the system.
