#The Flocculatorita

####By The Water Tzars: Nina Blahut, Lily Falk, Marcin Sawczuk, Yitzy Bitzyspider

<p align="center"> <img
src="https://github.com/yyr2/pics4520/blob/master/Floculatorita%20Mascot.png?raw=true" width= "350"> </p>
<p align="center">

*Figure :). Floco, the flocculatorita mascot.*

## Introduction and Background

The prefabricated plants (PF300) are a subset of AguaClara plants designed for small communities who may not have the resources to finance, or the population to require a built-in-place plant. There are currently 3 in Manzaragua, 1 in Cuatro Comunidades, 1 near Copan (Honduras) in use, and one at Cornell's Water Filtration Plant in the testing phase. Built-in-place AguaClara plants are housed in buildings with separate areas for flocculation, sedimentation and filtration. In contrast, the PF300 occupy considerably less space, as the plant is only two and a half meters tall.

PF300 plants have made it possible for small communities to receive clean water, and have served as an addition to increase the capacity of built-in-place AguaClara plants, as they were added in parallel with the main treatment process chain.

The low population density and small community size in areas that use PF300 plants has led to difficulty with employing plant operators. The PF300 plants provide water to fewer people, however require the same degree of monitoring as a full scale plant. As a result, delegating a plant operator has created a larger burden on these communities. An ideal system for an individual to check on the plant for coagulant dosing and general running issues has not yet been well established.

The PF300 flocculator is in need of improvement to increase flexibility of the design. Currently the flocculators are made out of 3" PVC pipe. High cost of the PVC fittings make it expensive to build flocculators according to this design for higher flow rates or residence times. This is because the change would require switching to bigger pipe diameters. Representatives from AguaClara’s partner organization in Honduras, Agua Para El Pueblo (APP), have expressed interest in a larger flocculator. A longer residence time would provide operators with more time to respond to high turbidity events to prevent the dirty water from reaching the sed-tank and disturbing the floc blanket which causes long term decrease of the effluent water quality. Moving forward, there is desire for the portable plants to come in multiple sizes. Hopefully, this would lead to a more cost efficient design of the prefabricated plants in various sizes.

The Water Tzars have worked to design a new flocculator which will be more flexible and scalable than the current system. The group has envisioned flocculation within a large diameter pipe divided into channel with baffles and expansions enabling complex flow within the pipe that would lead to successful floc formation. Moving forward the group will consider alternative materials for the sheets that will work as baffles.

<p align="center"> <img
src="https://github.com/yyr2/pics4520/blob/master/Flocculatorita%20Design.gif?raw=true" width= "350"> </p>
<p align="center">

*Figure 1. Sample Flocculatorita design.*

## Design Process

The design process for the small hydraulic flocculator is based on the AguaClara top down design approach (presentation 2, slide 20), but made slight alterations to make it possible for our flocculator to fit into a large PVC pipe or HDPE tank. We then modified the AguaClara Flocculator source code to come up with a class that designs a small flocculator that can be housed inside of a large PVC pipe, which we have named a "flocculatorita". The collision potential ($G_{CS} \theta$) for our design is constrained to 37,000, which is based on the collision potential that is currently used in AguaClara plants (2). Our design is also constrained to a total headloss of 40 cm. This constraint is also based on the head loss which is currently used in AguaClara flocculators (3). Next, the height of the flocculator is constrained to 2 meters. This is to ensure that the flocculatorita is not taller than a sedimentation tank. This logic is also borrowed from AguaClara source code (3). Lastly, our design is constrained by the available diameters of large PVC pipes that can be used as a tank for our flocculatorita.

The first step in AguaClara's top down design approach for the flocculator is to calculate the required flocculator volume. We used the same process as defined in the AguaClara Flocculator source code to determine the required active volume in our flocculator (3). To do so, the AguaClara flocculator class first calculates the Camp Stein velocity gradient (average velocity gradient) using the following equation:

$G_{CS} = {\frac{gh_{\rm{L}}}{\nu G\theta}}$

This calculation is done below in the property "vel_grad_avg." Then, the average velocity gradient is used to calculate required residence time in the flocculator by dividng [spelling] target collision potential by the calculated average velocity gradient:

 $\theta = {\frac{ G\theta}{G_{CS}}}$


  This calculation is carried out in the property "retention_time." Finally, the calculated retention time and user-defined flow rate is used to determine the required flocculator volume (calculation is performed in the class "vol"):

$\rlap{-} V_{floc} = {\theta}{Q}$


After calculating the necessary active volume in our flocculatorita, we determined the necessary active cross sectional area by dividing the volume by the height of the flocculator:

$A=  \rlap{-} V_{floc}/ H_{floc}$

We made some simplifying assumptions to decide which size PVC pipe was appropriate to use as a tank for the flocculatorita. We assumed that the active space inside of our tank would be the largest square that could be housed in a cross section of the PVC pipe tank, to avoid the complication of different sized/shaped flow channels. This simplifying assumption results in excess dead volume, but we hope in the future to come up with an algorithm to optimize the cross sectional area of the pipe to minimize that dead volume. Using our simplifying assumption, we found the side length of the largest square, and used Pythagorean's Theorem to find the length of the diagonal of the square. This length is the necessary diameter of the PVC pipe tank:

$D_{tank}=\sqrt{2*A}$

<p align="center"> <img
src="https://github.com/lilyfalk/CEE4520/blob/master/IMG_4222.JPG?raw=true" width= "250"> </p>
<p align="center">

*Figure 2. Top view showing the original design idea. This design was based on a square active area housed within the circular PVC pipe.*

These calculations are carried out in the property "min_diameter_tank." Then, the code selects the PVC pipe diameter that is closest to and larger than the calculated minimum from an input array of available PVC pipe diameters in the property "design diameter tank."

After selecting a PVC pipe to use as a tank, we solved for the side length of the square that would fit inside of the chosen pipe using the Pythagorean Theorem:

$L=\sqrt{\frac{1}{2}D_{tank}^2}$

This calculation is performed in the property "channel_L" because the length of one side of our square is analogous to the channel length in a regular AguaClara flocculator.

<p align="center"> <img
src="https://github.com/lilyfalk/CEE4520/blob/master/IMG_4224.JPG?raw=true" width= "250"> </p>
<p align="center">

*Figure 3. Top view showing example channels
 (three chosen for picture arbitrarily).*


The next step was to determine baffle spacing and channel width. Since there was not a clear constraint on either, we decided that we would allow the user to input the number of channels, and use that to determine channel width:

 $W_{channel}=L_{channel}/n_{channel}$

 A benefit to this method is that it creates channels with equal widths and maximizes the space used within the square cross section of active space. This calculation is included in the property "channel_W."

 <p align="center"> <img
 src="https://github.com/lilyfalk/CEE4520/blob/master/IMG_4226.png?raw=true" width= "250"> </p>
 <p align="center">

 *Figure 4. Top view with channels and baffles (number of each chosen arbitrarily for drawing).*


Next, we used the AguaClara source code to determine the maximum distance between expansions for the largest allowable H/S ratio (3). The equation used in that calculation is:

$H_{e_{Max}} = \left[ \frac{K}{2 \nu G_{CS}^2} \left( \frac{Q \Pi_{{HS}_{Max}}}{W_{channel}} \right)^3 \right]^\frac{1}{4}$

Next, we determined the number of flow expansions per baffle space with the calculation (2):

$n_{expansions} = {\rm ceil}\left( \frac{H}{H_{e_{Max}}} \right)$

This calculation used included in the property "expansion_n".

Our next step was to determine the baffle spacing. We did so using the AguaClara source code. The property is named "baffle_S" and it calculates baffle spacing using the equation:

$S = \left( \frac{K}{2 H_e G_{CS}^2 \nu } \right)^\frac{1}{3} \frac{Q}{W_{channel}}$

The next property in the Floccuratorita class determines the number of obstacles per baffle. This is done using the AguaClara source code, and it is simply one less than the number of expansions per baffle space, since one expansion is taken care of with the 180 degree bend (3).

The next property, "obstacle_size" determines the size of the obstacles, so that the energy dissipation rate for flow expansions caused by the obstacles and the 180 degree bends are equal. The Vena Contracta for a 180 degree bend is approximately 0.384 (presentation 1, slide 7), so we solved for the obstacle length, given the baffle spacing that would result in the same Vena Contracta:

 $L_{obstacle}=S_{baffle}(1-\Pi_{VC})$

 We plan to fabricate these obstacles using half pipes.

Then, the property "baffle_n" calculates the number of baffles:

 $n_{baffle}=\frac{L_{channel}n_{channels}}{S_{baffle}}$

 For the cost comparison, we are including the following factors:
 1. Cost of the main tank
 2. Cost of the sheets dividing the tank into channels
 3. Cost of the baffles
 4. Cost of the half-pipes used as obstacles for the flow

We also included a property called "pi_sedtank_floc," which calculates the ratio of the sed tank diameter to the flocculatorita diameter if the sed tank's up flow velocity is 1 mm/s and height is 2 m. According to the conservation of mass, the flow exiting the flocculator must equal the flow going through the sed tank, which is equal to the cross sectional area of the sed tank times its upflow velocity. Therefore,

$A_{sedtank}=Q/V_{up}$

"Pi_sedtank_floc" uses that relationship to find the cross sectional area of the sed tank and then uses that to find the diameter of the sed tank. Finally, it divides the diameter of the flocculatorita by the diameter of the sed tank and returns that ratio. This function does not account for the fact that diameters are only available in discrete sizes.

## Cost Comparison
First, we decided to model a floculatorita that has a residence time of 1 minute and flow rate of 1 liter/second in order to make a reasonable cost comparison between our design for the flocculatorita and the current flocculator used for the PF300 plant. We did so by making a child class of the "flocculatorita" class with those adjustments. This child class is named "Floc_1_min_res" and is shown in the block of code below. Next, we used that class to get an estimate of the cost of the floculatorita, which would handle similar flow and have the same collision potential as the current PF300 flocculator.

### Cost Comparison Analysis

Based on our cost comparison, the flocculatorita is 1.606 dimensionless times the cost of the current flocculator. That being said, this estimate is an overestimate due to the fact that it utilizes US prices more than Honduran prices. Even with the additional price, the new design presents improvement over the old as it is more adaptable, and has potential moving forward.

# Future Work

### Adding the auxiliary equipment
Current design of the flocculator does not include the auxiliary components or manufacturing procedures. To make the design suitable for commercial deployment, it should include the following aspects:

  1. Method for fixing the PVC sheets to the wall of the tank. We propose using long pieces of PVC glued to the inside of the tank wall, which will create a slot for sliding in the PVC sheet. The slot could be then filled with the silicone gasket maker, in order to seal the connection.

  2. Tank bottom design, preferably allowing for disassembly for servicing. Tank should have a flat bottom, which will be supported by the concrete floor. Although it requires placing the flocculator inside the structures with a solid floor, the advantage of having a support structure beneath the tank and therefore not having to worry about supporting the water mass by the tank bottom exceeds potential complications. Flat bottom of the tank can be attached to the corrugated pipe using clamps or bolts holding onto the pipe corrugations. Bottom should be fitting with the slots similar to the ones on the walls, in order to ensure sealed connection with the PVC sheets. Silicone gasket maker can be also used for sealing the connection between the pipe and the bottom.

  3. Attaching an entrance tank/rapid mix unit and a chemical dosing system. In the current PF 300 design, rapid mix and the dosing system are separate units. However, in order to fully take advantage of the compact design proposed in this project, it might be beneficial to incorporate both of them in the flocculator structure. This way, the plant layout will become simpler and more robust, as the components will be protected from impact by the outer structure of the corrugated pipe. Moreover, the pipe itself will provide sufficient structural support for mounting the entrance tank a the chemical dosing system, without the need for additional structure.

  4. Connection to the sedimentation tank, with a valve providing option for separating the two units and additional drain lines at both sides of the valve, in case of need for draining either the flocculator or the sed-tank. Connection should be made through the hole at the bottom of the flocculator tank.

  5. In order for 4. to work, water has to flow in an order which would allow for draining the flocculator after removing the baffles, i.e. connections between the channels separated by the PVC sheets has to be made at the bottom of each sheet (similar to the concrete AC flocculators)

  6. Drain line for wasting the water from the flocculator can be simply added by making a hole at the top of the last channel, above the water level in the first channel. Closing the connection between the flocculator and the sed tank will result with raising the water level until it reaches the drain line, from which it will be wasted.

  7. Baffles can be made in a similar way to the ones currently used, as packets of the polycarbonate sheets with the half-pipe flow constrictions, which can slide into the channels.



### Maximizing surface area

With our current design we only utilize roughly 64% of the available surface area in the tank. This obviously  is very inefficient from a design and cost perspective. As the current cost comparison demonstrates approximately a .6 increase using the flocculatorita design, if space could be maximized by extending the channels, at a minimum utilized surface area would increase to 84% and cost would decrease by .6, making the flocculatorita a comparable if not preferable design.

 $\%_{utilization}=\frac{A_{tank}-A_{flocculator}}{A_{tank}}*100\%$


<p align="center"> <img
src="https://github.com/yyr2/pics4520/blob/master/Wasted_Volume.jpg?raw=true" width= "350"> </p>
<p align="center">

*Figure 5. Comparison of the current design and future work's wasted volume in tank.*

 For future work, the challenge would be to update the code in such a way that it maximizes the effective area used for flocculation. This will have to take into account, among others, the following considerations:



  1. The *geometry* required to get the target velocity profiles necessary for flocculation to occur. Assuming extension of the channels to the edge of the tank, consideration must be taken regarding the differences due to the curvature of the tank and how these differences effect the flow and subsequently the relating velocity profile. It is recommended that one err on the side lower velocity profiles in the uncertain regions to ensure that at the very worst, already created flocs don't break apart.

<p align="center"> <img
src="https://github.com/yyr2/pics4520/blob/master/SA_Comparison.jpg?raw=true" width= "350"> </p>
<p align="center">

*Figure 6. Illustration of uncertainty regarding effective geometry differences to get target flocculating velocity profiles.*

  2. The flow from one channel to another and then out of the flocculator needs to be designed. Consideration on to perhaps using the space in the wasted volume sections or using the ends of the channels where there is uncertainty about the flow geometry as the channel connections.

  3. The maximum angle given from the line created by tracing the first channel's uppermost tip to the last channel's lowermost tip and the first channel's line needs to be created taking into account wasted volume, usable flocculating compartments (that are dependent on target velocity geometries), channel connections, and inflow and outflow pipes.


### Cost comparison future work

The current cost estimate for the flocculatorita is likely much higher than the true cost to produce such a design. This is due to the fact that the costs are based on United States pricing, and materials in Honduras tend to be less expensive. Future work on this project must include price estimates from Honduras, or other countries that may employ the new design.

Furthermore, our design does not include the cost of the support structure for the baffles, cost of the fittings for connecting the rapid mix and the sedimentation tank, cost of the entrance tank and the cost of adjustments necessary for assembling the tank (such as fixing the PVC sheets to the pipe walls or construction of the tank bottom). Moreover, it does not include the cost of manpower.

In addition, the current price estimate is based on PVC sheets being used as baffles in the flocculator. In the future the team will work to discover a different material that can be used as baffles. This ideal material must be durable, less expensive than PVC sheets, and more appropriate for this application than the polycarbonate sheets used in other AguaClara plants.

##Flocculatorita Code

```python
import aguaclara.core.head_loss as minorloss
import aguaclara.design.human_access as ha
import aguaclara.core.physchem as pc
import aguaclara.core.pipes as pipes
from aguaclara.core.units import unit_registry as u
import numpy as np
import pandas as pd

BAFFLE_THICKNESS = 2 * u.mm
PVC_CHANNEL_THICKNESS = 1 * u.inch

class Flocculatorita:
    """Calculates physical dimensions of a flocculatorita
    ----------------------------
    - BAFFLE_K (K or K_{baffle}): float
        - The minor loss coefficient of the flocculator baffles.
    - CHANNEL_N_MIN (N_{channel}: int
        - The minimum number of flocculator channels.
    - HS_RATIO_MIN (\Pi_{HS}): float
        - The minimum ratio between expansion height and baffle spacing
    - RATIO_MAX_HS (\Pi_{HS}): float
        - The maximum ratio between expansion height and baffle spacing
    - SDR (sdr): float
        - The standard dimension ratio.
    """

    # Increased both to provide a safety margin on flocculator head loss and
    # to simultaneously scale back on the actual collision potential we are
    # trying to achieve.
    # Originally calculated to be 2.3 from the equations:


    BAFFLE_K = 2.5
    CHANNEL_N_MIN = 1
    RATIO_MAX_HS = 6.0
    SDR = 41.0
    pi_VC_180bend=.384 #source: (Floc Design PP )

    def __init__(
            self,
            Q=4 * u.L/u.s,
            temp=25 * u.degC,
            Gt=37000,
            HL = 40 * u.cm,
            downstream_H = 2 * u.m,
            ent_tank_L=0*u.m,
            max_W=42 * u.inch,
            available_tank_diameters = [12.2, 15.1, 18.2,24.1, 30.2,36.0,42.0,47.9,59.9,72.0],
            available_obstacle_diameters = [1/2,3/4,1,5/4,3/2,2,5/2,3,7/2,4,5,6,8,10,12,14,16],
            n_channels=5,
            pi_VC_180bend=pi_VC_180bend,
            tank_diameters_prices = [[12.2, 4.07], [15.1, 5.70], [18.2, 8.00],[24.1, 12.64], [30.2, 18.60],[36.0, 24.33], [42.0, 28.40],[47.9 , 39.42] , [59.9, 63.51]],
            baffle_price = (20.5/1872) * u.USD/(u.inch**2),
            PVC_channel_price = (431/4608) * u.USD/(u.inch**2),
            obstacle_diameters_prices = [[1/2, 1.95/5],[3/4, 2.35/5],[1, 3.91/5],[5/4, 4.55/5],[3/2, 4.99/5],[2, 6.90/5],[5/2, 10.26/5],[3, 13.90/5],[7/2, 39.95/5],[4, 18.90/5],[5, 57.50/5],[6, 37.94/5],[8, 55.00/5],[10, 76.81/5],[12, 109.86/5],[14, 180.75/5],[16, 228.52/5]]
            ):

        self.Q = Q
        self.temp = temp
        self.Gt = Gt
        self.HL = HL
        self.downstream_H = downstream_H
        self.ent_tank_L = ent_tank_L
        self.max_W = max_W
        self.n_channels=n_channels
        self.pi_VC_180bend=pi_VC_180bend
        self.available_tank_diameters=available_tank_diameters
        self.tank_diameters_prices = tank_diameters_prices
        self.baffle_price = baffle_price
        self.PVC_channel_price = PVC_channel_price
        self.obstacle_diameters_prices = obstacle_diameters_prices
        self.available_obstacle_diameters = available_obstacle_diameters


    @property
    def vel_grad_avg(self):
        #NOTE: this is borrowed from AguaClara source code
        """Calculate the average velocity gradient (G-bar) of water flowing
        through the flocculator.
        :returns: Average velocity gradient (G-bar)
        :rtype: float * 1 / second
        """
        return ((u.standard_gravity * self.HL) /
               (pc.viscosity_kinematic(self.temp) * self.Gt)).to(u.s ** -1)

    @property
    def retention_time(self):
        #NOTE: this is borrowed from AguaClara source code
        """Calculates the hydraulic retention time neglecting the volume created by head loss in the flocculator.
        :returns: Hydraulic retention time (:math:`\theta`)
        :rtype: float * second
        """
        return (self.Gt / self.vel_grad_avg).to(u.s)

    @property
    def vol(self):
        #NOTE: this is borrowed from AguaClara source code
        """Calculate the target volume (not counting the volume added by head loss) of the flocculator.
        :returns: Target volume
        :rtype: float * meter ** 3
        """
        return (self.Q * self.retention_time).to(u.m ** 3)

    @property
    def cross_sectional_area(self):
        """This function calculates the necessary active cross sectional area of the flocculator"""
        return (self.vol/self.downstream_H).to(u.m**2)


    @property
    def min_diameter_tank(self):
        """"this function calculates the necessary diameter to accommodate the required cross sectional area, assuming that the only "active space" in the cross section is the largest square that will fit into the larger PVC pipe"""
        return ((2*self.cross_sectional_area)**.5).to(u.inch)

    @property
    def design_diameter_tank(self):
        """This function selects the closest available PVC tank to the calculated minimum pipe diameter"""
        for i in range(len(self.available_tank_diameters)):
            if self.available_tank_diameters[i]*u.inch <= self.min_diameter_tank:
                i +=1
            else:
                return self.available_tank_diameters[i]*u.inch

    @property
    def channel_L(self):
        """This function determines channel length based the largest square that fits inside of the selected tank. So, channel length is the the length of the square"""
        return ((self.design_diameter_tank)**2/2)**.5

    @property
    def channel_W(self):
       """This function calculates the channel width by dividing the total width of the active cross sectional area by number of channels"""
       return (self.channel_L/self.n_channels).to(u.cm)
       ###NOTE: incorporate baffle width

    @property
    def expansion_max_H(self):
        #NOTE: This is borrowed from AguaClara source code
        """"Return the maximum distance between expansions for the largest
        allowable H/S ratio.
        :returns: Maximum expansion distance
        :rtype: float * meter
        Examples
        --------
        exp_dist_max(20*u.L/u.s, 40*u.cm, 37000, 25*u.degC, 2*u.m)
        0.375 meter
        """
        return (((self.BAFFLE_K / (2 * pc.viscosity_kinematic(self.temp) * (self.vel_grad_avg ** 2))) *
                (self.Q * self.RATIO_MAX_HS / self.channel_W) ** 3) ** (1/4)).to(u.m)

    @property
    def expansion_n(self):
        #NOTE: This is borrowed from AguaClara source code
        """Return the minimum number of expansions per baffle space.
        :returns: Minimum number of expansions/baffle space
        :rtype: int
        """
        return np.ceil(self.downstream_H / self.expansion_max_H)

    @property
    def expansion_H(self):
      #NOTE: This is borrowed from AguaClara source code#NOTE: This is borrowed from AguaClara source code
        """Returns the height between flow expansions.
        :returns: Height between flow expansions
        :rtype: float * centimeter
        """
        return (self.downstream_H / self.expansion_n).to(u.cm)

    @property
    def baffle_S(self):
      #NOTE: This is borrowed from AguaClara source code
        """Return the spacing between baffles.
        :returns: Spacing between baffles
        :rtype: int
        """
        return ((self.BAFFLE_K /
                ((2 * self.expansion_H * (self.vel_grad_avg ** 2) *
                 pc.viscosity_kinematic(self.temp))).to_base_units()) ** (1/3) *
               self.Q / self.channel_W).to(u.cm)

    @property
    def obstacle_n(self):
      #NOTE: This is borrowed from AguaClara source code
        """Return the number of obstacles per baffle.
        :returns: Number of obstacles per baffle
        :rtype: int
        """
        return self.expansion_n - 1

    @property
    def obstacle_size(self):
        """This function calculates the size of obstacles, so that the obstacles cause the same flow expansion as a 180 degree bend in the flocculatorita"""

        for i in range(len(self.available_obstacle_diameters)):
            if (self.baffle_S*(1-self.pi_VC_180bend)).to(u.inch) >= self.available_obstacle_diameters[i]/2*u.inch :
                i +=1
            else:
                return self.available_obstacle_diameters[i]*u.inch

    @property
    def baffle_n(self):
        """This function calclulates the number of the baffles in the flocculator."""
        return (np.ceil((self.channel_L/self.baffle_S*self.n_channels))).to(u.dimensionless)

    @property
    def design(self):
        """Returns the designed values.
        :returns: list of designed values (G, t, channel_W, obstacle_n)
        :rtype: int
        """
        floc_dict = {'n_channels': self.n_channels,
                     'channel_L': self.channel_L,
                     'channel_W': self.channel_W,
                     'baffle_S': self.baffle_S,
                     'obstacle_n': self.obstacle_n,
                     'G': self.vel_grad_avg,
                     't': self.retention_time,
                     'expansion_max_H': self.expansion_max_H,
                     'min_diameter_tank': self.min_diameter_tank,
                     'design_diameter_tank': self.design_diameter_tank}
        return floc_dict

    @property
    def cost_of_tank(self):
        """Returns the cost of the tank.
        """
        for i in range(len(self.available_tank_diameters)):
            if self.available_tank_diameters[i]*u.inch < self.design_diameter_tank:
                i +=1
            else:
                return (self.tank_diameters_prices[i][1]*(u.USD/u.ft) * (self.downstream_H + self.HL + 10*u.cm)).to(u.USD)

    @property
    def cost_of_baffles(self):
        """Returns the cost of the baffels.
        """

        return (self.channel_W * (self.downstream_H + self.HL + (10 * u.cm)) * self.baffle_n * self.n_channels * self.baffle_price).to(u.USD)

    @property
    def cost_of_PVC_channels(self):
        """Returns the cost of the PVC Channels.
        """
        return ((self.n_channels+1) * (self.downstream_H + self.HL + 10 * u.cm) * self.channel_L * self.PVC_channel_price).to(u.USD)


    @property
    def cost_of_obstacles(self):
        """Returns the cost of the obstacles.
        """
        for i in range(len(self.available_obstacle_diameters)):
          if self.available_obstacle_diameters[i]*u.inch < self.obstacle_size:
            i +=1
          else:
            return (self.obstacle_diameters_prices[i][1]*(u.USD/u.ft) * self.obstacle_n*self.baffle_n*self.n_channels*self.channel_W/2).to(u.USD)

    @property
    def total_cost(self):
        """Returns the cost total cost.
        """
        return self.cost_of_tank + self.cost_of_baffles + self.cost_of_PVC_channels + self.cost_of_obstacles

    @property
    def cost(self):
        """Returns costs of of everything
        """
        cost_dict = {'cost of tank':self.cost_of_tank,
                     'cost of baffles':self.cost_of_baffles,
                     'cost of PVC channels':self.cost_of_PVC_channels,
                     'cost of halfpipes':self.cost_of_obstacles,
                     'total cost':self.total_cost}
        return cost_dict


    @property
    def pi_sedtank_floc(self):
        """This function calculates the ratio of the sed tank diameter to the flocculator diameter if the sed tank's up flow velocity is 1 mm/s and height is 2 m"""
        up_V=1*u.mm/u.s
        depth=2*u.m
        A_sedtank=self.Q/up_V
        d_sedtank=(2*A_sedtank**.5).to(u.inch)
        return (d_sedtank/self.min_diameter_tank)


##make a data frame to show results
q  = 5 * u.L/u.s #change this flow rate in order to display design specs for the flocculatorita handling that flow rate
tester=Flocculatorita(Q=q)

data ={'':['Tank Pipe Diameter', 'Width of Channels', 'Baffle Spacing', 'Cost'],
       '1 Channel': [Flocculatorita(n_channels=1, Q=q).design_diameter_tank, Flocculatorita(n_channels=1, Q=q).channel_W, Flocculatorita(n_channels=1, Q=q).baffle_S,Flocculatorita(n_channels=1, Q=q).total_cost],
       '2 Channels': [Flocculatorita(n_channels=2, Q=q).design_diameter_tank, Flocculatorita(n_channels=2, Q=q).channel_W, Flocculatorita(n_channels=2, Q=q).baffle_S, Flocculatorita(n_channels=2, Q=q).total_cost],
       '3 Channels': [Flocculatorita(n_channels=3, Q=q).design_diameter_tank, Flocculatorita(n_channels=3, Q=q).channel_W, Flocculatorita(n_channels=3, Q=q).baffle_S,Flocculatorita(n_channels=3, Q=q).total_cost],
       '4 Channels':[Flocculatorita(n_channels=4, Q=q).design_diameter_tank, Flocculatorita(n_channels=4, Q=q).channel_W, Flocculatorita(n_channels=4, Q=q).baffle_S, Flocculatorita(n_channels=4, Q=q).total_cost],
       '5 Channels':[Flocculatorita(n_channels=5, Q=q).design_diameter_tank, Flocculatorita(n_channels=5, Q=q).channel_W, Flocculatorita(n_channels=5, Q=q).baffle_S, Flocculatorita(n_channels=5, Q=q).total_cost],
       '6 Channels':[Flocculatorita(n_channels=6, Q=q).design_diameter_tank, Flocculatorita(n_channels=6, Q=q).channel_W, Flocculatorita(n_channels=6, Q=q).baffle_S,Flocculatorita(n_channels=6, Q=q).total_cost]
       }
Flocculatorita(n_channels=2, Q=q).total_cost

df=pd.DataFrame(data)
print(df)
Flocculatorita(n_channels=7, Q=q).retention_time
Channel_A = Flocculatorita(n_channels=7, Q=q).baffle_S*Flocculatorita(n_channels=7, Q=q).channel_W
((Flocculatorita(n_channels=7, Q=q).min_diameter_tank**2/Channel_A).to(u.dimensionless))**(1/2)
```

##Cost Comparison Code

```python
class Floc_1_min_res(Flocculatorita):
  """This class models a flocculatorita with 1 minute residence time"""
  @property
  def retention_time(self):
    return 5*u.min
  @property
  def vol(self):
    return ((self.Q*self.retention_time).to(u.L))

"""Now, Floc_1_min_res is used to estimate the cost of the floculatorita, which would handle similar flow and have the same collision potential as the current PF300 flocculator.  """
cc=Floc_1_min_res(Q=1*u.L/u.s)
print(cc.retention_time)
print(cc.total_cost)

cc.vel_grad_avg
cc.design_diameter_tank
cc.baffle_n

"""Below are the calculations for the estimate of the cost of the current PF3000 flocculator"""

three_in_pvc=(32.73*u.USD)/(10*u.ft) #this is the cost of a 10' long 3" pvc pipe from [McMaster]https://www.mcmaster.com/pvc
quantity_three_in_pvc=9*2*u.m
price_three_in_pvc=quantity_three_in_pvc*three_in_pvc ##total cost of the 3" PVC pipes that will used for the floculatorita

T_three_in_pvc=	7.66*u.USD #this is the cost from [McMaster]https://www.mcmaster.com/pvc
quantity_T_three_in_pvc=10
price_T_three_in_pvc=T_three_in_pvc*quantity_T_three_in_pvc


three_in_elbow=5.22*u.USD #this is the cost from [McMaster]https://www.mcmaster.com/pvc
quantity_three_in_elbow=12
price_three_in_elbow=three_in_elbow*quantity_three_in_elbow

pvc_sheet= 56.52*u.USD#used to make light deflectors, this is the cost from [McMaster]https://www.mcmaster.com/pvc
quantity_pvc_sheet=1
price_pvc_sheet=pvc_sheet*quantity_pvc_sheet


nuts = 9.18*u.USD #the price of one pack of 25 1/4" stainless steel nuts
quantity_nuts = 1
price_nuts = nuts * quantity_nuts

reducer_3to2 = 10.28 *u.USD #price of a 3" to 2" pvc pipe reducer from McMaster
quantity_reducer_3to2= 1
price_reducer_3to2 = reducer_3to2 * quantity_reducer_3to2

reducer_2to1 = 2.43 *u.USD #price of a 3" to 2" pvc pipe reducer from McMaster
quantity_reducer_2to1= 1
price_reducer_2to1 = reducer_2to1 * quantity_reducer_3to2

PF300cost=(price_three_in_pvc+price_T_three_in_pvc+price_three_in_elbow+price_pvc_sheet+price_nuts+price_reducer_3to2 +price_reducer_2to1).to(u.USD)



comparison=cc.total_cost/PF300cost
print('The floculatorita is', comparison, 'times the cost of the current floculatorita')
```

#References
- 1: Floc Design PP
- 2: Textbook section on Floc Design https://aguaclara.github.io/Textbook/Flocculation/Floc_Design.html#equation-flocculation-floc-design-3
- 3: Floc Source Code https://github.com/AguaClara/aguaclara/blob/master/aguaclara/design/floc.py
- 4: Flocculatorita Prices. Prices are based on US markets.
    - Design diameter: Fortiline Waterworks phone call with Tom in Ohio
    - PVC Channel:https://www.eplastics.com/sheets/hdpe/black-natural?page=3
    - Obstacles:https://www.pvcfittingsonline.com/pipe/schedule-40-pvc-pipe.html
