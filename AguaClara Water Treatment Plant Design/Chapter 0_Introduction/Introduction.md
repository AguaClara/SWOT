# Introduction to AguaClara Water Treatment Design

## The Global Context

The [Sustainable Development Goals: SDGs](https://www.un.org/sustainabledevelopment/sustainable-development-goals/) and specifically [SDG 6](https://www.un.org/sustainabledevelopment/water-and-sanitation/) provide the context and motivation for this text. The first SDG 6 target is: "By 2030, achieve universal and equitable access to safe and affordable drinking water for all." That goal is daunting and won't be met using the approaches of the past 5 decades. This text is about creating a new paradigm for the design of high performing water treatment technologies.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/SDG6.png" width="200">

The number of people who currently lack access to reliable safe water on tap is not known. Estimates range from "[1.8 billion who use a source of drinking water that is fecally contaminated](https://www.un.org/sustainabledevelopment/water-and-sanitation/#)" to the Centers for Disease Control recommendations for where it is [usually safe to drink tap water](https://lifehacker.com/know-what-countries-guarantee-drinkable-tap-water-with-1635070463).

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/CDC%20Global%20Safe%20Tap%20Water.png" width="600">

Figure 1. There are relatively few countries where it is almost always safe to drink the tap water.

The [UN estimate in 2017](https://www.un.org/sustainabledevelopment/blog/2017/07/billions-around-the-world-lack-safe-water-proper-sanitation-facilities-reveals-un-report/) was that 2.1 billion lack access to safe water. By 2030 there will be an additional [1.2 billion from population growth](https://news.un.org/en/story/2015/07/505352-un-projects-world-population-reach-85-billion-2030-driven-growth-developing).

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/Population-Infographic-01.jpg" width="300">


Thus by 2030 we need to provide safe water for at least 3.3 billion people AND maintain the water supply systems for the 5.2 billion who currently have access to safe water.

```python
from aide_design.play import*
import datetime
People_needing_water_2030 = 3.3*10**9
now = datetime.datetime.now()
Task_time = (2030 - now.year)*u.year
#If we assume we will meet this demand by building the same amount of new capacity each year, then we have
People_per_year = People_needing_water_2030/Task_time
People_per_year
#The percapita demand for water
Per_capita_demand = 3*u.mL/u.s
Per_capita_demand.to(u.L/u.day)
Rate_new_water_supply_capacity = (People_per_year * Per_capita_demand).to(u.L/(u.s*u.year))
Rate_new_water_supply_capacity
#
NYC_water_supply = 44000 * u.L/u.s
NYC_per_year = Rate_new_water_supply_capacity/NYC_water_supply
NYC_per_year
```
If we provide 260 L/day per person, then we need to provide the equivalent of 19 water supplies for New York City **every year** between now and 2030.

The need for drinking water supplies isn't limited to the global south. The California Urban Water Agencies [estimate that 530,000 or more people in rural areas of California are unable to turn on their tap and access clean, safe water](https://static1.squarespace.com/static/5a565e93b07869c78112e2e5/t/5a5965934192024b3f610be1/1515808194305/CUWA2017_AnnualReport.pdf).

## Why don't 2 billion people have access to safe water?

## History of Surface Water Treatment Technologies

| Technology | Description | Prerequisite | Owner | Year |
| - | - | - | - | - |
| simple sedimentation | particles settle | none | public | unknown |
| Flocculation | aluminum and iron salts | none | public | [1757](https://www.iwapublishing.com/news/coagulation-and-flocculation-water-and-wastewater-treatment) |
| Sedimentation | horizontal flow | flocculation | public | unknown |
| Lamellar sedimentation | plate or tube settlers | flocculation or floc blanket | public | [1904](http://www.hydroflotech.com/inclined-plate-clarifier-basic-theory-of-operation) |
| Slow sand filtration | single step treatment for low NTU water | none | public | [1829](https://en.wikipedia.org/wiki/Slow_sand_filter) |
| Rapid sand filtration |depth filtration | sedimentation | public | [1920](https://en.wikipedia.org/wiki/Rapid_sand_filter) |
| Stacked rapid sand filter | gravity powered backwash | lamellar sedimentation | AguaClara Cornell open source | [2012](https://ascelibrary.org/doi/abs/10.1061/%28ASCE%29EE.1943-7870.0000562) |
| Floc blanket | upflow fluidized suspension of flocs | flocculation | public | [1930](https://link.springer.com/chapter/10.1007%2F978-3-642-61196-4_2) |
| Jet reverser floc blanket | first fully fluidized floc blanket | flocculation | AguaClara Cornell open source | [2012](http://cuaguaclara.blogspot.com/2012/08/the-floc-blanket-quest.html) |
| Ballasted sedimentation | - | - | [Actiflo Veolia](http://www.veoliawatertechnologies.com.au/medias/topics/focus_actiflo.htm) | [1995](https://patents.google.com/patent/US5840195) |
| Superpulsator | pulsing flow through floc blanket | rapid mix | [Degremont](http://www.degremont-technologies.com/SUPERPULSATOR-R) | [1958](https://patents.google.com/patent/US3038608A) [1991](https://patents.google.com/patent/US5143625) |
| Dissolved air flotation | - | - | - | - |
See [Pretreatment Processes for Potable Water Treatment Plants by Jeff Lindgren for an excellent overview of available technologies, May 2014 (not including AguaClara innovations)](https://www.pnws-awwa.org/uploads/PDFs/conferences/2014/2.%20PNWS%20AWWA%20WTC%20Precon%2005%2007%202014%20Pretreatment%20by%20B&V%201&2%20-%20R1.pdf)


## Treatment Trains
The prerequisites in the table above reveal that surface water treatment almost always requires a series of treatment steps.

## Design Evolution

During the later half of the 20th century surface water treatment technologies evolved slowly. The slow evolution was likely a product of the regulatory environment, the high cost of water treatment infrastructure, and the low profit margin. The high cost of municipal scale water treatment infrastructure made experiments at scale infeasible and thus there was no mechanism to introduce disruptive innovations. With little opportunity for a significant return on investment there was little incentive to invest in the research and development that could have advanced the technologies. A final disincentive was the widely held belief that surface water treatment was a mature field with little opportunity for significant advancement. The advances of the latter half of the 20th century focused primarily on mechanization and automation (Supervisory Control and Data Acquisition - SCADA).

Design standards such as the [Great Lakes - Upper Mississippi River Board 10 States Standards](http://10statesstandards.com/) are evolving very slowly and retain an empirical approach to design. The empirical design methodology is a direct result of two confounding factors. The physics of particle interactions based on diffusion, fluid shear, and gravity are complex and given the challenges of characterizing surface water particle suspensions it was natural to assume that a mathematical description of the processes would be intractable.    

Mechanized and automated water treatment plants performed reasonably well in communities with ready access to technical support services and supply chains that could reliably deliver replacement parts. In the global south municipal water treatment plants haven't faired as well. In 2012, one of the main water treatment plants serving Kathmandu, Nepal had failed chlorine pumps and were using a red garden hose to siphon chlorine from the stock tank. They crimped the end of the hose to control the flow rate of the chlorine solution.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/Kathmandu_chemical_feed_room.png" width="400">

Figure 1. Failed chlorine doing system bypassed with a red tube that siphons the chlorine solution at a plant in Kathmandu, Nepal in 2012.

The ingenious and simple chemical dosing system that uses a siphon to completely bypass the failed pumps begs the question of whether design engineers could have invented a better option than the short lived pumps that they specified. We will investigate a gravity powered chemical dosing system that is far more reliable than chemical dosing pumps and that borrows from the simplicity of the garden hose solution used by the Nepali plant operators.

Chemical dosing systems are particularly vulnerable and their failures make plant operation very challenging. Providing the right coagulant dose is critical for efficient removal of particle and dissolved organics. Chemical dosing systems commonly rely on pumps and those pumps require regular maintenance and have relatively short mean times between failures.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/Kathmandu_alum_dosing.jpg" width="200">

Figure 2. Alum dosing system based on the rate that 25 kg block of alum are placed in the inlet channel of the plant.

The AguaClara Cornell program was founded in 2005 with the goal of creating a new generation of sustainable technologies that would perform well even in the rugged settings of rural communities. The goal wasn't simply to create technologies that would work for communities with very limited resources. The goal was to create the next generation of technologies that would both perform well in communities with limited resources and would be the highest performing technologies on multiple metrics for all communities.

## Empirical Design
For the past several decades surface water treatment technologies have been considered "mature" and when I (Monroe) took a design course on drinking water treatment in 1985 I had the impression that there was little room for further innovation. This perspective is remarkable given that with the exception of lamellar sedimentation there were no equations describing the core treatment processes.

Empirical design guidelines don't provide insight into how designs could be optimized or even what the performance of a water treatment plant will be. Thus designers can't compare alternative designs because

## Design for the Financers, Venders, Client, or Context
Tours of water treatment plants suggest that it is common for designs to be driven by the vender goal of a stable revenue stream for replacement parts rather than by a goal of meeting the client's needs. Mandatory software upgrades, mechanical valves, chemical pumps, mixing units provide a steady demand for proprietary components. Financers often prefer projects that can be implemented quickly either because they have target expenditures for a fiscal year or because loan repayment begins when the facility is turned over to the client.

Design for the client would strive to reduce capital, operating, and maintenance expenses. Clients also place a high value on reliability, ease of maintenance, and the ability to handle repairs with their staff. Design for the context would account for the capabilities of local and national supply chains. A key design consideration is to ensure that the treatment capabilities of the treatment plant match the variable water quality of the proposed water source. There are numerous slow sand filtration plants installed in the global south that are attempting to treat water sources that can not be effectively treated by slow sand filtration. The cost of the failure to consider the client and the context is born by the communities who end up with water treatment systems that aren't able to provide reliable safe water.

Design for the client requires empathy and a commitment to listen to and learn from plant operators. It also requires attention to detail and watching how plant operators interact with water treatment plants. Empathy leads to the goal of creating a work environment that makes it easy for the plant operators to do their routine tasks. This isn't just to make the plant operators work easy. A plant that is designed with the plant operator in mind will also engender pride and that pride will lead to better plant performance.

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/Improvised%20ladder%20access%20to%20sed%20tank.jpg" width="400">

Figure x. A plant operator built a makeshift ladder to enable easier access to the flocculation and sedimentation tanks in a package plant. This ladder considerably shortened the distance between the coagulant dose controls and the observation of flocculation.


## Design Bifurcations
Seemingly small decisions can have a profound effect on the evolution of design. Traditionally in tropical and temperate climates, flocculation and sedimentation units are built without an enclosing building. Without protection from the sun the materials used for plant construction must be UV resistant and thus plastic can't be used. This requires use of heavier and more expensive materials such stainless steel and aluminum. Metal plate settlers are heavy and thus they can't be easily removed by the plant operator.

Conventional sedimentation tank cleaning must be done by providing operator access below the plate settlers. This in turn requires that the space below the plate settlers be tall enough to accommodate a plant operator. Thus sedimentation tanks that are built in the open have to be deeper than sedimentation tanks that are built under a roof and they are more difficult to maintain because the operator has to enter the tank through a waterproof access port.

[![Plant operators opening hatch below plate settlers](http://img.youtube.com/vi/TSh-ZNqaW8Y/0.jpg)](http://www.youtube.com/watch?v=TSh-ZNqaW8Y)

Figure 3. Plant operators opening hatch below plate settlers in a traditional sedimentation tank.


[![Plant operator removing plate settlers from an AguaClara sedimentation tank settlers](http://img.youtube.com/vi/vZ2f6mduEls/0.jpg)](http://www.youtube.com/watch?v=vZ2f6mduEls)

Figure 4. Plant operator removing plate settlers from an AguaClara sedimentation tank settlers.

Dramatically different designs are also created when we choose gravity power and smart fluids rather than electricity for each of the unit processes.

## Respect, Empathy, Love and Curiosity power the AguaClara Innovation System

The AguaClara network of organizations has been methodically inventing improved water treatment technologies since 2005. Our success is based on respect, empathy and love. Innovation requires flocculation of ideas. The transport of ideas between organizations and individuals is mediated by respect. Respect as a cornerstone of organizational culture foster rapid and honest exchange of ideas.

Any large organization will require a leadership hierarchy and any hierarchy will rely on respect based on fear or respect based on love. [Fear-based hierarchies](https://www.forbes.com/sites/lizryan/2015/11/25/the-five-characteristics-of-fear-based-leaders/#a6179f38a968) impede the accurate sharing of information and can easily devolve into data-free and low-truth decision-making schemes. According to [Liz Ryan](https://www.forbes.com/sites/lizryan/2015/11/25/the-five-characteristics-of-fear-based-leaders/#a6179f38a968), the characteristics of fear-based leaders include:
- They'll Teach You, Whether You Like It or Not
- Everyone is a Friend or a Foe
- It's All about the Trophies
- They Don't Step Outside Boxes
- They're Addicted to Yardsticks

Love-based hierarchies foster honesty and a free-flow of information. Reflection is encouraged across the organization and truth, honesty, and integrity are valued. Staff at the bottom of the hierarchy know that their opinions and reflections are valued and thus they will be willing to report problems to organization leaders.

Love-based leaders relate to others based on true respect for the other. They will take the time to converse with people at all levels of the organization and will value the opportunity to speak with people who are the interface between the organization and the rest of the world. A person's value is based on being a person, not based on position in the hierarchy.

As water treatment plant designers it is critical that we spend time with a diverse set of stakeholders including community members and water treatment plant operators. Those relationships must begin with respect and valuing their insights. As we spend time together we can develop trust so that they communicate both the good and bad.

We've learned much from plant operators. They figured out how to reduce rising flocs at Agalteca, Honduras where we learned that conventional sedimentation tank inlet manifolds generate large circulation currents. Plant operators added curtains to the windows at Moroceli, Honduras because they noticed that direct sunlight on the sedimentation tanks caused an increase in settled water turbidity.

Empathy enables us to consider reality from another's perspective. Empathy is fundamental in design. Empathy enables us to bring the people who will use or benefit from a technology into the design considerations. Empathy brings the insight that water treatment plants need to have roofs and provide a secure work environment both day and night. Empathy brings the insight that replacement parts must be readily available and that generic components are preferred over specialty proprietary components.

Curiosity can flourish in a culture of love, respect, and empathy. Asking why and why not and pondering an ever growing number of questions has empowered student teams to take on the quest for new knowledge and new solutions.

# Water Contaminants
"[Particles transported by rivers are composed of resistant primary minerals (e.g., quartz and zircon), secondary minerals (clays, metallic oxides and oxyhydroxides) and biogenic remains](https://www.sciencedirect.com/science/article/pii/S0048969708010103).
## Turbidity
Define Turbidity
Show optical systems
explain rough correlation with suspended solids concentration and why that relationship varies depending on the particle size distribution and density.
## Pathogens
Pathogens are particles
## Dissolved species
Natural Organic Matter (NOM) plays a supersized role in influencing performance of surface water treatment plants.
Discuss charge density.
Observed stabilization of inorganic particles
# History (chlorine saved the world)

<img src="https://github.com/AguaClara/CEE4540_Master/raw/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%200_Introduction/Images/US_infectious_diseases_death_rate.gif" width="600"> from https://www.cdc.gov/mmwr/preview/mmwrhtml/mm4829a1.htm
