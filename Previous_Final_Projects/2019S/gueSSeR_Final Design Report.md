# Project title: Who treated it better? Membrane vs. StaRS edition
Team: gueSSeR
Team members: Rafael Heryapriadi, Sidney Lok, Steven Neumaier

## Introduction
Membrane filtration is an up-and-coming type of filtration option [Perhaps give a little history here including how many decades membranes have been used] [Addressed by Steve] for water treatment plants. The first water treatment plant to use membrane filtration was a plant in Colorado that opened in 1987 (Technology trends in membrane filtration use). Beginning around 2001, there has been significant investment in research and development of membrane filters. Membrane filtration is attractive because the pores are small enough to capture particles like Cryptosporidium oocysts. Membrane filtration requires a large membrane surface area to treat water at the rate it is needed in many communities. Therefore, to minimize space used by a membrane filter, it is arranged into a tight configuration in columns called modules, which are then arranged into arrays called skids. Water passes through the membranes pores which physically remove particles and pathogens.

Membrane filtration typically requires a pump to create a pressure differential across the membrane. This means membrane filtration will require electricity to run.

The goal of our design project is to compare the efficiency, cost, and feasibility of membrane filtration to AguaClara's Stacked Rapid Sand (StaRS) filters. AguaClara plants are designed with a purpose: to make safe drinking water more accessible to those who cannot afford a traditional drinking water treatment plant. Cost and efficiency of design are important to AguaClara plant design, so our work would reveal whether membrane filtration would be a better alternative to the existing StaRS filter.

## Methods
Our plan is to study one of the AguaClara plants in Honduras as a comparison to a low pressure membrane system from Pall. The plant we chose to compare was the Moroceli Plant, which was constructed in 2014 and has a design flow rate of 16 L/s. From the data we receive about the Moroceli plant, we are able to make estimates about the cost and size of plants of varying flow rates. The Pall membrane system we chose to compare was the Aria AP-6 Water Treatment System.

We want to allow others to use our estimates as a tool for comparing price and size of membrane and StaRS filters. Therefore, all of our calculations have been created with the intention of using a *Design Plant Flow Rate* that is inputted by the user. Additionally, we allow the user to change the electricity price as the location or price changes.

### Important constraints
Some constraints we initially identified were:
1. Plant Flow
2. Effluent Water Quality
3. Access to Electricity
4. Feed Water Quality
5. Chemical Cleaning Regime
6. Preventative Maintenance Program
7. Pretreatment Process/Chemistry, Cost/Benefit Evaluation at End of Membrane Life

As we worked on this project and tried to find information about these constraints for each treatment option, we found it difficult to get answers from Pall about membrane filters.

We ended up narrowing down our comparison to four points of interest:

1. Cost
2. Temperature
3. Particle Removal
4. Plan-view Area

We decided to look at cost to test for economic feasibility and also for basic business sense. Temperature came up as an interesting constraint to look at for us because (and this will be discussed further in the report) membranes tend to fail more quickly at colder temperatures. However, membranes perform well for removal of particles like Cryptosporidium, Giardia, and bacteria so that was something we wanted to look into and compare with StaRS filters. Plan-view area is closely related to cost because the larger a plant is, the more it will cost to buy the land and to construct. Additionally, there will be a higher materials and building cost associated with larger plants.

Flow rate of Moroceli plant: 16 L/s
Average turbidity before floc/sed: 14.23 NTU
Turbidity after floc/sed: 0.56 NTU
Average turbidity after filtration: 0.20 NTU
**Note: Data was taken from files that Monroe sent us from 2016**


### Trade-offs
Stack sand filter vs. Membrane filtration

Advantages of Membrane filtration
1. Less influenced by influent water conditions - flow and water quality
2. Effluent quality is mostly constant
3. Provide a physical barrier against suspended solids and smaller, nasty particles like Cryptosporidium, Giardia, Bacteria, Colloids
4. No need to buy coagulant

Disadvantages of Membrane filtration
1. Requires a pump and therefore requires electricity.
2. Flux depends on temperature and is greatly reduced in low temperatures
3. May require pumping air in for physical backwash and integrity testing
4. Requires chemical backwash - sodium hydroxide/hypochlorite or citric, sulfuric, phosphoric, or hydrochloric acids
5. Unable to remove dissolved organics as AguaClara floc/sed processes can with coagulant
6. Electricity and chemical costs


## Design alternatives
Membrane filtration is seen by many as an alternative for using flocculation, sedimentation (or floc/sed), and filtration. It is believed that using a membrane filter of a certain pore size will treat water as well as following the processes typically associated with flocculation, sedimentation, and filtration.

We will investigate the following three design alternatives:
1. Full AguaClara plant
2. AguaClara floc/sed + membrane filtration
3. Only membrane filtration

## Comparison of Design Alternatives
As mentioned before, the baseline for our comparisons was the Moroceli AguaClara plant, which handles 16 L/s flow.

We looked at several different membrane filtration systems that are commercially available. The Pall Corporation quoted us a system called the Pall Aria AP-6 Water Treatment System (Fig. 1). This was the system we used in our comparison.

<p align="center">
  <img src="https://shop.pall.com/INTERSHOP/static/WFS/PALL-PALLUS-Site/-/PALL/en_US/images/Power-Generation/wat_ds_pho_ariasys.gif" height=200>
</p>
<p align="center">

**Figure 1:** Depicted is a "skid" or singular module of the Pall Aria AP-6 Water Treatment System.

### Cost

The code to calculate the cost of an AguaClara StaRS filter and of a membrane module for a variable input flow rate is shown at the end of the report in the Calculations section. The code can be modified to calculate costs for different plant flows, if desirable.

Minty, an AguaClara engineer based in Honduras, provided us with the cost of a AguaClara stacked sand filter for 20 L/s flow at Gracias. The cost of the filter including the control box is 18500 USD, including materials and labor only.
[What is this cost estimate of 16,000 USD? ]
[Steve: The cost estimate of 16,000 USD was incorrect and will not be used in our final report]

 According to Pall's website, the model number AP-6 may have up to 60 modules and treats between 45 and 150 m^3/hr of water. We were quoted the price for a system that could treat 200 gallons per minute of water (~12.6 L/s) would be between 360,000 and 500,000 USD. Their website lists utility requirements for the Aria AP-6 System are 460v and 70 A. We use the utility requirements to get an estimate for the electricity costs as no data was provided/available. The utility requirement is likely an over estimate for the total electricity cost. Chemical costs are not published and not provided. Pall has specific, but unpublished and not provided, recommendations for a chemical backwash procedure and  specifications for chemicals. The website lists 10+ years as the lifetime for the Aria Membrane filters.


### Temperature
The Pall Aria module data sheet mentions that the maximum temperature that the module could operate in is 40 degrees Celsius. However, according to Farahbakhsh and Smith (2006), interactions between the temperature and the polymeric membrane may result in lower porosity and increased tortuosity at lower water temperatures. As AguaClara plants are able to operate without much dependence on water temperature, this should not be a problem.

Therefore, in comparing AguaClara plants with membrane filters for decision-making on which technology to use, AguaClara plants may be the better bet in regions that experience colder temperatures while both AguaClara plants and membrane filters are feasible in hotter regions.

### Particle Removal
[Where did you find this information about treated water turbidity for AguaClara? It is wrong!] [Addressed -SL]
AguaClara plants typically have an output turbidity of less than 0.3 NTU, meeting Honduran standards but not US EPA standards. According to Brooks et. al., AguaClara plants are able to robustly remove E. coli from water being treated.

The Pall Aria module data sheet notes that the output turbidity of their filters should be less than 0.1 NTU, which is under US EPA standards. The Pall Aria module is also capable of removing Cryptosporidium, Giardia, and MS2 coliphage or bacteriophage. [Do StaRS filters remove pathogens? See http://www.ajtmh.org/content/journals/10.4269/ajtmh.17-0577] [Addressed -SL]

[what is the flow rate of the module? Go metric! The data you present is useless without providing flow rates.] [Sidney: Unable to retrieve information.]
### Plan-view Area
The specifications of the Pall Aria Module say that the required space for the AP-6 system is 27 feet by 17 feet. An AguaClara StaRS filter is approximately $4m^{2}$ (Monroe's estimate).

The AguaClara StaRS filter is much smaller than the necessary membrane filter equivalent. However, the data we have for the AguaClara StaRS filter does not include the footprint for the control system. Neither include the space for operators to access the filter controls.

[I thought I gave you the information on footprint of the filters. See http://designserver.cee.cornell.edu/Designs/EtFlocSedFi/]

The footprint of an AguaClara StaRS filter is $4 m^{2}$ and the footprint of the Aria system is $42.64 m^{2}$.
[Interesting. But is this for the same flow rate? Can you do a comparison that includes the equipment needed by both filtration systems so you have a total space required comparison?] [Addressed in Future Work -SL]

# Conclusions
With the information we gathered from comparison of AguaClara technology versus Membrane technology, we created a decision tree (Fig. 2) to help users decide on the correct technology to use.

<p align="center">
  <img src="https://github.com/sidneylok/Personal/blob/master/Membrane%20v%20AguaClara%20Decision%20Tree%20(1).jpg?raw=true" height=500>
</p>
<p align="center">

**Figure 2:** A decision tree we made from our research that should help a user decide which technology to use.

An issue that we consistently ran into was being unable to retrieve information about the membranes from suppliers. We called Pall Corporation and Suez Corporation (another membrane filtration company) to find out more information about their filters, but were either redirected to an empty line or were simply refused the information we needed. This is an important consideration when comparing AguaClara systems and membrane filtration options. If a plant operator needed help troubleshooting or if a potential client wanted to assess the fit of an option to their specific need or situation, they would probably have more luck getting help from AguaClara than from Pall or Suez. Resilient systems need to have good feedback loops and troubleshooting support to make sure the technology does not become obsolete or leave the client unable to operate the product.

There are definitely some advantages to using membrane filters that cannot be found in AguaClara technology; for instance, if you are working with Cryptosporidium or Giardia. However, it only makes sense to use membrane filtration then if there is consistent, reliable access to electricity. Otherwise, AguaClara technology is more elegant, simple, and affordable option.

# Future Work
We recognize that this may not be the most realistic or wholistic look at the comparison between AguaClara plants and membrane filtration. Future work needs to be done in acquiring information of interest like flow rate of the membrane filter in order to paint a more complete picture. If additional information is acquired, the researcher should also look into updating the decision tree to reflect the new information.

# Bibliography
(n.d.). Retrieved from https://energypedia.info/wiki/Honduras_Energy_Situation

Brooks, Y. M., Tenorio-Moncada, E. A., Gohil, N., Yu, Y., Estrada-Mendez, M. R., Bardales, G., & Richardson, R. E. (2018). Performance Evaluation of Gravity-Fed Water Treatment Systems in Rural Honduras: Verifying Robust Reduction of Turbidity and Escherichia coli during Wet and Dry Weather. The American Journal of Tropical Medicine and Hygiene, 99(4), 881-888. doi:10.4269/ajtmh.17-0577

Farahbakhsh, K., & Smith, D. W. (2006). Membrane filtration for cold regions – impact of cold water on membrane integrity monitoring tests. Journal of Environmental Engineering and Science, 5(Supplement 1). doi:10.1139/s06-037

Pall Aria™ AP-Series Water Treatment Systems. (n.d.). Retrieved from https://shop.pall.com/us/en/power-utilities/steam-plants/water-supply/pall-aria-ap-series-water-treatment-systems-zidgri78l70?tracking=searchterm:aria

Technology trends in membrane filtration use. (2018). Filtration Separation, 55(1), 30-33. doi:10.1016/s0015-1882(18)30174-5

# Calculations
We are planning to make our calculations for designing the membrane filter to be adaptable to any flow rate needed to be designed for. However, for the purposes of comparing design alternatives, we will be using the Moroceli plant StaRS filter as a baseline for efficiency, cost, and feasibility perspectives.


```python
import aguaclara
from aguaclara.core.units import unit_registry as u
import numpy as np
from aguaclara.core import utility as ut
import math as m

```
Here are the dependent variables or inputs for the calculations of costs and plant areas. They are the Design plant flow rate and the cost of electricity per kilowatt-hour

```python
#Enter the desired flow rate here
Design_Plant_Flow_Rate = 16 * u.L/u.s
#Average electricity cost in Honduras from https://energypedia.info/wiki/Honduras_Energy_Situation
elec_cost = 0.1034 * u.USD / u.kWh
```
**Cost estimation**
Our estimated cost for an AguaClara plant stack sand filter with control is:

```python
#Using the Gracias plant to estimate prices of the StaRS filter
Gracias_StaRS_cost = 18500 * u.USD
Gracias_flowrate = 20 * u.L / u.s
AverageStaRS_cost = Gracias_StaRS_cost / (Gracias_flowrate/(u.L/u.s))

StaRS_Cost = Design_Plant_Flow_Rate * AverageStaRS_cost / (u.L/u.s)
StaRS_lifetime = (30 * u.year).to(u.s)

#Finding the cost in terms of USD / million liters treated
StaRS_per_mill_liters = (StaRS_Cost / (Design_Plant_Flow_Rate * StaRS_lifetime) * 1000000)/(u.USD/u.L)
StaRS_per_mill_liters = ((StaRS_Cost / (Design_Plant_Flow_Rate * StaRS_lifetime))).to(u.USD/u.ML)

print('An AguaClara stacked sand filter that treats', Design_Plant_Flow_Rate, 'will cost', StaRS_per_mill_liters, 'USD per million liters of water treated.')
```

Our estimated cost of the Pall Aria AP-6 system is:
```python
#Given values for Aria AP-6 system
Aria_flowrate = 200 * u.gal / u.min
Aria_buildingcost_low = 360000 * u.USD
Aria_buildingcost_high = 500000 * u.USD
Aria_lifetime = (10 * u.year).to(u.min)

#Estimating the cost for the design flow rate
Aria_cost_per_liter_per_sec_low = Aria_buildingcost_low / Aria_flowrate
Aria_cost_per_liter_per_sec_high = Aria_buildingcost_high / Aria_flowrate

Aria_cost_design_low = Aria_cost_per_liter_per_sec_low * Design_Plant_Flow_Rate
Aria_cost_design_high = Aria_cost_per_liter_per_sec_high * Design_Plant_Flow_Rate

#Electricity requirements for Aria AP-6 system
Voltage = 460 * u.V
Current = 70 * u.A
Wattage = Voltage * Current
Energy_Cost = (Wattage * 24 * u.hr * elec_cost / u.day).to(u.USD/u.min)


#Finding the cost in terms of USD / million liters treated
Total_Aria_cost_low = Aria_cost_design_low + Energy_Cost * Aria_lifetime
Total_Aria_cost_high = Aria_cost_design_high + Energy_Cost * Aria_lifetime

Aria_per_mill_liters_low = ((Total_Aria_cost_low / (Design_Plant_Flow_Rate * Aria_lifetime) * 1000000).to(u.USD/u.L))/(u.USD/u.L)
Aria_per_mill_liters_high = ((Total_Aria_cost_high / (Design_Plant_Flow_Rate * Aria_lifetime) * 1000000).to(u.USD/u.L))/(u.USD/u.L)

print('The Aria Membrane system for a', Design_Plant_Flow_Rate,'plant excluding labor, an unknown chemical cost, and maintenance is between', Aria_per_mill_liters_low, 'USD/million liters and', Aria_per_mill_liters_high, 'USD/million liters.')
```

Our estimates for the cost for a full AguaClara plant are:
```python
# The code in this section determines the plant cost for a full plant according to the Design_Plant_Flow_Rate, which can be changed above to adjust for a different desire flow rate. To calculate our estimates for a design plant price, we use data from the Moroceli plant.
Moroceli_plant_cost = 200883 * u.USD
Moroceli_flowrate = 16 * u.L / u.s
AguaClara_building_cost = Moroceli_plant_cost / Moroceli_flowrate * Design_Plant_Flow_Rate
AguaClara_lifetime = 30 * u.year
Moroceli_chem_cost = 6814 * u.USD / u.year

AguaClara_chemical_cost = Moroceli_chem_cost / Moroceli_flowrate * Design_Plant_Flow_Rate

AguaClara_total_cost = AguaClara_building_cost + AguaClara_chemical_cost * AguaClara_lifetime


AguaClara_cost_per_mill_liters = (AguaClara_total_cost / (Design_Plant_Flow_Rate * AguaClara_lifetime.to(u.s)) * 1000000)/(u.USD/u.L)

print('An AguaClara plant that treats', Design_Plant_Flow_Rate, 'will cost', AguaClara_cost_per_mill_liters, 'USD per million liters of water treated.')
```

**Size Comparison**

```python
StaRS_Footprint = 4 * u.m ** 2
Aria_Footprint = 27 * u.ft * 17 * u.ft

# The footprint of the AguaClara plant was calculated by looking at the OnShape drawing and scaling it by the known length of the jet reverser manifold, which is 6 m long.

Manifold_Length = 6 * u.m
OnShape_Manifold_Length = 145 * u.mm
Scale = Manifold_Length / OnShape_Manifold_Length
OnShape_Length = 322.284 * u.mm
OnShape_Width = 185.15 * u.mm
Plant_Length = OnShape_Length * Scale
Plant_Width = OnShape_Width * Scale
Plant_Footprint = Plant_Length * Plant_Width

print('The footprint of an AguaClara StaRS filter is ', StaRS_Footprint, 'and the footprint of the full AguaClara plant is', Plant_Footprint)
print('The footprint of the Aria system is',Aria_Footprint.to(u.m**2))
```
