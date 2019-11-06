

```python
from aide_design.play import*


```

# Breaking Borders to Change Water Availability in Bolivia

## Team Sssssnakes

## Aobei Cheng  |  Jacob Dahneke  |  Bo Yang

**Background**

Located in the Bolivian side of Lake Titicaca, Suriqui Island is well-known for its inhabitants being the last remaining community to extend the art of color boat construction. The inhabitants are in the immediate need of the water supply and treatment plant that could help them build the fresh-water drinking system in the Suriqui Island. There are four separate communities need water supplies. AguaClara is trying to apply its current water treatment technology to the local community, to offer the residents safe water at a sustainable and low cost. 

The water source being used by the water treatment plant is from Lake Titicaca, the largest freshwater lake in South America, straddles the border between Bolivia and Peru. Pollution from urban and agricultural development is a persistent problem in the lake. The proposed water treatment plant at Suriqui Island is a consequence of the emerging water contamination.

**Partner Organization:** AguaClara Reach

**Location:** Suriqui, Bolivia 

**Proposed Solution**

The proposed solution for constructing the water treatment plant is a single plant that provides water to the entire community. The plant is designed to be located at the highest elevation to have sufficient potential energy to deliver water to each community. The sample sketches could be found below.

The elevation of the plant above the highest residence in the island is 10 meters. This elevation ensures enough head to deliver water from the water treatment plant to all the households on the island.

The highest elevation of residence is 3867m (12688 feet) above sea level. The water treatment plant is therefore at an elevation of 3877m (12721 ft) above sea level.   The determination of the location of the treatment plant has three criterias: 1) the plant needs to be away from sewage outflow to ensure the water is not directly exposed to contamination. 2) Buiding the plant on a slope could reduce the amount of excavation required by the plant, because the bottom of the OStaRS filters is several meters lower in elevation than the bottom of the flocculation/ sedimentation tanks. 3) The plant should not be far away from the shorline, which can minimize the length of the water intake pipes. Based on the three criterias, the plant is designed to be built on the northeast side of the island indicated on the graph map. Since the area is away from the most populated (southwest side) of the island, the quality of the water intake is higher.

Due to the small residence population on the island, the cost of installing water usage meters is relatively expensive (the average price is approximately equivalent to the plant construction cost, according to Professor Monroe Weber-shirk). The average water usage per capita in Bolivia is estimated to be 25-50 L/p/day. In this study, the water usage per person is 100 L/p/day due to the absence of metering.

![alt_text](http://i65.tinypic.com/28k0zkn.png "3D view design")
The Plan-view of Suriqui Isaland. The proposed location of the water treatment plant and the distribution pipelines are described on the graph
![alt_text](http://i66.tinypic.com/e8n3tc.png "side view design")
The side-view elevation of Suriqui Island. The height difference between the lake water level and the water treatment plant is approx. 56 m.



These flow rates represent the expected average flow rate needed for the anticipated population 20 years out based on 2.5% geometric growth with 100 l/p/d and 10% for leakage.The calculation is shown below the table.

| Parameter| Units|Suriqui|Supicachi|Paco Chachacoma|Cuyampaya|Combined|
|:------------------:|:-------------:|:-----------------:|:----------------:|:----------------:|:----------------:|:----------------:|
| Current Population| Persons |1810|300|580|200|2890|  
|    Flow Rate   |  gpm|58|10|19|6.6|96|  
|    Flow Rate    |  lps    | 3.7|0.63|1.2|0.42|6.0| 

The designed Plant needs to meet the supply requirement of 6L/s. 

The water distribution system follows the existing road way around the island, as shown on the graph. 


```python
Population_Suriqui = 1810
Population_Supicachi = 300
Population_PacoChachacoma = 580
Population_Cuyampaya = 200

Water_use_per_person = (100*(u.l/u.day)).to(u.l/u.s)
Leakage_rate = 0.1
Population_growth_rate = 0.025

Flow_rate_Suriqui = (Population_Suriqui *(Water_use_per_person*(1+Leakage_rate)))*(1+Population_growth_rate)**20
Flow_rate_Supicachi = (Population_Supicachi *(Water_use_per_person*(1+Leakage_rate)))*(1+Population_growth_rate)**20
Flow_rate_PacoChachacoma = (Population_PacoChachacoma *(Water_use_per_person*(1+Leakage_rate)))*(1+Population_growth_rate)**20
Flow_rate_Cuyampaya = (Population_Cuyampaya *(Water_use_per_person*(1+Leakage_rate)))*(1+Population_growth_rate)**20
Flow_rate_total = Flow_rate_Suriqui+Flow_rate_Supicachi+Flow_rate_PacoChachacoma+Flow_rate_Cuyampaya
print('The flow rate required by residence in Suriqui is',Flow_rate_Suriqui)
print('The flow rate required by residence in Supicachi is', Flow_rate_Supicachi)
print('The flow rate required by residence in PacoChachacoma is',Flow_rate_PacoChachacoma)
print('The flow rate required by residence in Cuyampaya is', Flow_rate_Cuyampaya)
print('Therefore, the total flow rate required is '+ ut.sig(Flow_rate_total ,1)+'.')
```

    The flow rate required by residence in Suriqui is 3.776 liter / second
    The flow rate required by residence in Supicachi is 0.6259 liter / second
    The flow rate required by residence in PacoChachacoma is 1.21 liter / second
    The flow rate required by residence in Cuyampaya is 0.4172 liter / second
    Therefore, the total flow rate required is 6 l/s.
    

**Comparison of Alternatives**

| Plants at each community | Single Plant |Cost Analysis|
|:------------------:|:----------------------------:|:----------------------------:|
| Require at least 3 full-time operators (one operator at each plant)  | Requires only 1 full-time operator |save 20295USD* per year| 
|      Central to each community     |    Distance varies (possible for long distance transportation|Cost addition pipelines|
|       Smaller pumping required     |    Pumping to high elevation           |Cost pumping power|  
|       Cost easily attributed   |   Hard to distribute cost          |    - |

*Based on Bolivian average income 2017
The average income is assumed to be $6765. To operate a plant, one full-time employee and a part-time employee (1/2 amount of full-time) are needed to ensure the function of the water treatment plant everyday in a year. An 8-hour working period is assumed. 



```python
Ave_income = 6765*u.USD
Three_plants_salary = Ave_income*3*1.5
#1.5 = one full-time and one part-time operator
One_plant_salary = Ave_income*1.5
Money_saved = Three_plants_salary-One_plant_salary
print('The money saved per year will be '+ut.sig(Money_saved,5)+'.')
```

    The money saved per year will be 20295 USD.
    

**Transmission Line HeadLoss**

We also need to consider the major headloss of the transmission pipes. We assume the average velocity is around 0.4 ft/s. 


```python
#Headloss Calculation
Q = 6*u.l/u.s
v = 0.4*u.ft/u.s
diam = (4*Q/(np.pi*v))**(1/2)
Length = 9*u.km
Temperature = u.Quantity(8,u.degC)
Viscosity = pc.viscosity_kinematic(Temperature)
Piperough = 0.1
headloss = pc.headloss_fric(Q, diam, Length, Viscosity, Piperough)

print ('The headloss of the distribution system is '+ut.sig(headloss,3)+'')
```

    The headloss of the distribution system is 7.33 m
    

**Constraints**

The constraints include financial limitations, reliable energy sources, locally available construction materials, quality of water intake (Untreated sewage from more than 20 nearby cities; 15 tons Mercury/yr), and minimal funds for maintenance.



**Major Design Alternatives**

The previous design is based on the allocation of four separated systems to supply the community, while this new project will examine the viability of creating a single water treatment plant. The new design will then be compared with the previous design.

The new project will explore the cost and design to install a solar-powered pump or to use diesel powered electricity to create energy source for inlet pumping. This project will analyze the possibility of incorporating such a design.


**Steps to Solve the Problem**

1. Completely understand the constraints of working in this part of Bolivia
2. Preliminary analysis in Python
3. Consult with more experienced designers 
4. Finish Python calculations 
5. Conduct write up



## Energy Source


```python
# The average temperature in La Paz is 46F, which is roughly 8C throughout the year. 
temp = u.Quantity(8, u.degC)
density_water = pc.density_water(temp)
g = pc.gravity
# The highest elevation in the residential areas is 46 meters, and we add another 10 meters to it to make sure we
# have enough head for the entire island. We also add another 8 meters to take the headloss of the transmission pipe
# headloss. 
Height_req = 46*u.m + 10*u.m + 8*u.m
req_water = 6*(u.L/u.s)

Power_needed = (density_water*g*Height_req*req_water).to(u.kW)
print('To satisfy the required water flow as 6 L/s, the required power for the pump is',Power_needed)
```

    To satisfy the required water flow as 6 L/s, the required power for the pump is 3.765 kilowatt
    

After calculating the required pumping power, we need to select appropriate energy sources. In this study, we pick Diesel and Solar Energy as the two potential ones. 

We think that the comparison between solar and diesel powered pumping from the lake to the drinking water treatment plant need to both be considered. While initially it would seem like a diesel generator would make the most sense, we found this to not be the case. 

First off, for solar there are over 12 hours of sunlight per day on average this is advantageous because there is a lot of sun to be captured. In addition, the average temperature is relatively low which is factored into our spread sheet. The low temperature is advantageous because solar panels become less efficient with high temperatures. Moreover, the installed cost of solar has gone down significantly over the last thirty years. To put into perspective how much the price of solar has decreased in the last 35 years, in 1975 the average installed cost of solar per watt was 30 USD and in 2010 it was 1.50 USD (Vanek, 2017). This is a significant decrease, and it is helping create a strong argument for solar. This is interesting because the cost is significantly even considering the cost of the storage tank, which allows a constant inflow of 6L/s. 

Based our calculations for the solar energy, we introduce one alternative - the application for solar battery system. We subsitute the cost of constructing a storage tank with the cost of a battery system which stores energy and eliminates the need for storage. This would address unpredictable variability such as the cloudy or rainy weather. From our calculations below, we think this alternative is even better than the current solar plan. 

In our analysis, we also considered the option of a diesel-powered pump. While initially it would seem as if this would be more cost effective, there are a lot of constraints and costs involved. The main one being the cost of the diesel even though the Bolivian government has already subsidized part of the diesel price. In addition, the extent of diesel usage is also relevantly limited. Though the operation of diesel-based pumps is not related to the sunlight time nor the weather, which in fact is nice for the solar panels, we need to take the maintennance of the pump into consideration. 

In conclusion, the cost of solar is much more attractive, and considering the increased environmental benefits we think it is the best option.

Let's start with Diesel! 

## Diesel

**Introduction**

Diesel was relevantly limited compared to other fuels such as gasoline in Bolivia in early 2000s since the diesel is mainly imported from Chile and under strict control on the quota. Nowadays, the Bolivian government has a less strict policy in the domestic diesel use in Bolivia for its citizens, though such policy towards foreigners is still strict in terms of the daily usage and objectives. Another benefit for diesel is that there are lots of diesel-based water pumps in the market and we could get a lower total price potentially. Moreover, we don't need to store the water here and therefore there is no storage cost compared to solar energy since we can just directly pumping the water from the lake.

**Diesel Price** 

The diesel price in November 2017 is 3.75 Boliviano Dollars, which is 0.53 USD. That's the price after the deduction made by Bolivian government, compared to the normal price (to foreigners) as 8.8 BOB. 

**Self-Priming Pump**

Since the required power is 5.049 horsepower, we find a water pump with a 6-horsepower self-pumping engine system.

The diesel powered water pump we apply here is Multiquip Water Pump - QP2TK, 172 GPM, 2", Diesel Trash Pump. The picture of the water pump is shown below. 

![alt_text](https://www.absolutewaterpumps.com/media/catalog/product/cache/1/image/9df78eab33525d08d6e5fb8d27136e95/m/u/multiquip_qp2tk.jpg)

To be noted, this pump will be located next to the water as indicated in the map above and it's designed to be able to pump the water up to 63.33 meters.


```python
# First, we need to calculate the annual cost for diesel fuel. 

# Relationship: Diesel needed = fuel capacity of the pump*amounts of refill needed per day* 365 days
# From the information page of the pump, as indicated in the Citation, we get: 
# The fuel capacity for the pump is 0.95 gallon and the average run time for the engine is 2.7 hours.
# That tells us for every 2.7 hours, the engine needs a refill of 0.95 gallon. 

fuel_cap = (0.95*u.gallon).to(u.L) 
engine_run_time = 2.7*u.hour 
amount_fuel_filling = np.ceil(24*u.hour/engine_run_time)  
amount_fuel_needed = fuel_cap*amount_fuel_filling # per day

# Quoted on November 30th, the price for diesel is 0.53 USD/L. 
# Assume the price of diesel won't change for 30 years, 
fuel_price = 0.53*u.USD/u.L

annual_cost_diesel = fuel_price*fuel_cap*amount_fuel_filling*365
print('The daily usage of diesel of the pump is',amount_fuel_needed)
print('The annual cost for just the diesel filling is',annual_cost_diesel)
```

    The daily usage of diesel of the pump is 32.37 liter
    The annual cost for just the diesel filling is 6261 dollar
    

**Safety Tanks for Diesel Transportation**

The shipment of diesel from Bolivia mainland to Suriqui would be a big issue. Since we already know that there is a regular transportation of food and other supplies to and fabrics and merchandise from the Suriqui Island, we assume we can just use this existing transportation as the shipping tool for the diesel. We just need to purchase a set of safety tanks for the transportation. 

Since we need at least 26.91 liter or 7.11 gallon diesel per day, we plan to purchase a set of 13-gallon safety tanks for diesel transportation from the mainland to the island. We choose RDS Aluminum Transfer Marine Fuel Tank — 13-Gallon, Rectangular, Smooth, Model# 59180. The price is 200 USD. We plan to get 10 of those first every 5 years. 


Quoted from a traveler in Bolivia, "the Bolivian diesel has high sulphur which in some cases can permanently damage the vehicle’s diesel filter." Due to the similar potential damage to the engine machine and the fact that the warranty only covers one year, we assume there is a repurchase for two every 5 year. 

**Total Cost**


```python
price_diesel_pump = 2957*u.USD
# Refer to the tank website under Citation
price_diesel_tank = 200*u.USD
total_cost_diesel = annual_cost_diesel*30+price_diesel_pump*2*(30/5)+price_diesel_tank*10*(30/5)

print('The total cost for thirty years then will be',ut.sig(total_cost_diesel,6))
```

    The total cost for thirty years then will be 235316 USD
    

### Maintenance & Concerns

The maintenance for the diesel-based water pump focuses on: 

1. Piping valves
2. Pump Controller 
3. Water Supplies
4. Pump Temperature 
5. Pressure Relief
6. Pump Cooling, etc. 

The main concern about the diesel-based water pump is about the potential pollution and safety issues about the diesel use. 

### In short ...

The total cost of diesel-based pumping system will be around 201,281 USD for the 30-year plan and that cost includes the purchase of fuel, pumps, and safety tanks in transportation. We neglect the actual transportation cost here, which might be a big issue for other islands, since the island itself already has a regular transportation system. 

**Pros**: 
1. 7/24 Operation and easy operation techniques
1. No storage tanks needed 
1. Fair prices for the diesel-based pumps

**Cons**:
1. $$$
1. Poor quality of diesel supplies in Bolivia
1. Unpredictable future diesel import from Chile

## Solar Energy 




**Introduction**:

Solar Economic analysis keeps the goal of delivering a 6L/s plant. 

This analysis includes the cost of building a tank so that the solar panels can pump the required daily water while there is sun, and store it so that we can have a constant flow of 6 L/s. In addition, this analysis includes the cost of a pump through the system's lifetime. In the case of the water storage option, we only consider one tank, which stores dirty water so that the flow can be a constant 6 L/s throughout the day. 

We also did a second analysis where we compared the storage tank option to a battery system that stores electricity during the day so that the pump can meet the 6 L/s rating throughout the entire day. Introducing this battery system eliminates the need for a storage tank, because we can power the pump during the night with the stored energy from the day. 

Overall, the system with the batteries is more cost-efficient and has the ability to expand to supply electricity to the island in the future if that is desired.


```python
# According to Francis Vanek in his renewable energy book, the price per installed watt for solar is $1.50
# The average sunlight hours per day is from La Paz, a close city and is from this website http://www.la-paz.climatemps.com/sunlight.php
# The energy efficiency claimed by the company that makes the pump is 85% 

Efficiency_solar_pump = .85 

Pwr_needed_solar_pump = (Power_needed + ((1-Efficiency_solar_pump)*Power_needed)).to(u.watt)
print('The required power input for the pumping system is', Pwr_needed_solar_pump)

Pwr_needed_solar_pump_year = (Pwr_needed_solar_pump*24*365).to(u.MW)
print('The required power needed for the year so we can size the system is', Pwr_needed_solar_pump_year)

```

    The required power input for the pumping system is 4330 watt
    The required power needed for the year so we can size the system is 37.93 megawatt
    


```python
# here is a very usefull data set I used based off of solar insolation of La Paz
Solar_data_LaPaz = pd.read_csv('pvwatts_hourly-4540.csv',header=17,nrows=8760)
Solar_data_LaPaz[Solar_data_LaPaz.columns[1:11]]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Day</th>
      <th>Hour</th>
      <th>Beam Irradiance (W/m^2)</th>
      <th>Diffuse Irradiance (W/m^2)</th>
      <th>Ambient Temperature (C)</th>
      <th>Wind Speed (m/s)</th>
      <th>Plane of Array Irradiance (W/m^2)</th>
      <th>Cell Temperature (C)</th>
      <th>DC Array Output (W)</th>
      <th>AC System Output (W)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.5</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4.4</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.4</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>4.4</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.4</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>4.5</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.5</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>4.6</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.6</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>4.6</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.6</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>6</td>
      <td>0</td>
      <td>13</td>
      <td>5.2</td>
      <td>0.0</td>
      <td>11.48</td>
      <td>1.494</td>
      <td>74.51</td>
      <td>37.53</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>7</td>
      <td>0</td>
      <td>100</td>
      <td>5.4</td>
      <td>0.0</td>
      <td>91.43</td>
      <td>5.328</td>
      <td>583.8</td>
      <td>536.7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>8</td>
      <td>5</td>
      <td>199</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>184.5</td>
      <td>11.9</td>
      <td>1.144e+03</td>
      <td>1.084e+03</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>9</td>
      <td>21</td>
      <td>275</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>264.4</td>
      <td>17.16</td>
      <td>1.601e+03</td>
      <td>1.53e+03</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>10</td>
      <td>7</td>
      <td>353</td>
      <td>10.0</td>
      <td>0.0</td>
      <td>325.2</td>
      <td>23.12</td>
      <td>1.917e+03</td>
      <td>1.837e+03</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>11</td>
      <td>9</td>
      <td>395</td>
      <td>11.0</td>
      <td>0.0</td>
      <td>365.1</td>
      <td>26.05</td>
      <td>2.123e+03</td>
      <td>2.037e+03</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>12</td>
      <td>9</td>
      <td>411</td>
      <td>11.0</td>
      <td>3.6</td>
      <td>380.1</td>
      <td>18.94</td>
      <td>2.285e+03</td>
      <td>2.194e+03</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1</td>
      <td>13</td>
      <td>9</td>
      <td>400</td>
      <td>10.5</td>
      <td>3.3</td>
      <td>369.7</td>
      <td>18.49</td>
      <td>2.227e+03</td>
      <td>2.138e+03</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1</td>
      <td>14</td>
      <td>7</td>
      <td>363</td>
      <td>10.0</td>
      <td>3.1</td>
      <td>334.2</td>
      <td>17.3</td>
      <td>2.024e+03</td>
      <td>1.941e+03</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1</td>
      <td>15</td>
      <td>22</td>
      <td>289</td>
      <td>10.0</td>
      <td>2.6</td>
      <td>278.1</td>
      <td>16.24</td>
      <td>1.691e+03</td>
      <td>1.618e+03</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1</td>
      <td>16</td>
      <td>12</td>
      <td>213</td>
      <td>8.4</td>
      <td>3.1</td>
      <td>201.3</td>
      <td>12.25</td>
      <td>1.246e+03</td>
      <td>1.184e+03</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1</td>
      <td>17</td>
      <td>0</td>
      <td>122</td>
      <td>7.9</td>
      <td>5.2</td>
      <td>111.7</td>
      <td>8.97</td>
      <td>702.1</td>
      <td>652.5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1</td>
      <td>18</td>
      <td>0</td>
      <td>26</td>
      <td>7.4</td>
      <td>5.2</td>
      <td>23.02</td>
      <td>6.612</td>
      <td>146.2</td>
      <td>107.9</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1</td>
      <td>19</td>
      <td>0</td>
      <td>0</td>
      <td>6.7</td>
      <td>2.5</td>
      <td>0.0</td>
      <td>6.7</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1</td>
      <td>20</td>
      <td>0</td>
      <td>0</td>
      <td>6.7</td>
      <td>3.6</td>
      <td>0.0</td>
      <td>6.7</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>4.2</td>
      <td>5.9</td>
      <td>0.0</td>
      <td>4.2</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1</td>
      <td>22</td>
      <td>0</td>
      <td>0</td>
      <td>3.9</td>
      <td>7.4</td>
      <td>0.0</td>
      <td>3.9</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1</td>
      <td>23</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>4.8</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4.5</td>
      <td>1.4</td>
      <td>0.0</td>
      <td>4.5</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>5.4</td>
      <td>1.2</td>
      <td>0.0</td>
      <td>5.4</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>5.7</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>5.7</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>6.1</td>
      <td>0.8</td>
      <td>0.0</td>
      <td>6.1</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>6.6</td>
      <td>0.6</td>
      <td>0.0</td>
      <td>6.6</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>6.1</td>
      <td>0.4</td>
      <td>0.0</td>
      <td>6.1</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>8730</th>
      <td>30</td>
      <td>18</td>
      <td>0</td>
      <td>22</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>19.46</td>
      <td>5.115</td>
      <td>124.4</td>
      <td>86.48</td>
    </tr>
    <tr>
      <th>8731</th>
      <td>30</td>
      <td>19</td>
      <td>0</td>
      <td>0</td>
      <td>6.4</td>
      <td>3.1</td>
      <td>0.0</td>
      <td>6.4</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8732</th>
      <td>30</td>
      <td>20</td>
      <td>0</td>
      <td>0</td>
      <td>6.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8733</th>
      <td>30</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8734</th>
      <td>30</td>
      <td>22</td>
      <td>0</td>
      <td>0</td>
      <td>5.7</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.7</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8735</th>
      <td>30</td>
      <td>23</td>
      <td>0</td>
      <td>0</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8736</th>
      <td>31</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8737</th>
      <td>31</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4.8</td>
      <td>4.1</td>
      <td>0.0</td>
      <td>4.8</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8738</th>
      <td>31</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8739</th>
      <td>31</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>7.2</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8740</th>
      <td>31</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>4.1</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8741</th>
      <td>31</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>3.0</td>
      <td>4.1</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8742</th>
      <td>31</td>
      <td>6</td>
      <td>0</td>
      <td>12</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.59</td>
      <td>0.019</td>
      <td>69.19</td>
      <td>32.31</td>
    </tr>
    <tr>
      <th>8743</th>
      <td>31</td>
      <td>7</td>
      <td>0</td>
      <td>97</td>
      <td>5.4</td>
      <td>0.0</td>
      <td>88.45</td>
      <td>5.139</td>
      <td>565.2</td>
      <td>518.6</td>
    </tr>
    <tr>
      <th>8744</th>
      <td>31</td>
      <td>8</td>
      <td>13</td>
      <td>193</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>183.5</td>
      <td>13.8</td>
      <td>1.127e+03</td>
      <td>1.068e+03</td>
    </tr>
    <tr>
      <th>8745</th>
      <td>31</td>
      <td>9</td>
      <td>8</td>
      <td>285</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>264.4</td>
      <td>19.12</td>
      <td>1.588e+03</td>
      <td>1.517e+03</td>
    </tr>
    <tr>
      <th>8746</th>
      <td>31</td>
      <td>10</td>
      <td>8</td>
      <td>355</td>
      <td>11.4</td>
      <td>0.0</td>
      <td>327.9</td>
      <td>24.58</td>
      <td>1.92e+03</td>
      <td>1.84e+03</td>
    </tr>
    <tr>
      <th>8747</th>
      <td>31</td>
      <td>11</td>
      <td>9</td>
      <td>398</td>
      <td>12.0</td>
      <td>0.0</td>
      <td>367.9</td>
      <td>27.14</td>
      <td>2.128e+03</td>
      <td>2.042e+03</td>
    </tr>
    <tr>
      <th>8748</th>
      <td>31</td>
      <td>12</td>
      <td>9</td>
      <td>414</td>
      <td>13.0</td>
      <td>4.1</td>
      <td>382.8</td>
      <td>20.61</td>
      <td>2.284e+03</td>
      <td>2.193e+03</td>
    </tr>
    <tr>
      <th>8749</th>
      <td>31</td>
      <td>13</td>
      <td>9</td>
      <td>402</td>
      <td>12.7</td>
      <td>3.1</td>
      <td>371.6</td>
      <td>20.91</td>
      <td>2.213e+03</td>
      <td>2.125e+03</td>
    </tr>
    <tr>
      <th>8750</th>
      <td>31</td>
      <td>14</td>
      <td>7</td>
      <td>364</td>
      <td>13.0</td>
      <td>3.0</td>
      <td>335.2</td>
      <td>20.4</td>
      <td>2.001e+03</td>
      <td>1.919e+03</td>
    </tr>
    <tr>
      <th>8751</th>
      <td>31</td>
      <td>15</td>
      <td>22</td>
      <td>288</td>
      <td>12.0</td>
      <td>0.0</td>
      <td>277.2</td>
      <td>23.9</td>
      <td>1.628e+03</td>
      <td>1.556e+03</td>
    </tr>
    <tr>
      <th>8752</th>
      <td>31</td>
      <td>16</td>
      <td>11</td>
      <td>211</td>
      <td>11.8</td>
      <td>3.1</td>
      <td>198.8</td>
      <td>15.6</td>
      <td>1.212e+03</td>
      <td>1.151e+03</td>
    </tr>
    <tr>
      <th>8753</th>
      <td>31</td>
      <td>17</td>
      <td>0</td>
      <td>115</td>
      <td>11.0</td>
      <td>3.0</td>
      <td>104.9</td>
      <td>12.33</td>
      <td>649.6</td>
      <td>601.2</td>
    </tr>
    <tr>
      <th>8754</th>
      <td>31</td>
      <td>18</td>
      <td>0</td>
      <td>23</td>
      <td>8.5</td>
      <td>3.0</td>
      <td>20.35</td>
      <td>7.443</td>
      <td>128.8</td>
      <td>90.78</td>
    </tr>
    <tr>
      <th>8755</th>
      <td>31</td>
      <td>19</td>
      <td>0</td>
      <td>0</td>
      <td>7.8</td>
      <td>3.1</td>
      <td>0.0</td>
      <td>7.8</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8756</th>
      <td>31</td>
      <td>20</td>
      <td>0</td>
      <td>0</td>
      <td>7.1</td>
      <td>5.1</td>
      <td>0.0</td>
      <td>7.1</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8757</th>
      <td>31</td>
      <td>21</td>
      <td>0</td>
      <td>0</td>
      <td>6.2</td>
      <td>3.6</td>
      <td>0.0</td>
      <td>6.2</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8758</th>
      <td>31</td>
      <td>22</td>
      <td>0</td>
      <td>0</td>
      <td>5.5</td>
      <td>5.1</td>
      <td>0.0</td>
      <td>5.5</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8759</th>
      <td>31</td>
      <td>23</td>
      <td>0</td>
      <td>0</td>
      <td>4.9</td>
      <td>5.1</td>
      <td>0.0</td>
      <td>4.9</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>8760 rows × 10 columns</p>
</div>



**Sizing requirement of the solar panels**


```python
# We assume the power required to supply the pump is equivilent to solar data for the year. 
# The hourly-based ratio from spread sheet below shows that a 6.4 KW system produces 7496101.843 watts in La Paz 
# with required rerating factors. 
# Therefore, to find the required size of the solar system, we just apply the same ratio with the power needed. 

example_size_lapaz = 6.4*u.kwatt # See the header of csv file 
year_output_data = np.array(Solar_data_LaPaz['AC System Output (W)'])*u.W
year_output_total = np.sum(year_output_data)
print('The yearly total output is',year_output_total)

# 6.4 kW/7496101.843 W = req_sizing/Pwr_needed
req_sizing = ((example_size_lapaz /year_output)*Pwr_needed_solar_pump_year).to(u.kW)
Solar_Var_safety_factor = 1.1
```

    The yearly total output is 7.496e+06 watt
    


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-12-6c5e0316a60a> in <module>()
         10 
         11 # 6.4 kW/7496101.843 W = req_sizing/Pwr_needed
    ---> 12 req_sizing = ((example_size_lapaz /year_output)*Pwr_needed_solar_pump_year).to(u.kW)
         13 Solar_Var_safety_factor = 1.1
    

    NameError: name 'year_output' is not defined


**Pump cost**

The pump we choose is 240VAC Totally Enclosed Fan-Cooled Centrifugal Pump, 1-Phase, 2" NPT Inlet Size. 
![Alt text](https://static.grainger.com/rp/s/is/image/Grainger/1N487_AS01?hei=800&wid=935)


```python
cost_pump = 3348*u.dollars
# last_5_years so over 30 years need 6 pumps at most 
life_time_cost_pump = 6*cost_pump
print('The life time cost for the pump is',ut.sig(life_time_cost_pump,5))
```

The cost above is the same for either the storage tank method or the battery method. We will start discussing the difference of two methods as below. 

**Cost of Storage tank**


```python
size_req_solar_var = Solar_Var_safety_factor*req_sizing
size_req_solar_var_for_storage_tank_option = size_req_solar_var

Cost_Intalled_solar_per_watt = 1.5*u.dollars
cost_Solar_Panels_for_storage_tank_option = Cost_Intalled_solar_per_watt*(size_req_solar_var.magnitude)*1000
print('The rating size of the solar system for the storage tank option is',size_req_solar_var_for_storage_tank_option)
print('The cost for the instaliation of the solar system for the storage tank option is', ut.sig(cost_Solar_Panels_for_storage_tank_option,6))

# Water Tank 
avg_hours_sun_day = 12.12*u.h
ratio = (24*u.h/avg_hours_sun_day)
tot_wat_req = ratio*req_water
ability_store = tot_wat_req-req_water
seconds_day = (1*u.day).to(u.s)
tank_capac = (ability_store*seconds_day)
Cost_tank = .1135*u.dollar/u.L*tank_capac # Check the source below
print('The cost of a water tank is',ut.sig(Cost_tank,6))
```

### Total cost of the system with a tank in place powered by solar energy


```python
Total_cost_with_tank_system = life_time_cost_pump+cost_Solar_Panels_for_storage_tank_option+cost_Tank
print('The total proposed cost of the system with a tank over 30 years is',ut.sig(Total_cost_with_tank_system,6))
```

**Cost of the battery system**


```python
# The battery system is 90% efficient 
Extra_electricy_factor_batteries = 1.1
size_req_solar_var_for_battery_option = size_req_solar_var*Extra_electricy_factor_batteries
cost_Solar_Panels_for_battery_option = Cost_Intalled_solar_per_watt*size_req_solar_var_for_battery_option.magnitude*1000

print('The rating size of the solar system coupled with batteries due to inneficiencies is',size_req_solar_var_for_battery_option)
print('The cost for the instaliation of the solar system coupled with batteries due to inneficiencies is', ut.sig(cost_Solar_Panels_for_battery_option,5))

Battery_cost = 5500*u.dollars # Check Source below
Supporting_hardware = 700*u.dollars # Check Source below
Life_time_battery = 15*u.years # Check Source below
Time_use = 30*u.years
Cost_battery_system = (Battery_cost + Supporting_hardware)*(Time_use/Life_time_battery)

print('The cost of the battery system over 30 years is', ut.sig(Cost_battery_system,5))
```

### Total cost of the system with a battery system powered by solar energy


```python
Total_cost_with_battery_system = life_time_cost_pump + Cost_battery_system + cost_Solar_Panels_for_battery_option
print('The total proposed cost of the system with a battery system over 30 years is', ut.sig(Total_cost_with_battery_system,5))
```

### In Short... 

Based on the analysis comparing the solar system paired with a tank to the battery system option, we think that the battery option makes more sense because of many reasons.

**Pros**:
1. Less expensive
2. More sustainable
3. Less construction
4. Eliminates issue of variability
5. Ability to expand and produce electricity for island

**Cons**:
1. 10% energy loss from input of battery to usable energy
2. Specialized operator education 
3. Possibly high installation cost in Bolivia

# Conclusion 

Team Ssssnakes made a descriptive and numeric analysis on the centralized water treatment plant in Suriqui Island. We pick an appropriate location for the water input and calculate the desired elevation of the wtp. We then conduct cost-effective analysis for two energy-based pumps: diesel and solar energy. In short, our team believes the solar-based pumping system equipped with solar battery is the best option for Suriqui and the estimated cost is 61887 USD.

# Suggestions for Future Work

The future research analysts should study the economic and sociological cost of having multiple water treatment plants on the island, and compare that with the results of this study. The multiple plants design is assumed to have less distribution systems, but more operation and construction costs. In addition, the future teams could analyze the unit price of water and the associated logistics. A detailed plant design should be provided to the community. Finally if the solar system paired with batteries is chosen, it might be able to provide a starting place for also supplying electricity to the community. 

# Citation

Source: Google Earth

[Capstone Design Ideas 17](https://confluence.cornell.edu/display/cee4540/Capstone+Design+Ideas+17)

[Bolivian Online](http://www.bolivia-online.net/en/la-paz/134/lake-titicaca-the-islands)

[Bolivian Average Wage](http://www.averagesalarysurvey.com/bolivia)

[Average Water usage per capita](http://isu.indstate.edu/disrael/h20_jed_fig.pdf)

[Diesel & Fuel Issues in Bolivia](http://www.overlanddiaries.com/diesel-fuel-issues-in-bolivia/)

[Diesel Pump](https://www.absolutewaterpumps.com/multiquip-water-pump-qp2tk-172-gpm-2-diesel-trash-pump)

[Pump Testing and Maintainence Checklist](http://www.ppsa.org/assets/SafetyMaterialsandGuide/fm_fire_pump_inspection_checklist_and_form.pdf)

[Storage Tank](https://www.paawwa.org/wp-content/uploads/2013/06/22Hershey.pdf)

[Tesla Battery](https://www.tesla.com/powerwall)

[Additional Source](https://confluence.cornell.edu/download/attachments/350945826/EIA%20Bolivia.zip?version=1&modificationDate=1508334009000&api=v2)
