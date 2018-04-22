
# Rural Drinking Water in Puerto Rico and AguaClara Feasibility

## Flamingos

### Ben Diskin, Clare O'Connor, Thomas Suesser

## Introduction

In Puerto Rico, the main state-operated water authority, PRASA, serves about 96% of the island's population through many water systems, the rest of the population is served by other systems which are referred to as non-PRASA. The 240 non-PRASA systems serve about 100,000 people and on average violate  water quality standards far more often than systems governed by PRASA, according to guidelines set by the Safe Water Drinking Act (SWDA). A goal of this report is to determine what is causing some of  these water systems to violate the SWDA and evaluate whether AguaClara 1 L/s plants would be a useful addition to some of the communities currently served by non-PRASA systems. An initial search found that 132 of the initial 240 are systems that serve fewer than 3000 people and rely on surface water.  From these systems, the number and type of violations was determined. Once an evaluation of the violations was completed we looked into the feasibility of 1 L/s plants in these communities based on resources, need, and what would be needed to have 1 L/s plants meet EPA standards. The reason we limited our search of the systems to 3000 people is due an estimate on the number of 1 L/s plants that could be run in parallel, as guessed by Monroe. Additionally, a map was created using ArcGIS to connect the communities, violations, and locations in one place and a brief cost analysis was done to create a framework for determining cost to construct and operate plants in Puerto Rico.

#### Acronyms:
    CCR: Consumer Confidence Reports
    EPA: U.S. Environmental Protection Agency
    FEMA: Federal Emergency Management Agency
    JCA: Junta de Calidad Ambiental de Puerto Rico (Environmental Quality Board)
    LCR: Lead and Copper Rule
    MCL: Maximum Contaminant Level
    MCLG: Maximum Contaminant Level Goal
    PRASA: Puerto Rico Aqueduct and Sewer Authority
    PWS: Public Water System
    RTCR: Revised Total Coliform Rule
    USGS: United States Geological Survey
    SDWA: Safe Drinking Water Act
   


#### Determination of location of non-PRASA drinking water systems and violations:

Using the Environmental Protection Agency's tool for locating [Consumer Confidence Reports (CCR)](https://ofmpub.epa.gov/apex/safewater/f?p=136:103:::NO:RP,103:P103_STATE:PR) , non-compliant, non-PRASA water systems were located. This tool provides information on most water systems in the United States. For this analysis, the search of reports was limted to communities in Puerto Rico using surface water and served populations less than 3000 people. Using these parameters, 132 water systems were identified. Of these, five were non-community water sources, and were removed from the set of systems to be mapped and analyzed. Of the remaining 127, 110 have had violations in the past five years preventing them from meeting EPA standards. Many of the violations are re-ocurring within the past five years and many systems, especially those serving smaller populations, have been in violation of some rules every month they are tested ([1](https://ofmpub.epa.gov/apex/safewater/f?p=ccr_wyl:102))



#### Water Auhorities in Puerto Rico
As with all US territories, Puerto Rican water systems are required to meet EPA conditions for drinking water as defined in the Safe Water Drinking Act (SWDA). The SWDA sets minimum criteria to be met in every water system. These regulations are called National Primary Drinking Water Standards (NPDWS), in addition to these primary criteria there are also National Secondary Drinking Water Standards (NSDWS), which are recommended by the EPA, but are not enforced on a national level. Most states and territories are allowed to implement and enforce the secondary standards. Puerto Rico has been afforded what is called 'primacy' and as such has the power to enforce the secondary standards. As water quality often operates from an environmental sector of government, the organization in Puerto Rico that monitors water quality is the Environmental Quality Board, in Spanish: the Junta de Calidad Ambiental de Puerto Rico (JCA). The board is tasked with monitoring bodies of water throughout PR for quality and works with PRASA and USGS to accomplish this. In addition to the JCA, the Puerto Rico Department of Health does quality sampling for many non-PRASA systems. 

#### Map of Relevant Water Systems

[ArcGIS map of relevant water systems]( http://www.arcgis.com/home/webmap/viewer.html?url=https://services1.arcgis.com/0Lw2m57KEotYYFaA/ArcGIS/rest/services/PR_system_map/FeatureServer&source=sd )


The map found at the above link shows the location of nearly all 132 of the water systems that meet our filter criteria. Each data point corresponds to one water system, and includes the following attributes: 
1. System Name
2. Population Served
3. Phone Number - the contact listed by the CCR report
4. Town Served - one of the 78 Puerto Rican municipalities, similar to counties in US states
5. Population Density - the 2010 census density for each of the above municipalities, in people per square mile.
6. Total Coliform >50 - A binary system; receives a “1” if this system had greated than 50 total coliform rule violations during our study period
7. Total Coliform >25 - Analogous to above.
8. Surface Water  - Receives a “1” if this system had any surface water rule violations during our study period
9. Lead and Copper - Receives a “1” if this system had any lead and copper rule violations during our study period


The map is publicly available at the link listed above, and simply contains the georeferenced points and their attributes. These points can be viewed overlaid on a variety of georeferenced “basemaps”, which ArcGIS online provides. Basemap options include satellite imagery, topographic maps, street and political maps, rendered terrain maps, and more. Within the ArcGIS online map viewer, data can be filtered and searched by any of the attribute categories, systems can also be labeled on the map, and other display options can be explored. The user is encouraged to “play” around with the map to learn how to best utilize its various capabilities. Start by hovering over the “PR system map” layer in “Contents” at the left hand side, and explore from there.

The locations of each point is not meant to be treated as exact, as the CCR database does not include coordinates of the water systems. Instead, these locations are based off of the addresses given in the database, searched using Google Maps. In nearly all cases, the points are located on the road and town given in the database, but the point on the road is approximate. In a few cases, the exact address was found on Google Maps. In the future, further information for any individual system can be added to the attributes of each point. 

The map aims to provide a visual and spatial tool for navigating between the different water systems that can be used publicly in the future as AguaClara continues to develop its efforts in Puerto Rico.


### Violations

A comprehensive list of violations for each plant was compiled using the EPA Water Systems Violation Report ([3](https://ofmpub.epa.gov/apex/sfdw/f?p=108:11:::NO:11,RIR:IREQ_PWSID:PR0004584)). This report serves as a database of all water quality violations that the EPA finds when inspectors go to plants around the United States and its territories and to check that the water is safe and clean for drinking. In this report, they provide a vast quantity of information, including the location of the given water treatment plant, the size of the population served, and further information regarding any violation of the water treatment rules. Further digging into this database, one can access all the data about the violations, which includes the specific rule violated, when the violation was documented, and the status of the violation, which could be open, known, or returned to compliance. Our search was limited to violations with known or open compliance, because plants with these violations are the plants that still have problems, and could therefore be a candidate for an AguaClara plant. Plants with open or known violations may also be dealing with enforcement of penalties through state or federal means. The EPA, when checking a plant, has a long list of violations and rules that it must check for, but many of these rules were non-existent in the plants in our search, so they are not included in the table below:


|| Lead and Copper|Long Term 2|Stage 1 + 2|Surface Water|Coliform Rule|Volatile Organic |Synthetic Organic | Nitrates| 
|:------------------:|:----------------------------:|:---------------------:|
|         Totals                            |             28   |62|21|16|3757|21|70|3|
|       Number of Plants with violation     |             22|4|10|5|83|1|1|1|
|       Average Violations per plant$^1$        |              1.27|15.5|2.1|3.2|45.27|21|70|3|
$^1$ Average over plants with violation present, not total plant number


The chart above shows the types of EPA violations found in the 132 water systems from our search. The types of rule violations are as follows: 

1. Lead and Copper Rule 	
2. Long Term 2 Enhanced Surface Water Treatment Rule
3. Surface Water Treatment Rule
4. Stage 1 and Stage 2 Disinfectants and Disinfection Byproducts Rule
5. Total Coliform Rule
6. Volatile Organic Chemicals
7. Synthetic Organic Chemicals
8. Nitrates

The data collected gives the total number of violations over the past 5 years (which may have be more than 1 violation for any given plant), the number of plants with the violation, and the average number of violations per plant. We limited our search to the most recent 5 years, because this time frame gives a window of the plant’s most recent violations, but can also show the scope of a problem, and can point out a plant the has had several violations of a specific category. This would be reflected in the average number of violations per plant. 

#### Total Coliform Rule

The most commonly violated regulation is the Total Colliform Rule. In a statement from the EPA the Total Colliform Rule is concerned with measuring a "group of related bacteria that are (with few exceptions) not harmful to humans" ([2](https://www.epa.gov/dwreginfo/revised-total-coliform-rule-and-total-coliform-rule)). Total coliforms (TC) are used as an indicator of other pathogens that may be present in drinking water. The limit on TC is that less than 5.0% of samples may be total coliform-positive (TC+) in a month; in small systems that collect fewer than 40 routine samples per month, no more than one sample may be TC+, this clause likely applies to every non-PRASA system in Puerto Rico based on national standards for testing. Any sample that tests TC+ must also be sampled for either fecal coliforms or E. coli. A violation occurs when there are two consecutive TC+ samples and one is also positive for E. coli fecal coliforms ([2](https://www.epa.gov/dwreginfo/revised-total-coliform-rule-and-total-coliform-rule)). Though not inherently harmful, the presence of coliforms indicate with high likelihood that other pathogens may be present in the water system. This is the reason all TC+ results are addtiionally tested for fecal contamination and E. coli, which indicate that contamination from an external source is present. 

#### Lead and Copper Rule

Another rule prevalent in a many systems, and is in the open compliance category is the Lead and Copper Rule (LCR). According to an NRDC fact sheet many of these violation exist due to a lack of testing, which results in a failure to meet this rule ([8](https://www.nrdc.org/sites/default/files/threats-on-tap-drinking-water-puerto-rico-ip.pdf)). However several of the failures are due to inadequate levels of contaminants in the water.  Specific standards are set by the EPA; for lead, the maximum limit is 15 parts per billion (ppb) and for copper, the maximum limit is 1.3 parts per million (ppm)([4](https://www.epa.gov/sites/production/files/2015-11/documents/howepargulates_cfr-2003-title40-vol20-part141_0.pdf)). Additonally, testing for these contaminants requires testing of water in the pipes of the water treatment system, as well as testing water at the taps of sites served by the system ([4](https://www.epa.gov/sites/production/files/2015-11/documents/howepargulates_cfr-2003-title40-vol20-part141_0.pdf)). If either the water in the treatment system fails to meet the requirements or an excess of 10 percent of the sampled taps fail to meet the requirements, the treatment plant is responsible for taking corrective actions. These actions can include educating the public on reducing lead exposure, optimizing corrosion control treatment, or replacing service and distribution pipes that it can access. Corrosion of metal pipes are usually the source of the lead and copper, and replacing contaminating and out-of-date pipes is imperative to provide clean drinking water. 

The health risks associated with heightened levels of lead and copper in water can be severe. Both metals can enter the body through breathing or eating and drinking, and they build up over time ([5](http://www.health.state.mn.us/divs/eh/water/factsheet/com/leadcopper.pdf)). As copper builds up, it can cause serious vomiting, nausea and diarrhea. Further and higher levels of exposure can cause liver and kidney damage as well. Lead is also a very dangerous metal to have in the body; it can have detrimental effects on the brain, nervous system, blood cells and kidneys. It can also hinder growth and development of infants exposed ([5](http://www.health.state.mn.us/divs/eh/water/factsheet/com/leadcopper.pdf)). 

#### Surface Water Treatment Rule

Originally established in 1989, the Surface Water Treatment Rule (SWTR) was established to treat water for waterborne diseases, specifically diseases caused by viruses, Legionella, and Giardia lamblia. This rule specifically applies to surface water or groundwater under the direct influence of surface water. It was later followed up by more targeted rules, including the Long Term 2 Surface Water Treatment Rule, which is discussed in more detail in a later section. 

The specific requirements of the SWTR are, as summed up by the EPA SWTR fact sheet ([9](https://www.epa.gov/sites/production/files/documents/SWTR_Fact_Sheet.pdf)).

1. At least 99.9% (3-log) removal and/or inactivation of Giardia lamblia cysts through filtration and inactivation (disinfection) barriers
2. At least 99.99% (4-log) removal and/or inactivation of viruses through filtration and inactivation (disinfection) barriers

The rule also sets in place requirements for turbidity based on the filtration system, and again are summed up based on the EPA fact sheet below:

- **Conventional and direct filtration**: The turbidity level of representative samples of CFE must be less than or equal to 0.3 NTU in at least 95% of the measurements taken each month; the maximum limit of any one sample is 1 NTU.
- **Slow sand and diatomaceous earth (DE) filtration**: The turbidity level of representative samples of CFE must be less than or equal to 1 NTU in at least 95% of the measurements taken each month; the maximum limit of any one sample is 5 NTU
- **Membrane and Bag/Cartridge (BC) filtration**: The turbidity level of representative samples of CFE must be less than or equal to 0.3 NTU in at least 95% of the measurements taken each month; the maximum limit of any one sample of BC filtration is 5 NTU and the maximum limit of any one sample of membrane filtration is 1 NTU. 

The final piece of the rule sets in place the disinfection residual concentration, which must not be less than 0.2 mg/L at the entrance of the system and must be detectable at some level throughout. The rule sets in place monitoring standards so that the systems can be continually checked for all of these conditions, which allow the water to be safe.

These treatment standards make the water safe from most waterborne diseases, and especially focus on the specific parasite Giardia, which is found in water that has been contaminated by feces. When it infects people, it can cause diarrhea, nausea, and dehydration, and can last anywhere from 2 to 6 weeks, according to the Center for Disease Control (CDC) ([10](https://www.cdc.gov/parasites/giardia/general-info.html)). People most at risk are children, especially diaper-aged, and people who drink untreated or poorly treated water. Keeping this parasite, and other viruses out of the water through proper treatment methods will keep users of the water safe and healthy.

#### Stage 1 and Stage 2 Disinfectants and Disinfection Byproducts Rules

The  Stage 1 and Stage 2 Disinfectants and Disinfection Byproducts Rules were both rules created in 1998 and 2006 respectively to reduce exposure to disinfectants and disinfection byproducts that could be present in treated water. Certain disinfectants can react with naturally occurring minerals and substances in the water to increase health risks. The specific byproducts regulated are: 1) Trihalomethanes, 2) Haloacetic acids, 3) Chlorite, and 4) Bromite, according to the EPA ([11](https://www.epa.gov/dwreginfo/stage-1-and-stage-2-disinfectants-and-disinfection-byproducts-rules)). The specific associated health risks, when testing on lab animals, included bladder cancer and negative reproductive effects. By limiting the amount of disinfectants and disinfectant byproducts, this rule keeps drinking water safe for humans and mitigates these dangerous health  risks.

#### Long Term 2 Enhanced Surface Water Treatment Rule

The Long Term 2 Enhanced Surface Water Treatment Rule (LT2ESWTR) was created to address the health concerns related to pathogenic microorganisms, including Cryptosporidium, in drinking water. The rule was initially created when amendments to the Safe Water Drinking Act (SWDA) of 1996 was passed. This current rule is the second phase of initial rules passed by Congress, with the intent to be more strict on systems that are more at risk to being contaminated by Cryptosporidium.
The LT2ESWTR first requires that filtered water treatment systems be sampled for E. Coli, a less expensive means than to sample Cryptosporidium, and only if systems have a high concentration of E. Coli will they be sampled for Cryptosporidium. After this sampling period, systems are classified into bins, which separate the higher and lower bacteria concentrations. Low bins require no additional water treatment, but high bins must “provide 90 to 99.7 percent additional treatment for Cryptosporidium,”  according to the EPA fact sheet on the rule ([6](https://nepis.epa.gov/Exe/ZyPDF.cgi/P10056JS.PDF?Dockey=P10056JS.PDF)). The sheet further states that “all unfiltered water systems must provide at least 99 or 99.9 percent inactivation of Cryptosporidium.” 

The health risks associated with the bacteria Cryptosporidium can range depending on the severity of the exposure. It causes the disease Cryptosporidiosis, which gives humans and animals infected watery diarrhea. According to the CDC, the illness last for 1 to 2 weeks and is not severe, but for people with weakened immune systems such as people with AIDS or undergoing cancer treatment, the disease can be fatal ([7](https://www.cdc.gov/parasites/crypto/illness.html)). Therefore, keeping it out of drinking water, which is the most common way it spreads, is paramount.




#### Feasibility of AgauClara plants

In regards to the regulations discussed in previous sections, AguaClara treatment systems will meet most of the EPA requirements. Firstly, given that the piping of an AguaClara system is essentially all PVC, there will be no Lead or Copper being leached into the water at the treatment facility, which is required by the Lead and Copper Rule. This does not necessarily mean that the pipes that deliver water to home are safe, given that that infrastructure is already in place, the AguaClara system would provide nothing additional and therefore meet the requirements of that rule. Secondly, the use of chlorine to treat coliform bacteria, as required by the Total Coliform Rule, is met by AguaClara plants. These plants use chlorine in the form of calcium hypochlorite to treat the water for coliform bacteria. 


With respect to the Surface Water Treatment Rule and the rules that followed (the Stage 1 and Stage 2 Disinfectants and Disinfection Byproducts Rules and the Long Term 2 Enhanced Surface Water Treatment Rule), AguaClara are as effective as conventional water treatment systems. The flocculation, sedimentation, and filtration steps in the process are similar to conventional water treatment systems in the overall treatment process. AguaClara additionally uses a floc blanket, which reduces settled water turbidity by using plate settlers to return flocs to the bottom of the sedimentation tank and by using a jet reverser to resuspend the flocs. This allows the floc blanket to form, which removes small particles through further flocculation and reduces the water turbidity after the entire sedimentation process. The filtration systems found at previously built AguaClara plants in Honduras use some form of sand filtration, either with Slow Sand Filtration (SSF), Rapid Sand Filtration (RSF), or Stacked Rapid Sand Filtration (StaRS). These filtration systems in combination with the other steps described previously will treat the water as well as it needs to be, as specified by the Surface Water Treatment rule. The additions and amendments specify more detailed requirements for the systems including bacteria that could be present and disinfectant byproducts of the treatment. The AguaClara System would be very apt to consistently handle the violations of the rules that these Puerto Rican systems have displayed. In terms of benefits of replacing existing systems, AguaClara would provide cleaner and safer drinking water than what is currently existing in many of the systems. 

The main concern with plant functionality is the requirement that turbidity be below 0.3 NTU with no more than one value above 1 NTU. Current AguaClara plants operate slightly above this threshold, however there is a big range in performance of AguaClara plants with EStaRS filters. Some meet the 0.3 standard and others don't. An example of a plant that consistently meets the performance standards is the plant in Moroceli, Honduras ([12](http://aguaclara.github.io/index.html)). This plant could be used as a model for future plants built in Puerto Rico. The other concern with plant functionality is within the filter backwash rule. The EPA requires that “recycled filter backwash water to go through all processes of a system’s conventional or direct filtration treatment” if plants recycle filter backwash water. ([13](https://www.epa.gov/dwreginfo/surface-water-treatment-rules)). Currently, AguaClara systems do not do this due to the energy needs to pump the water back up to the entrance tank, which means there is room for improvement. With old AguaClara plants as a model, new plants could be designed and built with modifications to meet this requirement. 


In addition to regulatory components, many other factors would need to be considered before implementing plants. These may include: influent water source and conditions (including turbidity and quantity), the current system in place, cost to install and maintain, terrain, population to be served and many others. The next section of this analysis defines the framework underwhich costs to implement could be determined.


#### Cost Analysis Framework for New Plants

While a complete comparative cost analysis of between current water systems in Puerto Rico and an AguaClara plant of similar capacity is not possible without extensive site-specific information, we can begin to create a framework for approaching such a cost analysis. It is important to list the questions that need to be asked and the data that needs to be gathered in order to pursue a full cost analysis. AguaClara plants in Honduras are the best source of information for future analyses.

This framework is broken into 4 categories: Site, Physical Plant, Supplies and Chemicals, and Labor.

1. Site
    The process of finding a suitable site for an AguaClara plant is obviously heavily dependent on the water source. The same constraints for source and ample elevation for a passive system apply in Puerto Rico as in Honduras. 

2. Physical Plant
    Construction costs vary with plant size and location. The spreadsheet linked below provides an itemized list of costs to construct a 1 L/s AguaClara plant. While the values listed are of marginal usefulness, the items listed will provide a good starting point to estimate costs in Puerto Rico.
    - [Link to itemized costs]( https://docs.google.com/a/cornell.edu/spreadsheets/d/1rR643mJhG6lsj_oqQ1Y8MTg8wN-PVxMQuQ_r6r98hwY/edit?usp=sharing )

3. Supplies and Chemicals
	Historically, an approximation of \$2 per million liters of treated water has been used an 
approximation for flocculation-sedimentation-filtration systems such as AguaClara’s.

 -Calcium hypochlorite, at approximately \$1 per kilogram, contains 70% chlorine, of which 
2mg/L of equivalent chlorine gas are typically needed. 
4. Labor
	Labor costs will obviously vary between Puerto Rico and Honduras. The tasks and demands of an operator of similar-capacity in Puerto Rico and Honduras will be similar at base level. However, since Puerto Rico is subject to United States regulations extra operational regulations may increase the labor required to run a plant in Puerto Rico. a big aspect that will matter in terms of cost is the difference in minimum wage in the two locations. Minimum wage in Puerto Rico is \$7.25 per hour, whereas in Honduras, the minimum hourly wage for someone working in water ranges from 34.49 lempira (1.46 USD) and 42.99 lempira (1.78 USD). This difference will greatly impact the operation costs of the plant, and makes estimation of plant costs more difficult. One way to balance this greater labor cost is to build plants large enough so that they could be run only 8 hours or 12 hours a day, thus decreasing the amount of time an operator would need to be present. 
    

#### Potential Plants for Further Analysis

Using the types of violations, number of people served, and location/accessibility as criterion for a new plant, a two sets of five plants were formulated. We chose to ignore the plants with the Lead and Copper Rule violations, because this violation could occur at the plant, but it could also occur in the pipes leading to the specific taps tested. We decided to focus on plants with violations that we know an AguaClara plant could address, in particular the Total Coliform Rule, which was present in large number at a many plants throughout Puerto Rico. Our first criterion were plants that had at least more than 25 violations in the past 5 years. Our second criterion was the urban versus rural classification; according to a United States Census Document, a rural area is anywhere that is not classified as urban and has a population density less than 1,000 people per square mile ([14](https://www2.census.gov/geo/pdfs/reference/GARM/Ch12GARM.pdf)). The idea is to serve the most people possible, and using these criteria, a list of the best five treatment plants that could be replaced by an AguaClara plant was formulated. This list is shown below:


1. Periche
    - Population served: 1100
    - Violations in past 5 years: 35
    - Location: San German (population density, 652.55)
2. Corea Metralla
    - Population served: 1000
    - violation in past 5 years: 50
    - Location: Penuelas (population density, 544.32)
3. La Sapia
    - Population served: 510
    - violation in past 5 years: 55
    - Location: Orocovis (population density, 367.53)
4. Com Eladio Andreu
    - Population served: 500
    - violation in past 5 years: 46
    - Location: Corozal (population density, 872.35)
5. Santa Barbara
    - Population served: 500
    - violation in past 5 years: 55
    - Location: Jayuya (population density, 373.54)

The second list is composed of plants which violated aspects of the Surface water treatment rule. These plants would be a good candidate for an AguaClara plant because some set of their processes is not working right and so an entirely new plant could be in order. For the plants violating the Total Coliform Rule, appropriate chlorine application might solve the problem depending on what exact violation occurred. For plants violating the Surface Water Rule many different violations are possible including elevated turbidity, inproper filtration methods, or an inadequate reduction of Cryptosporidium, Giardia, or viruses. 

1. Yahuecas
    - Population served: 2840
    - Violations in past 5 years: 4
    - Location: Adjuntas (population density, 625.11)
2. Guilarte
    - Population served: 2090
    - violation in past 5 years: 1
    - Location: Adjuntas (population density, 625.11)
3. Guayabota
    - Population served: 1852
    - violation in past 5 years: 14
    - Location: Yabucoa (population density, 687.50)
4. Ranchera
    - Population served: 1560
    - violation in past 5 years: 4
    - Location: Yauco (population density, 611.59)
5. Jagua Pasto
    - Population served: 1270
    - violation in past 5 years: 3
    - Location: Guayanilla (population density, 509.60)


```python
from aide_design.play import*
from aide_design import floc_model as floc
from pytexit import py2tex
DataFrame = pd.read_csv('reports_dataframe.csv')
pd.get_option("display.max_rows", 127)
#Below are the items that were imported by the code above so that you know what abbreviations to use in your code. 

# Third-party imports
#import numpy as np
#import pandas as pd
#import matplotlib.pyplot as plt
#import matplotlib

# AIDE imports
#import aide_design
#import aide_design.pipedatabase as pipe
#from aide_design.units import unit_registry as u
#from aide_design import physchem as pc
#import aide_design.expert_inputs as exp
#import aide_design.materials_database as mat
#import aide_design.utility as ut
#import aide_design.k_value_of_reductions_utility as k
#import aide_design.pipeline_utility as pipeline
import warnings
```


```python
DataFrame

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
      <th>Water System Name</th>
      <th>Population Served</th>
      <th>Pb + Cu Rule</th>
      <th>Radionucleotides</th>
      <th>Long Term 2</th>
      <th>Surface Water Rule</th>
      <th>Stage 1+2</th>
      <th>Total Coliform</th>
      <th>Volatile Organic Chemical</th>
      <th>Synthetic Organics</th>
      <th>Nitrates</th>
      <th>Source Type</th>
      <th>System Address</th>
      <th>Contact Phone</th>
      <th>Cities Served</th>
      <th>Counties Served</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>YAHUECAS</td>
      <td>2,840</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>4 (known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>PO BOX 7080\nBO. OBRERO STATION\nSANTURCE, PR ...</td>
      <td>787-758-5454</td>
      <td>ADJUNTAS</td>
      <td>Adjuntas Municipio</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GARZAS</td>
      <td>2,782</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 10 KM. 29.3\nADJUNTAS, PR 00601</td>
      <td>787-620-2277</td>
      <td>ADJUNTAS</td>
      <td>Adjuntas Municipio</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SABANA GRANDE</td>
      <td>2,707</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 611 KM. 7.1\nUTUADO, PR 00641</td>
      <td>787-620-2277</td>
      <td>UTAUDO, UTUADO</td>
      <td>Utuado Municipio</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SANAMUERTO</td>
      <td>2,391</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 567 KM. 1.2 INT.\nMOROVIS, PR 00720</td>
      <td>787-620-2277</td>
      <td>MOROVIS, OROCOVIS</td>
      <td>Morovis Municipio, Orocovis Municipio</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MATRULLA</td>
      <td>2,350</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 143 KM.33.8\nOROCOVIS, PR 00916</td>
      <td>787-620-2277</td>
      <td>OROCOVIS</td>
      <td>Orocovis Municipio</td>
    </tr>
    <tr>
      <th>5</th>
      <td>INDIERA ALTA</td>
      <td>2,273</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>\nROAD 428 KM 1\nMARICAO, PR 00706</td>
      <td>NaN</td>
      <td>MARICAO</td>
      <td>Maricao Municipio</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ACUED. BO. GUAYABOTA</td>
      <td>2,268</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 182 KM. 12.3\nBO. GUAYABOTA\nYABUCOA, PR...</td>
      <td>787-893-2688</td>
      <td>YABUCOA</td>
      <td>Yabucoa Municipio</td>
    </tr>
    <tr>
      <th>7</th>
      <td>MAMEYES ARRIBA</td>
      <td>2,152</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 530 KM. 1.2 INT.\nJAYUYA, PR 00664</td>
      <td>787-620-2277</td>
      <td>JAYUYA, MAMEYES ARRIBA</td>
      <td>Jayuya Municipio</td>
    </tr>
    <tr>
      <th>8</th>
      <td>GUILARTE</td>
      <td>2,090</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 131 KM.2.5\nADJUNTAS, PR 00601</td>
      <td>787-620-2277</td>
      <td>ADJUNTAS</td>
      <td>Adjuntas Municipio</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ESPINO</td>
      <td>2,072</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 124 KM. 17.7 INT.\nLAS MARIAS, PR 00670</td>
      <td>787-620-2277</td>
      <td>ESPINO, SAN LORENZO</td>
      <td>San Lorenzo Municipio</td>
    </tr>
    <tr>
      <th>10</th>
      <td>LAS DELICIAS</td>
      <td>1,916</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 149 KM. 30.0 INT.\nCIALES, PR 00638</td>
      <td>787-620-2277</td>
      <td>CIALES</td>
      <td>Ciales Municipio</td>
    </tr>
    <tr>
      <th>11</th>
      <td>ACUED. COM. BO. QUEBRADILLAS</td>
      <td>1,862</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 152 KM. 7.8 INT.\nSECTOR FARALLON\nBARRA...</td>
      <td>787-857-2501</td>
      <td>BARRANQUITAS</td>
      <td>Barranquitas Municipio</td>
    </tr>
    <tr>
      <th>12</th>
      <td>GUAYABOTA</td>
      <td>1,852</td>
      <td>1.0</td>
      <td>0</td>
      <td>14 (known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 3 R-90 KM. 9.9\nYABUCOA, PR 00767</td>
      <td>787-620-2277</td>
      <td>GUAYABOTA, YABUCOA</td>
      <td>Yabucoa Municipio</td>
    </tr>
    <tr>
      <th>13</th>
      <td>CIMARRONA</td>
      <td>1,817</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 713 KM. 0.1\nGUAYAMA, PR 00784</td>
      <td>787-620-2277</td>
      <td>BARCELONETA</td>
      <td>Barceloneta Municipio</td>
    </tr>
    <tr>
      <th>14</th>
      <td>RIO ARRIBA</td>
      <td>1,777</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 10 KM. 65.4 INT.\nARECIBO, PR 00612</td>
      <td>787-620-2277</td>
      <td>ARECIBO</td>
      <td>Arecibo Municipio</td>
    </tr>
    <tr>
      <th>15</th>
      <td>COM. ANONES MAYA</td>
      <td>1,750</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>49(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 878 KM.3.7\nBO ANONES\nNARANJITO, PR 00719</td>
      <td>787-869-6392</td>
      <td>NARANJITO</td>
      <td>Naranjito Municipio</td>
    </tr>
    <tr>
      <th>16</th>
      <td>CULEBRAS</td>
      <td>1,702</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 738 END\nCAYEY, PR 00660</td>
      <td>787-620-2277</td>
      <td>CAYEY, CULEBRAS</td>
      <td>Cayey Municipio</td>
    </tr>
    <tr>
      <th>17</th>
      <td>GUARAGUAO</td>
      <td>1,680</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>2(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 10 KM.16.8\nPONCE, PR 00731</td>
      <td>787-620-2277</td>
      <td>PONCE</td>
      <td>Ponce Municipio</td>
    </tr>
    <tr>
      <th>18</th>
      <td>RANCHERA</td>
      <td>1,560</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>4(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR.128 R 371 KM.10.6\nYAUCO, PR 00698</td>
      <td>787-620-2277</td>
      <td>RANCHERAS, YAUCO</td>
      <td>Ponce Municipio, Yauco Municipio</td>
    </tr>
    <tr>
      <th>19</th>
      <td>COM. RANCHO GRANDE</td>
      <td>1,555</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 969 BO. MAIZALES\nNAGUABO, PR 00718</td>
      <td>787-874-3040</td>
      <td>NAGUABO</td>
      <td>Naguabo Municipio</td>
    </tr>
    <tr>
      <th>20</th>
      <td>ZAMAS</td>
      <td>1,400</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>43(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 528 KM. 3.5\nJAYUYA, PR 00664</td>
      <td>787-828-0078</td>
      <td>JAYUYA</td>
      <td>Jayuya Municipio</td>
    </tr>
    <tr>
      <th>21</th>
      <td>JAGUA PASTO</td>
      <td>1,270</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>3(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 378 KM.10\nGUAYANILLA, PR 00656</td>
      <td>787-620-2277</td>
      <td>GUAYANILLA, JAGUA PASTO</td>
      <td>Guayanilla Municipio</td>
    </tr>
    <tr>
      <th>22</th>
      <td>MAMEYES ABAJO</td>
      <td>1,150</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 140 KM. 19.2 INT.\nUTUADO, PR 00641</td>
      <td>787-620-2277</td>
      <td>MAMEYES ABAJO, UTUADO</td>
      <td>Utuado Municipio</td>
    </tr>
    <tr>
      <th>23</th>
      <td>CANALIZO</td>
      <td>1,147</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 140 KM. 4.0\nJAYUYA, PR 00664</td>
      <td>787-620-2277</td>
      <td>JAYUYA</td>
      <td>Jayuya Municipio</td>
    </tr>
    <tr>
      <th>24</th>
      <td>PERICHE</td>
      <td>1,100</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>35(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 361 KM. 6.2 INT.\nBO CAIN ALTO\nSAN GERM...</td>
      <td>787-892-5664</td>
      <td>SAN GERMAN</td>
      <td>San German Municipio</td>
    </tr>
    <tr>
      <th>25</th>
      <td>JAGUA CEIBA</td>
      <td>1,085</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>1(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 132 R386 KM. 5\nPENUELAS, PR 00624</td>
      <td>787-620-2277</td>
      <td>PENUELAS</td>
      <td>Penuelas Municipio</td>
    </tr>
    <tr>
      <th>26</th>
      <td>MALPASO</td>
      <td>1,029</td>
      <td>2.0</td>
      <td>0</td>
      <td>0</td>
      <td>1(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 131 KM.4\nPENUELAS, PR 00724</td>
      <td>787-620-2277</td>
      <td>PENUELAS</td>
      <td>Penuelas Municipio</td>
    </tr>
    <tr>
      <th>27</th>
      <td>COPAR</td>
      <td>1,000</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CAR 568 KM. 28.5\nSECTOR LA HERRADURA BO.PADIL...</td>
      <td>787-859-3362</td>
      <td>COROZAL</td>
      <td>Corozal Municipio</td>
    </tr>
    <tr>
      <th>28</th>
      <td>COREA METRALLA</td>
      <td>1,000</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>50(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 387 KM. 4.2\nSEC. CORREA BO.QUEBRADA CEI...</td>
      <td>787-836-5669</td>
      <td>PENUELAS</td>
      <td>Penuelas Municipio</td>
    </tr>
    <tr>
      <th>29</th>
      <td>MONTE DEL ESTADO</td>
      <td>973</td>
      <td>1.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 366 KM 1.0 INT.\nMARICAO, PR 00606</td>
      <td>787-620-2277</td>
      <td>MARICAO, TABONUCO</td>
      <td>Maricao Municipio</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>97</th>
      <td>ACUED. DE LA COMUNIDAD</td>
      <td>100</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>SEC.MAGUELLES FCA.RAFAEL RUIZ\nCARR. 128 RAMAL...</td>
      <td>787-897-3427</td>
      <td>LARES</td>
      <td>Lares Municipio</td>
    </tr>
    <tr>
      <th>98</th>
      <td>COMUNIDAD EL FRIO</td>
      <td>100</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>53(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 143 KM. 30.5\nSECTOR EL FRIO\nOROCOVIS, ...</td>
      <td>787-867-6753</td>
      <td>OROCOVIS</td>
      <td>Orocovis Municipio</td>
    </tr>
    <tr>
      <th>99</th>
      <td>SISTEMA DE AGUA MATUYAS BAJO</td>
      <td>88</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>53(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR 759 KM 6.2 INTERIOR\nBO. MATUYAS BAJO\nMA...</td>
      <td>787-204-1595</td>
      <td>NaN</td>
      <td>Maunabo Municipio</td>
    </tr>
    <tr>
      <th>100</th>
      <td>FINCA LOS GARCIA</td>
      <td>84</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>53(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>SEC. HOYO BO. PALMASOLA\nCARR. 957 KM. 3.4\nCA...</td>
      <td>787-886-2243</td>
      <td>CANOVANAS</td>
      <td>Canovanas Municipio</td>
    </tr>
    <tr>
      <th>101</th>
      <td>ACUEDUCTO FAMILIA TORRES</td>
      <td>80</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>HC-7 BOX 24094\nPONCE, PR 00731</td>
      <td>787-259-0437</td>
      <td>PONCE</td>
      <td>Ponce Municipio</td>
    </tr>
    <tr>
      <th>102</th>
      <td>EL YUMURI</td>
      <td>80</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>51(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 139 KM. 17.2\nPONCE, PR 00731</td>
      <td>787-844-7767</td>
      <td>PONCE</td>
      <td>Ponce Municipio</td>
    </tr>
    <tr>
      <th>103</th>
      <td>LOS VAZQUEZ</td>
      <td>80</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 944 KM. 2.8 INT.\nSEC.LOS VAZQUEZ BO. HA...</td>
      <td>787-737-7873</td>
      <td>GURABO</td>
      <td>Gurabo Municipio</td>
    </tr>
    <tr>
      <th>104</th>
      <td>ACEITUNA I</td>
      <td>69</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR.561 PRIMER RAMAL\nSECTOR ACEITUNA SIERRIT...</td>
      <td>787-847-1351</td>
      <td>VILLALBA</td>
      <td>Villalba Municipio</td>
    </tr>
    <tr>
      <th>105</th>
      <td>SIST. RURAL GRAULAO</td>
      <td>64</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 10 KM. 56.7\nBO. SALTO ABAJO\nUTUADO, PR...</td>
      <td>787-894-9036</td>
      <td>UTUADO</td>
      <td>Utuado Municipio</td>
    </tr>
    <tr>
      <th>106</th>
      <td>ACUED. DELGADO VEGA Y OTROS</td>
      <td>60</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>45(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. #1 KM 30 INTERSECCION 795\nCOMUNIDAD LA ...</td>
      <td>787-747-1848</td>
      <td>CAGUAS</td>
      <td>Caguas Municipio</td>
    </tr>
    <tr>
      <th>107</th>
      <td>ACUED. LA GRAMA</td>
      <td>60</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>FINCA HIPOLITO MONTERO\nCARR. 613 KM. 7.1 BO.T...</td>
      <td>787-894-4122</td>
      <td>UTUADO</td>
      <td>Utuado Municipio</td>
    </tr>
    <tr>
      <th>108</th>
      <td>COMUNIDAD MENDEZ</td>
      <td>60</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>54(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR.119 KM.7.6 SEC.MENDEZ\nBO.ROSARIO ALTO\nS...</td>
      <td>787-892-8023</td>
      <td>SAN GERMAN</td>
      <td>San German Municipio</td>
    </tr>
    <tr>
      <th>109</th>
      <td>TALANTE</td>
      <td>60</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>54(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>APARTADO 261\nMAUNABO, PR 00707</td>
      <td>787-861-8345</td>
      <td>MAUNABO</td>
      <td>Maunabo Municipio</td>
    </tr>
    <tr>
      <th>110</th>
      <td>CERROTE</td>
      <td>58</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>37(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 374 KM. 5.3 INT.\nBO. RIO PRIETO SEC. CE...</td>
      <td>787-267-5711</td>
      <td>YAUCO</td>
      <td>Yauco Municipio</td>
    </tr>
    <tr>
      <th>111</th>
      <td>COMITE RESIDENTE SECTOR BELLEZA</td>
      <td>58</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 3391 KM. 1.4\nSECTOR BELLAZA BO. RUCIO\n...</td>
      <td>NaN</td>
      <td>PENUELAS</td>
      <td>Penuelas Municipio</td>
    </tr>
    <tr>
      <th>112</th>
      <td>VIVI ABAJO</td>
      <td>57</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR.111 KM.2.1 INT\nBO.VIVI ABAJO FCA. ANGEL ...</td>
      <td>787-894-0319</td>
      <td>UTUADO</td>
      <td>Utuado Municipio</td>
    </tr>
    <tr>
      <th>113</th>
      <td>ACUEDUCTO COMUNIDAD SAN JOSE</td>
      <td>56</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>HC-72 BOX 4185\nNARANJITO, PR 00719</td>
      <td>787-869-7794</td>
      <td>NARANJITO</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>114</th>
      <td>ACUED. LAS DELICIAS</td>
      <td>48</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>BO.CIALITOS FCA.RADAMES CINTRO\nSEC.LAS DELICI...</td>
      <td>787-828-4248</td>
      <td>CIALES</td>
      <td>Ciales Municipio</td>
    </tr>
    <tr>
      <th>115</th>
      <td>ACUED. HACIENDA PLANELL</td>
      <td>40</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>54(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 124 RAMAL 4431 KM. 1.0\nBO.PEZUELA FCA.E...</td>
      <td>787-   -</td>
      <td>LARES</td>
      <td>Lares Municipio</td>
    </tr>
    <tr>
      <th>116</th>
      <td>LA CARMELITA</td>
      <td>38</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>54(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 139 KM. 20.7\nSECT. LA CARMELITA\nPONCE,...</td>
      <td>787-284-1056</td>
      <td>PONCE</td>
      <td>Ponce Municipio</td>
    </tr>
    <tr>
      <th>117</th>
      <td>ACEITUNA III</td>
      <td>36</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 561 PRIMER RAMAL FINAL\nSECTOR ACEITUNA\...</td>
      <td>787-847-7687</td>
      <td>VILLALBA</td>
      <td>Villalba Municipio</td>
    </tr>
    <tr>
      <th>118</th>
      <td>TANAMA COMUNAL</td>
      <td>35</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR.526 KM.6.4\nBO.TANAMA\nADJUNTAS, PR 00601</td>
      <td>787-829-0639</td>
      <td>ADJUNTAS</td>
      <td>Adjuntas Municipio</td>
    </tr>
    <tr>
      <th>119</th>
      <td>SECTOR LAJITAS</td>
      <td>33</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>55(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>BO. BORINQUEN\nCARR. 765 KM. 3.4 INT.\nCAGUAS,...</td>
      <td>787-703-1068</td>
      <td>CAGUAS</td>
      <td>Caguas Municipio</td>
    </tr>
    <tr>
      <th>120</th>
      <td>CRUCERO</td>
      <td>29</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>54(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 131 KM 5.0\nBO. GUILARTA, SECTOR CRUCERO...</td>
      <td>787-829-5618</td>
      <td>ADJUNTAS</td>
      <td>Adjuntas Municipio</td>
    </tr>
    <tr>
      <th>121</th>
      <td>ACUEDUCTO COMUNIDAD EDEM</td>
      <td>25</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>28(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 7740 KM 3.9 INT.\nBO. ESPINO SECT. QUEBR...</td>
      <td>787-736-6169</td>
      <td>SAN LORENZO</td>
      <td>San Lorenzo Municipio</td>
    </tr>
    <tr>
      <th>122</th>
      <td>JEA QUALITY</td>
      <td>25</td>
      <td>nan</td>
      <td>4(known)</td>
      <td>0</td>
      <td>0</td>
      <td>2(known)</td>
      <td>2(known)</td>
      <td>21(known)</td>
      <td>70(known)</td>
      <td>3(known)</td>
      <td>Surface water</td>
      <td>CARR. 802 KM. 3.4 INT.\nBO. MANA SECTOR QDA FR...</td>
      <td>787-420-8483</td>
      <td>COROZAL</td>
      <td>Corozal Municipio</td>
    </tr>
    <tr>
      <th>123</th>
      <td>LA MONTANA</td>
      <td>25</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>54(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>BO. RIO PRIETO SEC. LA MONTANA\nCARR. 374 KM. ...</td>
      <td>787-829-3614</td>
      <td>YAUCO</td>
      <td>Yauco Municipio</td>
    </tr>
    <tr>
      <th>124</th>
      <td>PLT.  MUNICIPAL CAROLINA</td>
      <td>25</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>APARTADO # 8\nCAROLINA, PR 00986-0008</td>
      <td>787-257-2454</td>
      <td>CAROLINA</td>
      <td>Carolina Municipio</td>
    </tr>
    <tr>
      <th>125</th>
      <td>FARALLON</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>12(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR.742 INT. BO.FARALLON\nSECTOR CAMACHO\nCAY...</td>
      <td>787-738-6141</td>
      <td>CAYEY</td>
      <td>Cayey Municipio</td>
    </tr>
    <tr>
      <th>126</th>
      <td>LUQUILLO URBANO</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>21(known)</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Surface water</td>
      <td>CARR. 983 KM 6.2\nSABANA WARD\nLUQUILLO, PR 00773</td>
      <td>787-620-2277</td>
      <td>LUQUILLO</td>
      <td>Luquillo Municipio</td>
    </tr>
  </tbody>
</table>
<p>127 rows × 16 columns</p>
</div>



## References:



1. EPA Consumer Confidence Reports, USEPA, [online]( https://ofmpub.epa.gov/apex/safewater/f?p=ccr_wyl:102 )
2. [Revised Total Coliform Rule And Total Coliform Rule, EPA 40 CFR 141.21 Subpart Cand 79 FR 10665](https://www.epa.gov/dwreginfo/revised-total-coliform-rule-and-total-coliform-rule)
3. [EPA Water Systems Violation Report](https://ofmpub.epa.gov/apex/sfdw/f?p=108:11:::NO:11,RIR:IREQ_PWSID:PR0004584)
4. [Lead and Copper Rule, USEPA, EPA 40 141 Subpart Q](https://www.epa.gov/sites/production/files/2015-11/documents/howepargulates_cfr-2003-title40-vol20-part141_0.pdf)
5. Lead and Copper Fact Sheet, Minnesota Dept. of Health, http://www.health.state.mn.us/divs/eh/water/factsheet/com/leadcopper.pdf
6. LT2ESWR Fact Sheet https://nepis.epa.gov/Exe/ZyPDF.cgi/P10056JS.PDF?Dockey=P10056JS.PDF
7. CDC Parasites-Cryptosporium-Illness and Symptoms https://www.cdc.gov/parasites/crypto/illness.html
8. Threats on Tap- Drinking water in Puerto Rico https://www.nrdc.org/sites/default/files/threats-on-tap-drinking-water-puerto-rico-ip.pdf
9. Surface Water Rule Fact Sheet, EPA, (https://www.epa.gov/sites/production/files/documents/SWTR_Fact_Sheet.pdf)
10. Giardia, General Reference, USCDC, https://www.cdc.gov/parasites/giardia/general-info.html
11. Stage 1 and 2 Disinfectant Rule, USEPA, https://www.epa.gov/dwreginfo/stage-1-and-stage-2-disinfectants-and-disinfection-byproducts-rules
12. [POST App](http://aguaclara.github.io/index.html), AguaClara, 2017
13. Surface wwater treatment rules, USEPA, https://www.epa.gov/dwreginfo/surface-water-treatment-rules
14. Census Data, Population Density, US Census, https://www2.census.gov/geo/pdfs/reference/GARM/Ch12GARM.pdf
