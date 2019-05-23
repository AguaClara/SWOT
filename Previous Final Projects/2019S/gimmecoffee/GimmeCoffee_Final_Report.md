# Construction and Operational Estimation Cost Model of Water Treatment Plants
### Team GimmeCoffee
### Lynn Li (ll643), Allison Tran (ant42), and Yeonjin Yun (yy374)
### Due 05/18/2019

# Introduction
For our final project we are going to create a quantitative cost estimation model and provide qualitative economic information about available floc/clarification/porous media filtration systems. We will create both an overall construction cost model as well as a operation and maintenance cost model. Through research from online resources as well as from real-time water treatment plant performance data we will identify the advantages and disadvantages of the AguaClara treatment scheme relative to the other available technologies from an economic standpoint. After being taught to "question everything", we developed a curiosity about the effectiveness of current water treatment plants and whether or not AguaClara is currently implementing the best methods available given cost factors. We have also noticed a lack of documented information in regard to current treatment methods and their prices. Therefore we hypothesize that many plants across the globe are using methods that are standard but not necessarily the most cost effective method. By creating a simplified method of estimating construction/operating cost through python models with design constraints we hope to provide an accessible method of comparison that can make the treatment process more effective. Once this is achieved, it will be cheaper to implement filtration processes, and more people will be able to have access to clean drinking water.

# Project Proposal
For our project, we will first proceed by gathering qualitative information about the alternatives we have chosen from online resources and from the AguaClara Textbook. In order to do this efficiently, each of us has randomly selected one step of the process to research. From this we will get an overall understanding of pros and cons of each system which will allow us to figure out what variables we can manipulate and how this will affect the overall cost of the system. Afterwards, we will be contacting various treatment plants that are using different treatment systems for their performance data. Example of plants that we have plan to contact are the Ithaca Water Treatment Plant (mechanical flocculator, plate settlers, and membrane filtration as well as the Cornell Treatment Plant (mechanical flocculator, horizontal flow sedimentation, and sand filtration). From there we will create a python model from the equations provided from [Preliminary Cost Estimation Models for Construction, Operation, and Maintenance of Water Treatment Plants, 2013](https://ascelibrary.org/doi/10.1061/(ASCE)IS.1943-555X.0000155). We will test the accuracy of this model by using the plant data given we have obtained as well as using data from AguaClara plants.

# Design Parameters

**Key Parameters**
- Construction Costs  
- Operational Costs
- Capital Cost
  - Net Velocities are a rough alternative to capital costs
- Effectiveness (correlates with cost efficiency)
  - EPA standards require that drinking water turbidity not go over 0.3 NTU

For this project we will be using American EPA drinking water standards even though we recognize the fact that drinking water standards vary from location to location around the globe.

# Economic Trade Offs

### Flocculation
|                              | Option 1: Mechanical Flocculator   | Option 2: Hydraulic Flocculator (Conventional) | Option 3: Hydraulic Flocculator (AguaClara) |
| ----------------------------:| ---------------------------------- | ---------------------------------------------- | ------------------------------------------- |
|               Capital Cost |    Cost of Motors   |          Cost of building flocculator           |          Cost of building flocculator       |
|               Operating Cost | Electricity Cost to run the motors | No major operating costs                       | No major operating costs                    |
|  Maintenance Cost (one time) | Property/Equipment Maintenance     | Slight Labor Cost                              | Slight Labor Cost                           |
|                Economic Pros |                                    |              No use of electricity, Low maintenance cost               |        No use of electricity, Low maintenance cost     |
|                Economic Cons | Waste of electricity, Maintenance cost for the motors               |                                                |                                             |

### Clarification
|                                       | Clarification Option 1: Conventional                                                          | Clarification Option 2: [AguaClara Floc Banket/Plate Settler/Floc Hopper System](https://aguaclara.github.io/Textbook/Sedimentation/Sed_Design.html)                                | Clarification Option 3: Superpulsator®          |
| -------------------------------------:| --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| Equipment Cost Relative to Each Other | Minimal                                                                                       | Medium                                                                                                                                                                              | Low                                             |
| Operation Cost Relative to Each Other | Low                                                                                           | Low                                                                                                                                                                                 | ?                                               |
|                 Detention Time* (min) | 240                                                                                           | 60                                                                                                                                                                                  | 60                                              |
|                         Economic Pros |                                                                                               | Doesn't require an energy input (uses gravity), has a higher removal per unit plan area compared to Conventional, and the floc blanket improves performance of a sedimentation tank |                                                 |
|                         Economic Cons | Requires an energy input and a mechanical cleaning system that fails is difficult to maintain |                                                                                                                                                                                     | Requires manual cleaning of sedimentation tank. |

(* ) Detention time has a direct impact on construction costs

### Porous Media Filtration
|                                                       | Activated Carbon Filtration                                                                                                                     | Rapid Gravity Filtration                                                                          |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Equipment cost relative to classic sand filtration    | High                                                                                                                                            | High                                                                                              |
| Operation cost relative to classic sand filtration    | High                                                                                                                                            | High                                                                                              |
| Construction cost relative to classic sand filtration | High                                                                                                                                            | High                                                                                              |
| Economic pros                                         | Activated carbon itself is relatively cheap                                                                                                     | High filter rate and short backwashing time                                                       |
| Economic cons                                         | Cost of operating carbon-handling equipment is high, adsorption capacity of carbon is low so frequent regeneration means higher operating costs | Requires frequent cleaning, construction of technical facilities, and high energy and labor costs |

# Calculations
```Python
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
import math
import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile
```

## Simple Preliminary Construction Cost Estimation Model for Water Treatment Plants
```Python
# c = chlorine feed capacity (lb/day)
c_sample = 5000*(u.lb/u.day)
# f = feed capacity (lb/h)
f_sample = 2700*(u.lb/u.hr)
# v = total basin volume (ft^3)
v_sample = 10000*(u.ft**3)
# s = net effective settling area (ft^2)
s_sample = 7000*(u.ft**2)
# fa = total filter area (ft^2)
fa_sample = 14000*(u.ft**2)
# x = plant flow rate, plant capacity (mgd)
x_sample = 100*(u.Mgal/u.day)
# p = pumping capacity (gpm)
p_sample = 16*(u.gal/u.min)
# b = basin capacity (gal)
b_sample = 250000*(u.gal)
# sv = storage volume (gal)
sv_sample = 450*(u.gal)
# cw = clearwell capacity (gal)
cw_sample = 3000*(u.gal)

@u.wraps(u.USD, [u.lb/u.day, u.lb/u.hr, u.ft**3, u.ft**2, u.ft**2, u.Mgal/u.day, u.gal/u.min, u.gal, u.gal, u.gal], False)
def simple_CC(c, f, v, s, fa, x, p, b, sv, cw):
  # cylinder chlorine storage
  pretreatment_cc =  ((((3)*(10**-6))*(u.USD/(u.lb**3/u.day**3))*(c**3)) - 0.0158*(u.USD/((u.lb/u.day)**2))*c**2 + 98.896*(u.USD/((u.lb/u.day)))*c + 10708*u.USD)
  # liquid alum feed system
  coagulation_cc = (-0.0262*(u.USD*u.hr**2/u.lb**2)*(f**2)) + (292.72*(u.USD*u.hr/u.lb)*f) + 56640*u.USD
  # rapid mix (G = 300/s)
  rapid_mix_cc = (0.0002*(u.USD/u.ft**6)*(v**2)) + 24.2*(u.USD/u.ft**3)*v + 29690*u.USD
  # vertical turbine flocculation (G = 50/s)
  flocculator_cc = -0.0006*(u.USD/((u.ft)**6))*(v**2) + 29.796*(u.USD/((u.ft)**3))*v + 34290*u.USD
  # upflow solid contact clarifiers
  clarifier_cc = (-0.0031*(u.USD/u.ft**4)*(s**2)) + (140.98*(u.USD/u.ft**2)*s) + 221973*u.USD
  # gravity filtration structures
  gravity_cc = (0.000001*(u.USD/u.ft**6)*(fa**3)) - (0.0439*(u.USD/u.ft**4)*(fa**2)) + (1039*(u.USD/u.ft**2)*fa) + 477982*u.USD
  # rapid sand filtration media
  rapid_sand_cc = (7827.9*(u.USD/(u.Mgal/u.day))*x) + 13969*u.USD
  # backwash pumping facilities
  backwash_cc = (12.427*(u.USD/((u.gal/u.min)**3))*(p**3)) - (650.05*(u.USD/((u.gal/u.min)**2))*(p**2)) + (23879*(u.USD/(u.gal/u.min))*p) + 69478*u.USD
  # hydraulic surface wash systems
  hydraulic_sa_cc = (0.0006*(u.USD/((u.ft)**4))*(fa**2)) + (50.64*(u.USD/((u.ft)**2))*fa) + 80743*u.USD
  # wash water surge basins
  wash_water_surge_cc = 869.07*(u.USD/(u.gal)**0.5845)*(b**0.5845)
  # wash water storage tanks
  wash_water_storage_cc = (886.95*(u.USD/u.gal)*sv) + 27291*u.USD
  # Management: Administrative, laboratory and maintenance building
  management_cc = 73024*(u.USD/(u.Mgal/u.day)**0.5523)*(x**0.5523)
  # below-ground clearwell storage
  storage_cc = (-0.0782*(u.USD/u.gal**2))*(cw**2) + (1271.1*(u.USD/u.gal))*(cw) + 118926*u.USD

  total_cc = pretreatment_cc + coagulation_cc + rapid_mix_cc + flocculator_cc + clarifier_cc +  gravity_cc + rapid_sand_cc + backwash_cc + hydraulic_sa_cc + wash_water_surge_cc + wash_water_storage_cc + management_cc + storage_cc
  return total_cc

Total_cc_sample = simple_CC(c_sample, f_sample, v_sample, s_sample, fa_sample, x_sample, p_sample, b_sample, sv_sample, cw_sample)
print ('The total plant construction cost estimation is', ut.round_sf(Total_cc_sample,4),'.')
# The Total Plant Construction Cost Estimation is 1.979e+07 dollars
```

## Complex Preliminary Construction Cost Estimation Model for Water Treatment Plants
```Python
class Construction_Cost:
  def __init__(self, c, f, v, s, fa, x, p, b, sv, cw):
      """Instantiate Cost object, representing an example plant.

      :param c: chlorine feed capacity
      :type c: float * u.lb/u.day
      :param f: feed capacity
      :type f: float * u.lb/u.hr
      :param v: total basin volume
      :type v: float * (u.ft)**3
      :param s: net effective settling area
      :type s: float * (u.ft)**2
      :param fa: total filter area
      :type fa: float * (u.ft)**2
      :param x: plant flow rate, plant capacity
      :type x: float * u.Mgal/u.day
      :param p: pumping capacity
      :type p: float * u.gal/u.min
      :param b: basin capacity
      :type b: float * u.gal
      :param sv: storage volume
      :type sv: float * u.gal
      :param cw: clear well capacity
      :type cw: float * u.gal
      """
      self.c = c
      self.f = f
      self.v = v
      self.s = s
      self.fa = fa
      self.x = x
      self.p = p
      self.b = b
      self.sv = sv
      self.cw = cw

  #@property
    # cylinder chlorine storage
  def pretreatment_cc2(self):
    if self.c >= 10*(u.lb/u.day) and self.c <= 10000*(u.lb/u.day):
      return ((((3)*(10**-6))*(u.USD/((u.lb/u.day)**3))*(self.c**3))) - 0.0158*(u.USD/((u.lb/u.day)**2))*self.c**2 + 98.896*(u.USD/((u.lb/u.day)))*self.c + 10708*u.USD
    elif self.c == 0:
      return(0)
    else:
      print('Chlorine Feed Capacity input is outside of range.')
      return(-1)

  #@property
  # liquid alum feed system
  def coagulation_cc(self):
    if self.f >= 5.4*(u.lb/u.hr) and self.f <= 5400*(u.lb/u.hr):
      return (-0.0262*(u.USD*u.hr**2/u.lb**2)*(self.f**2)) + (292.72*(u.USD*u.hr/u.lb)*self.f) + 56640*u.USD
    elif self.f == 0:
      return(0)
    else:
      print('Feed Capacity input is outside of range.')
      return(-1)

  #@property
  # rapid mix (G = 300/s)
  def rapid_mix_cc(self):
    if self.v >= 100*(u.ft**3) and self.v <= 20000*(u.ft**3):
      return (0.0002*(u.USD/u.ft**6)*(self.v**2)) + 24.2*(u.USD/u.ft**3)*self.v + 29690*u.USD
    elif self.v == 0:
      return(0)
    else:
      print('Total Basin Volume input is outside of range.')
      return(-1)

  #@property
  # vertical turbine flocculation (G = 50/s)
  def flocculator_cc(self):
    if self.v >= 1800*(u.ft**3) and self.v <= 25000*(u.ft**3):
      return -0.0006*(u.USD/((u.ft)**6))*(self.v**2) + 29.796*(u.USD/((u.ft)**3))*self.v + 34290*u.USD
    elif self.v == 0:
      return(0)
    else:
      print('Total Basin Volume input is outside of range.')
      return(-1)

  #@property
  # upflow solid contact clarifiers
  def clarifier_cc(self):
    if self.s >= 255*(u.ft**2) and self.s <= 14533*(u.ft**2):
      return (-0.0031*(u.USD/u.ft**4)*(self.s**2)) + (140.98*(u.USD/u.ft**2)*self.s) + 221973*u.USD
    elif self.s== 0:
      return(0)
    else:
      print('Net Effective Settling Area input is outside of range.')
      return(-1)

  #@property
  # gravity filtration structures
  def gravity_cc(self):
    if self.fa >= 140*(u.ft**2) and self.fa <= 28000*(u.ft**2):
      return (0.000001*(u.USD/u.ft**6)*(self.fa**3)) - (0.0439*(u.USD/u.ft**4)*(self.fa**2)) + (1039*(u.USD/u.ft**2)*self.fa) + 477982*u.USD
    elif self.fa == 0:
      return(0)
    else:
      print('Total Filter Area input is outside of range.')
      return(-1)

  #@property
  # rapid sand filtration media
  def rapid_sand_cc(self):
    if self.x >= 1*(u.Mgal/u.day) and self.x <= 200*(u.Mgal/u.day):
      return (7827.9*(u.USD/(u.Mgal/u.day))*self.x) + 13969*u.USD
    elif self.x == 0:
      return(0)
    else:
      print('Plant Flow Rate input is outside of range.')
      return(-1)

  #@property
  # backwash pumping facilities
  def backwash_cc(self):
    if self.p >=1.8*(u.gal/u.min) and self.p <= 33*(u.gal/u.min):
      return (12.427*(u.USD/((u.gal/u.min)**3))*(self.p**3)) - (650.05*(u.USD/((u.gal/u.min)**2))*(self.p**2)) + (23879*(u.USD/(u.gal/u.min))*self.p) + 69478*u.USD
    elif self.p == 0:
      return(0)
    else:
      print('Pumping Capacity input is outside of range.')
      return(-1)

  #@property
  # hydraulic surface wash systems
  def hydraulic_sa_cc(self):
    if self.fa >= 140*(u.ft)**2 and self.fa <= 28000*(u.ft)**2:
      return (0.0006*(u.USD/((u.ft)**4))*(self.fa**2)) + (50.64*(u.USD/((u.ft)**2))*self.fa) + 80743*u.USD
    elif self.fa == 0:
      return(0)
    else:
      print('Total Filter Area input is outside of range.')
      return(-1)

  #@property
  # wash water surge basins
  def wash_water_surge_cc(self):
    if self.b >= 10000*u.gal and self.b <= 500000*u.gal:
      return 869.07*(u.USD/(u.gal)**0.5845)*(self.b**0.5845)
    elif self.b == 0:
      return(0)
    else:
      print('Basin Capacity input is outside range.')
      return(-1)

  #@property  
  # wash water storage tanks
  def wash_water_storage_cc(self):
    if self.sv >= 21*u.gal and self.sv <= 900*u.gal:
      return (886.95*(u.USD/u.gal)*self.sv) + 27291*u.USD
    elif self.sv == 0:
      return(0)
    else:
      print('Storage Volume input is outside range.')
      return(-1)

  #@property  
  # Management: Administrative, laboratory and maintenance building
  def management_cc(self):
    if self.x >= 1*(u.Mgal/u.day) and self.x <= 200*(u.Mgal/u.day):
      return 73024*(u.USD/(u.Mgal/u.day)**0.5523)*(self.x**0.5523)
    elif self.x == 0:
      return(0)
    else:
      print('Plant Capacity input is outside range.')
      return(-1)

  #@property
  # below-ground clearwell storage
  def storage_cc(self):
    if self.cw >= 10*u.gal and self.cw <= 7500*u.gal:
      return (-0.0782*(u.USD/u.gal**2))*(self.cw**2) + (1271.1*(u.USD/u.gal))*(self.cw) + 118926*u.USD
    elif self.cw == 0:
      return(0)
    else:
      print('Clearwell Capacity input is outside range.')
      return(-1)

  #@property
  # total cost
  def total_cc(self):
    pretreatment_cc2 = self.pretreatment_cc2()
    coagulation_cc = self.coagulation_cc()
    rapid_mix_cc = self.rapid_mix_cc()
    flocculator_cc = self.flocculator_cc()
    clarifier_cc = self.clarifier_cc()
    gravity_cc = self.gravity_cc()
    rapid_sand_cc = self.rapid_sand_cc()
    backwash_cc = self.backwash_cc()
    hydraulic_sa_cc = self.hydraulic_sa_cc()
    wash_water_surge_cc = self.wash_water_surge_cc()
    wash_water_storage_cc = self.wash_water_storage_cc()
    management_cc = self.management_cc()
    storage_cc = self.storage_cc()

    if pretreatment_cc2 == -1 or coagulation_cc == -1 or rapid_mix_cc == -1 or flocculator_cc == -1 or clarifier_cc == -1 or gravity_cc == -1 or rapid_sand_cc == -1 or backwash_cc == -1 or hydraulic_sa_cc == -1 or wash_water_surge_cc == -1 or wash_water_storage_cc == -1 or management_cc == -1 or storage_cc == -1:
      print('The total cost could not be computed because a parameter is outside the range.')
    else:
      return pretreatment_cc2 + coagulation_cc + rapid_mix_cc + flocculator_cc + clarifier_cc +  gravity_cc + rapid_sand_cc + backwash_cc + hydraulic_sa_cc + wash_water_surge_cc + wash_water_storage_cc + management_cc + storage_cc

Cost_c_sample = Construction_Cost(c_sample, f_sample, v_sample, s_sample, fa_sample, x_sample, p_sample, b_sample, sv_sample, cw_sample)
Cost_c_sample_total = Cost_c_sample.total_cc()
print('The total plant construction cost estimation is', ut.round_sf(Cost_c_sample.total_cc(),6),'.')
#The total construction costs of the plant are 1.979e+07 dollars

Q=1000*u.L/u.s

cost_cex = Construction_Cost(c_sample, f_sample, v_sample, s_sample, Q/(11*u.mm/u.s), Q, p_sample, b_sample, sv_sample, cw_sample)
filt_cost=cost_cex.rapid_sand_cc()+cost_cex.gravity_cc()
filt_cost.to_base_units()/Q
```

## Simple Preliminary Operation and Maintenance Cost Estimation Model for Water Treatment Plants
```Python
@u.wraps(u.USD, [u.lb/u.day, u.lb/u.hr, u.ft**3, u.ft**2, u.ft**2, u.Mgal/u.day, u.gal/u.min], False)
def simple_OC(c, f, v, fa, x, s, p):
  # cylinder chlorine storage
  pretreatment_oc =  ((((6)*(10**-7))*(u.USD/(u.lb**3/u.day**3))*(c**3)) - 0.009*(u.USD/((u.lb/u.day)**2))*c**2 + 68.23*(u.USD/((u.lb/u.day)))*c + 21371*u.USD)
  # liquid alum feed system
  coagulation_oc = 2212.7*(u.USD/(u.lb/u.hr)**0.2919)*(f**0.2919)
  # rapid mix (G = 300/s)
  rapid_mix_oc = ((-3)*(10**(-8))*(u.USD/(u.ft**9)))*(v**3) + (0.0008*(u.USD/(u.ft**6)))*(v**2) + 2.8628*(u.USD/(u.ft)**3)*v + 23676*u.USD
  # upflow solid contact clarifiers
  clarifier_oc = (-0.00007*(u.USD/u.ft**4))*(s**2) + 3.8893*(u.USD/u.ft**2)*s + 25236*u.USD
  # gravity filtration structures
  gravity_oc = (((7)*(10**-8))*(u.USD/(u.Mgal/u.day)**3)*(x**3)) - (0.0026*(u.USD/(u.Mgal/u.day)**2)*(x**2)) + (61.589*(u.USD/(u.Mgal/u.day))*x) + 49584*u.USD
  # backwash pumping facilities
  backwash_oc = ((4*10**-9)*((u.USD/((u.gal/u.min)**3)))*(p**3)) - ((0.0002)*((u.USD)/((u.gal/u.min)**2))*(p**2)) + ((5.1398)*(u.USD/((u.gal/u.min)))*(p)) + (11540*(u.USD))
  # hydraulic surface wash systems
  hydraulic_sa_oc = ((4*10**-9)*(u.USD/(u.ft**6))*(fa**3))-((0.0002)*(u.USD/(u.ft**4))*(fa**2)) + ((3.9838*(u.USD/(u.ft**2)))*fa) + 4682*(u.USD)
  # Management: Administrative, laboratory and maintenance building
  management_oc = 92981*(u.USD/(u.Mgal/u.day)**0.4526)*(x**0.4526)

  total_oc = pretreatment_oc + coagulation_oc + rapid_mix_oc + clarifier_oc +  gravity_oc + backwash_oc + hydraulic_sa_oc + management_oc
  return total_oc

Total_oc_sample = simple_OC(c_sample, f_sample, v_sample, fa_sample, x_sample, s_sample, p_sample)
print ('The total plant operation and maintenance cost estimation is', ut.round_sf(Total_oc_sample,4), '.')
#The total plant operation and management cost estimation is 1.233e+06 dollars.
```

## Complex Preliminary Operational Cost Estimation Model for Water Treatment Plants
```Python
class Operation_Cost:
  def __init__(self, c, f, v, fa, x, s, p):
      """Instantiate Cost object, representing an example plant.

      :param c: chlorine feed capacity
      :type c: float * u.lb/u.day
      :param f: feed capacity
      :type f: float * u.lb/u.hr
      :param v: total basin volume
      :type v: float * (u.ft)**3
      :param s: net effective settling area
      :type s: float * (u.ft)**2
      :param fa: total filter area
      :type fa: float * (u.ft)**2
      :param x: plant flow rate, plant capacity
      :type x: float * u.Mgal/u.day
      :param p: pumping capacity
      :type p: float * u.gal/u.min
      """
      self.c = c
      self.f = f
      self.v = v
      self.s = s
      self.fa = fa
      self.x = x
      self.p = p

  #@property
    # cylinder chlorine storage
  def pretreatment_oc2(self):
    if self.c >= 10*(u.lb/u.day) and self.c <= 10000*(u.lb/u.day):
      return ((((6)*(10**-7))*(u.USD/(u.lb**3/u.day**3))*(self.c**3)) - 0.009*(u.USD/((u.lb/u.day)**2))*self.c**2 + 68.23*(u.USD/((u.lb/u.day)))*self.c + 21371*u.USD)
    elif self.c == 0:
      return(0)
    else:
      print('Chlorine Feed Capacity input is outside of range.')
      return(-1)

  #@property
  # liquid alum feed system
  def coagulation_oc(self):
    if self.f >= 5.4*(u.lb/u.hr) and self.f <= 5400*(u.lb/u.hr):
      return 2212.7*(u.USD/(u.lb/u.hr)**0.2919)*(self.f**0.2919)
    elif self.f == 0:
      return(0)
    else:
      print('Feed Capacity input is outside of range.')
      return(-1)

  #@property
  # rapid mix (G = 300/s)
  def rapid_mix_oc(self):
    if self.v >= 1800*(u.ft**3) and self.v <= 25000*(u.ft**3):
      return ((-3)*(10**(-8))*(u.USD/(u.ft**9)))*(self.v**3) + (0.0008*(u.USD/(u.ft**6)))*(self.v**2) + 2.8628*(u.USD/(u.ft)**3)*self.v + 23676*u.USD
    elif self.v == 0:
      return(0)
    else:
      print('Total Basin Volume input is outside of range.')
      return(-1)

  #@property
  # upflow solid contact clarifiers
  def clarifier_oc(self):
    if self.s >= 255*(u.ft**2) and self.s <= 14533*(u.ft**2):
      return (-0.00007*(u.USD/u.ft**4))*(self.s**2) + 3.8893*(u.USD/u.ft**2)*self.s + 25236*u.USD
    elif self.s== 0:
      return(0)
    else:
      print('Net Effective Settling Area input is outside of range.')
      return(-1)

  #@property
  # gravity filtration structures
  def gravity_oc(self):
    if self.x >= 1*(u.Mgal/u.day) and self.x <= 200*(u.Mgal/u.day):
      return (((7)*(10**-8))*(u.USD/(u.Mgal/u.day)**3)*(self.x**3)) - (0.0026*(u.USD/(u.Mgal/u.day)**2)*(self.x**2)) + (61.589*(u.USD/(u.Mgal/u.day))*(self.x)) + 49584*u.USD
    elif self.fa == 0:
      return(0)
    else:
      print('Total Filter Area input is outside of range.')
      return(-1)

  #@property
  # backwash pumping facilities
  def backwash_oc(self):
    if self.p >=1.8*(u.gal/u.min) and self.p <= 33*(u.gal/u.min):
      return ((4*10**-9)*((u.USD/((u.gal/u.min)**3)))*(self.p**3)) - ((0.0002)*((u.USD)/((u.gal/u.min)**2))*(self.p**2)) + ((5.1398)*(u.USD/((u.gal/u.min)))*(self.p)) + (11540*(u.USD))
    elif self.p == 0:
      return(0)
    else:
      print('Pumping Capacity input is outside of range.')
      return(-1)

  #@property
  # hydraulic surface wash systems
  def hydraulic_sa_oc(self):
    if self.fa >= 140*(u.ft)**2 and self.fa <= 28000*(u.ft)**2:
      return ((4*10**-9)*(u.USD/(u.ft**6))*(self.fa**3))-((0.0002)*(u.USD/(u.ft**4))*(self.fa**2)) + ((3.9838*(u.USD/(u.ft**2)))*self.fa) + 4682*(u.USD)
    elif self.fa == 0:
      return(0)
    else:
      print('Total Filter Area input is outside of range.')
      return(-1)

  #@property  
  # Management: Administrative, laboratory and maintenance building
  def management_oc(self):
    if self.x >= 1*(u.Mgal/u.day) and self.x <= 200*(u.Mgal/u.day):
      return 92981*(u.USD/(u.Mgal/u.day)**0.4526)*(self.x**0.4526)
    elif self.x == 0:
      return(0)
    else:
      print('Plant Capacity input is outside range.')
      return(-1)

  #@property
  # total cost
  def total_oc(self):
    pretreatment_oc2 = self.pretreatment_oc2()
    coagulation_oc = self.coagulation_oc()
    rapid_mix_oc = self.rapid_mix_oc()
    clarifier_oc = self.clarifier_oc()
    gravity_oc = self.gravity_oc()
    backwash_oc = self.backwash_oc()
    hydraulic_sa_oc = self.hydraulic_sa_oc()
    management_oc = self.management_oc()

    if pretreatment_oc2 == -1 or coagulation_oc == -1 or rapid_mix_oc == -1 or clarifier_oc == -1 or gravity_oc == -1 or backwash_oc == -1 or hydraulic_sa_oc == -1 or management_oc == -1:
      print('The total cost could not be computed because a parameter is outside the range.')
    else:
      return pretreatment_oc2 + coagulation_oc + rapid_mix_oc + clarifier_oc +  gravity_oc + backwash_oc + hydraulic_sa_oc + management_oc

Cost_o_sample = Operation_Cost(c_sample, f_sample, v_sample, fa_sample, x_sample, s_sample, p_sample)
total_cost_o_sample =  Cost_o_sample.total_oc()
print('The total plant operation and maintenance cost estimation is', ut.round_sf(total_cost_o_sample,3),'.')
#The total operational and maintenance costs of the plant are 1.23e+06 dollar
```

## Test with Ithaca Treatment Plant Parameters
```Python
df = pd.read_excel('Projects/2019/final/gimmecoffee/mop2018.xls', sheetname='mopfrm')

RW_Flow = df['Raw Water Flow Rate']
avg_2018_RW_FR=(RW_Flow[37])*u.Mgal/u.day
avg_2018_RW_FR.to(u.L/u.s)

Chlorine_Fed = df['Chlorine Fed']
Chlorine_Tank_Conc = df['Chlorine Tank Concentration']
avg_2018_Chlorine_Feed_Capacity=((Chlorine_Fed[37]*u.gal/u.day)*(Chlorine_Tank_Conc[37]*u.milligram/u.liter)).to(u.lb/u.day)
avg_2018_Chlorine_Feed_Capacity

# x = plant flow rate, plant capacity (mgd)
x_ith = avg_2018_RW_FR
# range for x was between 1 to 200
percentage = avg_2018_RW_FR/(200*u.Mgal/u.day) #percentage of where Ithaca ranks on the min to max range
# c = chlorine feed capacity (lb/day)
c_ith = avg_2018_Chlorine_Feed_Capacity
# f = feed capacity (lb/h)
f_ith = (percentage*(5400-5.4)+5.4)*(u.lb/u.hr)
# v = total basin volume (ft^3)
v_ith = (percentage*(25000-1800)+1800)*(u.ft**3)
# s = net effective settling area (ft^2)
s_ith = (percentage*(14533-255)+255)*(u.ft**2)
# fa = total filter area (ft^2)
fa_ith = (percentage*(2800-140)+140)*(u.ft**2)
# p = pumping capacity (gpm)
p_ith = (percentage*(33-1.8)+1.8)*(u.gal/u.min)
# b = basin capacity (gal)
b_ith = (percentage*(500000-10000)+10000)*(u.gal)
# sv = storage volume (gal)
sv_ith = (percentage*(900-21)+21)*(u.gal)
# cw = clearwell capacity (gal)
cw_ith = (percentage*(7500-10)+10)*(u.gal)

# simple construction
Total_Ithaca_cc = simple_CC(c_ith, f_ith, v_ith, s_ith, fa_ith, x_ith, p_ith, b_ith, sv_ith, cw_ith)
print ('The total Ithaca plant construction cost estimation is', ut.round_sf(Total_Ithaca_cc,4), '.')
# complex construction
Cost_Ithaca_C = Construction_Cost(c_ith, f_ith, v_ith, s_ith, fa_ith, x_ith, p_ith, b_ith, sv_ith, cw_ith)
total_ith_cost_c = Cost_Ithaca_C.total_cc()
print('The total Ithaca plant construction cost estimation is', ut.round_sf(total_ith_cost_c,6))
# simple operation
Total_Ithaca_oc = simple_OC(c_ith, f_ith, v_ith, fa_ith, x_ith, s_ith, p_ith)
print ('The total Ithaca plant operation and maintenance cost estimation is', ut.round_sf(Total_Ithaca_oc,4), '.')
# complex operation
Cost_Ithaca_o = Operation_Cost(c_ith, f_ith, v_ith, fa_ith, x_ith, s_ith, p_ith)
total_ith_cost_o =  Cost_Ithaca_o.total_oc()
print('The total Ithaca plant operation and maintenance cost estimation is', ut.round_sf(total_ith_cost_o,3))
```

## Calculating the Minimum Cost of Construction and Operation/Maintenance for a Water Treatment Plant
```Python
# x = plant flow rate, plant capacity (mgd)
x_min = 1*(u.Mgal/u.day)
# c = chlorine feed capacity (lb/day)
c_min = (10)*(u.lb/u.day)
# f = feed capacity (lb/h)
f_min = (5.4)*(u.lb/u.hr)
# v = total basin volume (ft^3)
v_min = (1800)*(u.ft**3)
# s = net effective settling area (ft^2)
s_min = (255)*(u.ft**2)
# fa = total filter area (ft^2)
fa_min = (140)*(u.ft**2)
# p = pumping capacity (gpm)
p_min = (1.8)*(u.gal/u.min)
# b = basin capacity (gal)
b_min = (10000)*(u.gal)
# sv = storage volume (gal)
sv_min = (21)*(u.gal)
# cw = clearwell capacity (gal)
cw_min = (10)*(u.gal)

# simple construction
Minimum_cc = simple_CC(c_min, f_min, v_min, s_min, fa_min, x_min, p_min, b_min, sv_min, cw_min)
print ('The minimum total plant construction cost estimation is', ut.round_sf(Minimum_cc,4), '.')
# complex construction
Mininum_cc_complex = Construction_Cost(c_min, f_min, v_min, s_min, fa_min, x_min, p_min, b_min, sv_min, cw_min)
Min_cost_complex = Mininum_cc_complex.total_cc()
print('The minimum total plant construction cost estimation', ut.round_sf(Min_cost_complex,6),'.')
# simple operation
Total_oc_min = simple_OC(c_min, f_min, v_min, fa_min, x_min, s_min, p_min)
print ('The total minimum plant operation and maintenance cost estimation is', ut.round_sf(Total_oc_min,4), '.')
# complex operation
Cost_o_min = Operation_Cost(c_min, f_min, v_min, fa_min, x_min, s_min, p_min)
total_cost_o_min =  Cost_o_min.total_oc()
print('The total minimum operational and maintenance cost estimation of the plant is', ut.round_sf(total_cost_o_min,3),'.')
```

## Calculating the Maximum Cost of Construction and Operation/Maintenance for a Water Treatment Plant
```Python
# x = plant flow rate, plant capacity (mgd)
x_max = 200*(u.Mgal/u.day)
# c = chlorine feed capacity (lb/day)
c_max = (10000)*(u.lb/u.day)
# f = feed capacity (lb/h)
f_max = (5400)*(u.lb/u.hr)
# v = total basin volume (ft^3)
v_max = (20000)*(u.ft**3)
# s = net effective settling area (ft^2)
s_max = (14533)*(u.ft**2)
# fa = total filter area (ft^2)
fa_max = (28000)*(u.ft**2)
# p = pumping capacity (gpm)
p_max = (33)*(u.gal/u.min)
# b = basin capacity (gal)
b_max = (500000)*(u.gal)
# sv = storage volume (gal)
sv_max = (900)*(u.gal)
# cw = clearwell capacity (gal)
cw_max = (7500)*(u.gal)

# simple construction
Maximum_cc = simple_CC(c_max, f_max, v_min, s_max, fa_max, x_max, p_max, b_max, sv_max, cw_max)
print ('The maximum total plant construction cost estimation is', ut.round_sf(Maximum_cc,4), '.')
# complex construction
Maximum_cc_complex = Construction_Cost(c_max, f_max, v_max, s_max, fa_max, x_max, p_max, b_max, sv_max, cw_max)
Max_cost_complex = Maximum_cc_complex.total_cc()
print('The maximum total plant construction cost estimation is', ut.round_sf(Max_cost_complex,6))
# simple operation
Total_oc_max = simple_OC(c_max, f_max, v_max, fa_max, x_max, s_max, p_max)
print ('The total maximum plant operation and maintenance cost estimation is', ut.round_sf(Total_oc_max,4), '.')
# complex operation
Cost_o_max = Operation_Cost(c_max, f_max, v_max, fa_max, x_max, s_max, p_max)
total_cost_o_max =  Cost_o_max.total_oc()
print('The total maximum plant operation and maintenance cost estimation is', ut.round_sf(total_cost_o_max,3))
```

|  | Model Ithaca Estimation Cost | Actual Ithaca Cost | Model Minimum Cost | Model Maximum Cost |
|---:|---|---|---|---|
| Construction Cost | $2.1 million | $37-39 million | $1.77 million| $36.45 million |
| Operating and Maintenance Cost | $293,000 | $713,209 | $243,000 | $1.8 million |

# Equations
[General Plant Costs](https://ascelibrary.org/doi/10.1061/%28ASCE%29IS.1943-555X.0000155)

### Construction Cost
![Equation 1](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_cost1.PNG)

![Equation 2](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_cost2.PNG)

![Equation 3](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_cost3.PNG)

![Equation 4](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_cost4.PNG)

### Annual Operation and Maintenance Cost
![Equation 5](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_oc1.PNG)

![Equation 6](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_oc2.PNG)

![Equation 7](https://github.com/ll643/GimmeCoffee/raw/master/GimmeCoffee_oc3.PNG)

# Real Data
## Known Plant Cost Chart
|                          Plant | Plant Flow Rate (L/s) | Construction Cost (USD) | Operating Costs (USD)                                                                  | Capital Costs (USD) |
| ------------------------------:| --------------------- | ----------------------- | -------------------------------------------------------------------------------------- | ------------------- |
|   Ithaca Water Treatment Plant | 103                   | $37-39 million          | [$713,209](https://github.com/ll643/GimmeCoffee/blob/master/IWTP_Budget_2018-2019.pdf) |                     |
|        Gracias AguaClara Plant | 120                   | $974,591.59             |                                                                                        |                     |
|      Las Vegas AguaClara Plant | 70                    | $408,989.48             |                                                                                        |                     |
|      Zamorano AguaClara Plants | 30                    | $391,222.92             |                                                                                        |                     |
|    San Nicolás AguaClara Plant | 32                    | $246,577.79             |                                                                                        |                     |
| Jesús de Otoro AguaClara Plant | 20                    | $233,452.47             |                                                                                        |                     |
|       Morocelí AguaClara Plant | 16                    | $200,883.39             |                                                                                        |                     |
|     San Matías AguaClara Plant | 14                    | $191,248.60             |                                                                                        |                     |

## Ithaca Water Treatment Plant Operating Data
| Ithaca Water Treatment Plant (Avg) |    2018    |
| ----------------------------------:| ---------- |
|   Chlorine Feed Capacity (lb/day)  |  11.935    |   
|                      RW Flow (MGD) |  2.349     |
|                          Raw (NTU) |  46.5      |
|                      Settled (NTU) | 0.6192     |
|                     Finished (NTU) | 0.0157     |
|               Total Efficiency (%) | 99.9       |
|                                 pH | 8.0        |
| Free Chlorine Residuals Eff (mg/L) | 1.826      |
|           Skid Waste Total* (kgal) | 115.178    |
(*) Skid waste can be used to measure operational costs

# Conclusion
Using the equations generated from the [Preliminary Cost Estimation Models for Construction, Operation, and Maintenance of Water Treatment Plants Report](https://ascelibrary.org/doi/10.1061/%28ASCE%29IS.1943-555X.0000155), we were able to create four cost models in Python to estimate the construction and operation/maintenance costs of a water treatment plant: two of these models are "simple" and the other two are "complex" so that there is a simple and a complex model for both construction cost estimation and operation/maintenance cost estimation. The simple models require manual inputs of the variables which must have units and there is no way to negate a variable or to check if the input is within the bounds of the equation. The equations in the cost itself has units so if the input variable does not have the correct units the code will crash which is not the most elegant way to prevent input errors but it acts as safety blanket. In comparison, the complex models allow the user to negate terms which are not relevant to their plant and it checks to make sure that the inputs are within the ranges set by the report. If the input is not in this range the code will print a statement telling the user that their input is out of range. Again, like the simple model, the user must input constants with the correct units. In order to test the accuracy of our models, we ran them with constants given to us by the Ithaca Water Treatment Plant. Unfortunately, we could not find all of the plant design parameters that we needed for the model from the operating data which was sent to us so we had to estimate for the missing variables. We knew for certain that the flow rate of the Ithaca Treatment Plant is 2.4 MGD on a range from 1 to 200 MGD for our model so we calculated the percentage of the Ithaca Flow Rate on the range and used that percentage to calculate for the remaining missing variables. The construction and operating costs which were generated by the models were smaller than the actual costs. This can be attributed to the fact that we had to estimate more than half of the plant design parameters and in addition we did not include all of the equations which are included in the original report. Our low costs mean that we negated certain attributes of a water treatment plant used in the Ithaca Treatment Plant. There are more than 50 equations provided in the original report which this model was based off of, and due to time constraints it was not feasible for us to include all of these equations. However, the framework of each model is set so that it would very simple to add more variables and equations which would be a future avenue for this project.

# Comments and Suggestions
As mentioned in the Conclusion, there is a lot of work which can be done if this project is to be furthered. Most of this work would be coding work to make the Class function we created more elegant and user friendly. Other than adding more equations, one can also work on code which would assign units to the inputs and/or autocorrect the units of the inputs. In addition, there is a possibility of creating an Excel extension for this project. Users could input their plant design parameters onto an Excel sheet if they do not have any Python background and the code could pull the numbers from the Excel sheet and input them into the models. However, regardless, we are proud of the model which we have managed to create and through the process of creating this model we all definitely strengthened our Python coding abilities. We hope to see this project grow into something more sophisticated that AguaClara can implement in the near future!

# Bibliography
Conceptual Design Report Haverstraw Water Supply Project (Rep.). (2008). New York, NY: Black & Veatch New York LLP. Retrieved from http://documents.dps.ny.gov/public/Common/ViewDoc.aspx?DocRefId={12F1C6AB-4F9E-4881-BF39-AC854D37DE11}

Flocculation design.pptx. 2019. Retrieved from: https://github.com/AguaClara/CEE4540_Master/raw/master/Lectures/In%20Class/Flocculator%20Design.pptx

Flocculation model.pptx. 2019. Retrieved from:
https://github.com/AguaClara/CEE4540_Master/raw/master/Lectures/In%20Class/Flocculation%20Model.pptx

Handbook of Industrial Water Treatment. (n.d.). Retrieved from https://www.suezwatertechnologies.com/handbook/handbook-industrial-water-treatment

National Primary Drinking Water Regulations. Retrieved from: https://www.epa.gov/sites/production/files/2016-06/documents/npwdr_complete_table.pdf

Sharma, J. R., Najafi, M., & Qasim, S. R. (2013, March 6). Preliminary Cost Estimation Models for Construction, Operation, and Maintenance of Water Treatment Plants. Retrieved from https://ascelibrary.org/doi/10.1061/(ASCE)IS.1943-555X.0000155

Rapid Sand Filtration. 2018. Retrieved from: https://sswm.info/sswm-university-course/module-6-disaster-situations-planning-and-preparedness/further-resources-0/rapid-sand-filtration

Water Treatment Manuals: Filtration. Environmental Protection Agency (1995). Retrieved from: https://www.epa.ie/pubs/advice/drinkingwater/EPA_water_treatment_manual_%20filtration1.pdf
