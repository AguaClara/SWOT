# Flow Control and Measurement Summary Sheet: Useful if we ever need the flow control devices section
Welcome to the first summary sheet of CEE 4540! These documents will be guides and references for you throughout the semester. Since Professor Monroe's class time is limited, so too is the amount of material he can fit on the slides while ensuring that they remain understandable. Thus, these summary sheets will supplement the powerpoints by going into further detail on the course concepts introduced in the slides.

Equations, universal constants, and other helpful goodies can be found in the [aide_design repository on GitHub](https://github.com/AguaClara/aide_design/tree/master/aide_design "aide_design"). Most equations and constants you find in these summary sheets will already have been coded into aide_design, and will be shown here in the following format:  

Variable: `pc.gravity`  
Function: `pc.area_circle(DiamCircle)`.

The letters before the `.`, in this case `pc`, indicate the file within aide_design where the variable or function can be found. In the examples above, `pc.gravity` and `pc.area_circle(DiamCircle)` show that the variable `gravity` and function `area_circle(DiamCicle)` are located inside the physchem.py (`pc`) file. You are heavily, strongly, *tremendously* recommended to look up any aide_design equations you plan to use within in their aide_design file before using them. Each equation has comments describing what the specific conditions are to using it.

For the most part, [hyperlinks in these documents will contain supplementary information](http://likethis.com/ "This link does not go anywhere"). The information contained in the linked external sites is there in case you don't feel completely comfortable with a concept, but is not necessary to learn thoroughly and will not be tested.

<br>
<br>


---

<br>
<br>

## Table of Contents
Please use this table to control/command find the sections you are looking for.

#### **Section 2: Introduction to Flow Control: The Search for Constant Head**  
**2.1)** Tank with a valve  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Flow $Q$ and Water Level $h$ as a Function of Time  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Drain System for a Tank  
**2.2)** Conventional Flow Control Devices  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Floats  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Overflow Tanks  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Mattiot Bottles  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Float Valves  

#### **Section 3: AguaClara Flow Control and Measurement Technologies**   
**3.1)** "Almost Linear" Flow Controller  
**3.2)** Linear Flow Orifice Meter (LFOM)  
**3.3)** Linear Dose Controller  

<br>
<br>


---

<br>
<br>

## Section 2: Introduction to Flow Control: The Search for Constant Head   

The term **constant head** means that flowing water flows with the same energy over time, the flow rate does not change. Constant head implies constant flow. It is as if the orifice equation applied to a hole in the bottom of a bucket, but somehow $\Delta h$ never changes, the water level in the bucket is always the same even though water is flowing out of it. Since the water level is always the same, the flow is always the same too. The challenge is getting the water level to always stay the same, or to create a system that doesn't just use buckets and holes to maintain constant head.

While constant head can now be achieved with pump/computers systems, this was not always the case. Getting constant head has been a challenge to engineers for a long time. This problem becomes even harder when considering that we need constant head for dosing purposes. For example, the chlorine concentration in treated water must always be the same for a particular plant, even if the plant flow rate changes over the course of a day. If the same flow of chlorine is dosed as the flow rate of a plant changes, then the concentration of chlorine in the treated water will not be what it should be. The ideal dosing system accounts for the change of plant flow rate.  

So the challenge of constant head in chemical dosing is not _just_ providing one continuous flow of chlorine, it is also varying that flow in proportion to the plant flow rate.  

This section presents some historical solutions to creating constant head.

### Important Terms

1. Constant Head
2. Chlorination
3.

### Important Equations
1. Tank-with-a-valve / Hole-in-a-bucket equation
2. Tank Drain equation

## 2.1) Tank with a Valve  
### Flow $Q$ and Water Level $h$ as a Function of Time  
As evidenced by the orifice equation, a bucket or tank of water with a hole poked in the bottom or side does not provide constant flow over time. Why not? In the orifice equation, $Q = \Pi_{vc} A_{or} \sqrt{2g \Delta h}$, flow $Q$ is a function of the height of water above the orifice, $\Delta h$. Since the water drains from the hole over time, the height of water above the orifice necessarily changes. The first approach in the search for a constant flow rate is understanding and manipulating the 'tank-with-a-valve' system, as tightening or loosening a valve is one of the most simple ways of controlling the flow of water.

The system we are using to gain an understanding of this 'tank-with-a-valve' scenario is shown below. In the image, a hypochlorite solution is slowly dripping and mixing with piped source water, thereby disinfecting it. The valve is almost closed to make sure that the hypochlorite solution drips instead of flows.

![What does this text do again?](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/complete_hypochlorinator.jpg?raw=true)

[Found here](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Derivation_flow_through_tank_with_a_valve.md "Hypochlorinator derivation"), the derivation for flow as a function of time yields the following equation:

$$ \frac{Q}{Q_0} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$$

Such that:  
$Q$ = $Q(t)$ = flow of hypochlorite through valve at time $t$   
$Q_0$ = flow of hypochlorite through valve at time $t$ = 0    
$t$ = elapsed time  
$t_{Design}$ = time it would take for tank to empty if flow stayed constant at $Q_0$, which it does not  
$h_{Tank}$ = elevation of water level with reference to tank bottom at time $t$ = 0  
$h_0$ = elevation of water level with reference to the valve at time $t$ = 0   
**Note:** While the derivation uses a hypochlorinator as an example, this section will refer to the hypochlorinte solution as 'water' from now on, since that is the fluid most commonly considered in this class.

This equation has consistently been a source of confusion for students, and its nuances are thoroughly explained in the derivation, which you are recommended to read. These nuances will be quickly summarized below:

- $t_{Design}$ is **NOT** the time it takes to drain the tank. It is the time that it _would_ take to drain the tank _if_ the flow rate at time $t = 0$, $Q_0$, were the flow rate forever, which it is not. $t_{Design}$ was used in the derivation to simplify the equation, which is why this potentially-confusing parameter exists. The actual time it takes to drain the tank lies somewhere between $t_{Design}$ and $2 \cdot t_{Design}$ and depends on the ratio between $h_{Tank}$ and $h_{0}$
- $h_{Tank}$ is not the same as $h_{0}$. $h_{Tank}$ is the height of water level in the tank with reference to the tank bottom. $h_{0}$ is the water level in the tank with reference to the valve. Neither change with time, they both refer to the water level and time $t$ = 0. Therefore, $h_{0} \geq h_{Tank}$ is true if the valve is located at or below the bottom of the tank. If the tank is elevated far above the valve, then the $h_{0} > > h_{Tank}$. If the valve is at the same elevation as the bottom of the tank, then $h_{0} = h_{Tank}$. Please refer to the image above to clarify $h_{0}$ and $h_{Tank}$.

"How does this 'tank-with-a-valve' scenario differ from the 'hole-in-a-bucket' scenario?" you might ask. If you would like, you may go through the derivation on your own, using the orifice equation instead of the minor loss equation for the first step. If you do so, you'll find that the equation remains almost the same, the only difference is that the $\frac{h_{Tank}}{h_0}$ term drops out for an orifice, as $h_{Tank} = h_0$. The big difference in the systems lies with the flexibility of the valve. It can be tightened or loosened to change the flow rate, whereas changing the size of an orifice multiple times in a row is not easy nor recommended.

Thanks to the derivation, we have an expression of flow out of the system as a function of time. To complete our understanding, we need another expression for water level $h$ (or
$\Delta h$) as a function of time. Fortunately, this is very easy to find. Both the orifice equation for the hole-in-a-bucket scenario and the minor loss equation for the 'tank-with-a-valve' scenario show that flow that is proportional to the square root of the driving head, $Q \propto h$. We can use this proportionality to come up with an equation relating the height of the water to the flow of water using the flow and height at time $t = 0$ as a reference:

$$\frac{Q}{Q_0} = \sqrt{\frac{h}{h_0}}$$

Substituting this equation back into $\frac{Q}{Q_0} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$, we obtain an equation relating height of water as a function of time.  

$$\frac{h}{h_0} = \left( 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0} \right)^2$$

Such that:  
$h$ = $h(t)$ = elevation of water level with reference to the valve.

With these two equations for flow $Q$ and water level $h$ as a function of time, we can make a plot, shown below, to visualize what's going on. The plot below shows normalized water level (referred to as depth) and flow. Normalized simply refers to the ratio of current/initial, so normalized flow refers to $\frac{Q}{Q_0}$ and normalized depth _in the tank_ refers to $\frac{h}{h_0}$. **The 'tank-in-a-valve' system this plot is based on has the valve at the same elevation as the bottom of the tank**, so $h_{Tank} = h_0$. $t_{Design} = 4$ days

![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Tank_valve_not_elevated.jpg?raw=true)

This plot shows the interesting relationship of both water depth and flow over time. The relationship is unfortunate in this case, as normalized flow goes from 1 to 0, which is clearly not _constant_ head. Ideally, the normalized flow $\frac{Q}{Q_0}$ would be a horizontal line, such that  $\frac{Q}{Q_0} = 1$. We can manipulate the equation $\frac{Q}{Q_0} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$ to get closer to $\frac{Q}{Q_0} = 1$ by making $\frac{h_{Tank}}{h_{0}}$ very, very large to make the $\frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}$ term drop out. What does this mean in real life? It means having the valve far, far below the bottom of the tank. Since putting the valve underground does not make sense, this solution implies that the tank must be raised far, far above the valve. In the plot below, $h_0 = 50 \cdot h_{Tank}$

![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Tank_valve_elevated.jpg?raw=true)

This plot is exactly what we want, $\frac{Q}{Q_0} \approx 1$. While the water depth declines as the tank empties, the flow rate remains roughly constant. Unfortunately, we had to elevate our tank about 50 times its height. So for a standard 1 meter tall tank, it would have to be elevated by 50 meters. This is not realistically feasible. Other solutions must be used for effective and elegant constant head management.

### Drain System for a Tank  
While our efforts to understand the 'tank-with-a-valve' scenario did not lead to a great constant head/chemical dosing solution, we can use our understanding to properly design drain systems for AguaClara reactors like flocculators and sedimentation tanks, since they basically tanks with valves. Our goal is to calculate how large to make the drain pipe for flocculators or sed tanks if we want them to drain in a certain amount of time, $t_{Drain}$. Note that $t_{Drain}$ is _not_ the same as $t_{Design}$ from the previous section. The derivation for the following equation is found [here](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Derivation_drain_system_design.md), along with more details on AguaClara's pipe stub method for draining tanks. The derived Tank Drain equation is as follows:

$$D_{Pipe} = \sqrt{ \frac{8 L_{Tank} W_{Tank}}{\pi t_{Drain}}} {\left( \frac{H_{Tank} \sum K_e }{2g} \right)^{\frac{1}{4}}}$$

The equation can also be rearranged to solve for the time it would take to drain a tank given its dimensions and a certain drain pipe size:

$$t_{Drain} =  \frac{8 L_{Tank} W_{Tank}}{\pi D_{Pipe}^2} {\left( \frac{H_{Tank} \sum K_e }{2g} \right)^{\frac{1}{2}}}$$

Such that the variables are as they appear in the image below:  
![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Pipe_stub_drainage_variables.jpg?raw=true)


## 2.2) Constant Head Devices  
This section will describe very briefly some common devices and clever systems that can be used to generate constant head. Visualizing these devices in action is extremely helpful to understanding them, which is why you are recommended to view the 'Constant head devices' section in the 'Flow Control and Measurement' powerpoint. Since the powerpoint does a great job of illustrating these devices, this section will be kept very brief.

### Floats  
A logical way to ensure constant head is to find a device that moves in accordance with the water level- something that floats. The idea is to combine this something that floats, which is usually referred to as just a **float**, with another device that allows the water to flow, usually an orifice. By fixing the orifice to the float such that the orifice is always underwater, constant head can be achieved. No matter what happens to the water level, the float will float and the orifice will always experience constant head. There are many, many possibilities with float systems, two of which are shown below.

**Advantages:**
- Easy to design and fabricate
- System does not need to be shut off to add more water to tank

**Disadvantages:**  
- Inflexible. What happens when you want to change the distance between the orifice and the float?

![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Different_Floats.jpg?raw=true)

### Overflow Tanks
This constant head system requires a pump. It consists of an overhead tank to store water with an orifice or pipe for the constant head of water to flow through. The pump fills the overhead tank as it empties, and provides more water than necessary. This extra water leaves through an overflow pipe, which is why this device is called an overflow tank. An image is shown below. Within the AguaClara lab, the Ram Pump team uses an overflow tank setup, if you would like a closer look.

**Advantages:**  
- System does not need to be shut off to add more water to tank
- Very simple to design if you have an adequate pump available

**Disadvantages:**
- Requires a pump and therefore electricity
- Requires lots of vertical space

![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Overflow_tank.jpg?raw=true)

### Marriot Bottles   
Marriot bottles are simple yet exceedingly clever devices to ensure constant flow out of a bottle or tank. [This video](https://www.youtube.com/watch?v=y1S5Md0WhNM "1 minute and 21 seconds of pure beauty") provides a great example of one in practice. The only outlet to atmosphere is through the long tube filled with air, as the top of the bottle is completely capped. Therefore the bottom of _both_ tubes is always at atmospheric pressure, even as the water level in the bottle falls.

**Advantages:**  
- Easy to fabricate  
- Can change the amount of constant head by raising or lowering the end of the tube that is dispensing the water

**Disadvantages:**  
- Batch process, adding water requires that the system stop working for some time.

![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Marriot_bottle.jpg?raw=true)

### Float Valves  
A very clever device, a float valve consists of a float attached to a lever which controls a valve. When there is a low water level, the valve is open. As the water rises, it pushes the float upwards. As the float moves upwards, the lever forces the valve to close, until the float reaches its maximum level and the valve closes completely. Float valves can be used to create tanks or bottles with unchanging water levels, even as water exits the tank or bottle. Float valves are a critical part to AguaClara's flow control system. Most toilets found in homes have float valves to ensure that water doesn't spill out of the toilet tank and onto the floor. [Here is a video](https://www.youtube.com/watch?v=hAxAyoSMQhI "This is the best video ever") explaining how a conventional toilet works. Please note the role of the float valve, which is to make sure that the water stops entering the toilet's tank once the water level has reached a specific point.


**Advantages:**  
- Very flexible in its uses. Can easily be a component of a more complex system, like toilets
- Can be very compact

**Disadvantages:**
- Doesn't actually create constant flow. It simply allows the water level in a tank to be constant, or to rise to an upper limit. An orifice or other device would be required in the tank using a float valve to create constant flow.

![Credit to https://www.amazon.com/Kerick-Valve-MA052-Float-Adjustable/dp/B0077RAP1I for the valve image](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Float_valve.jpg?raw=true)


## Section 3: AguaClara Flow Control and Measurement Technologies
Now that you have the necessary context, you finally get to learn about AguaClara's technologies and innovations! Each technology or component for this section will have five subsections:
- **What it is**  
- **What it does**  
- **Why it is necessary**
- **How it works**
- **Notes**

Using all of the acquired knowledge and information from the sections above, AguaClara has designed different flow control and measurement technologies for different purposes and scenarios. Each of these has evolved over time as new and creative innovations have improved the original designs.

Before diving into the technologies, recall the purpose of the chemicals that we are seeking to constantly **dose**, and why it is important to keep a constant, specific dose. Also recall that 'dose' means 'concentration of chemical' _in the water we are trying to treat_, not in the stock tanks of the chemicals.
- [**Coagulant**](https://en.wikipedia.org/wiki/Coagulation_(water_treatment) "Coagulation wikipedia") like alum, PAC, and some iron-based chemicals are used to turn small particles into bigger particles, allowing them to be captured more easily. Waters with high [**turbidity**](https://en.wikipedia.org/wiki/Turbidity "Turbidity wikipedia"), indicative of a lot of particles like clay and bacteria, require more coagulant to treat effectively. Additionally, waters with a lot of [**organic matter**](https://en.wikipedia.org/wiki/Organic_matter "Organic matter wikipedia") require significantly more coagulant to treat.
- [**Chlorine**](https://en.wikipedia.org/wiki/Water_chlorination "Chlorination wikipedia") is used to disinfect water that has already been fully treated. A proper and consistent chlorine dose is required, as too low of a dose creates a risk of reintroduction of pathogens in the distribution system and too high of a dose increases the risk of carcinogenic [disinfection byproduct](https://en.wikipedia.org/wiki/Disinfection_by-product "DBP wikipedia") formation.

### Important Terms  
1. Dose
2. Coagulant
3. Chlorination
4. Turbidity
5. Organic Matter
6. Constant Head Tank

### Important Equations
1.

## 3.1) "Almost Linear" Flow Controller
### What it is
This device consists of a bottle of chemical solution (called the **Constant Head Tank**, CHT) a float valve to keep a solution in the CHT at a constant water level, a flexible tube starting at the bottom of the CHT, and many precisely located holes in a pipe, as the image below shows. The holes in the pipe hold the other end of the tube that starts at the CHT.

Chemical solution, either coagulant or chlorine, is stored in a stock tank somewhere above the CHT. A different tube connects the stock tank to the float valve within the CHT.

![Image link](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Images/Almost_linear_flow_controller.jpg?raw=true)

## What it does  
This flow controller provides a constant flow of chemical solution to the water in the plant. When the end of the flexible tube is placed in a hole, the elevation difference between the water lever in the bottle and the hole is set and does not change unless the tube is then placed in another hole. Thus, a constant flow is provided.   

## Why it is necessary
As has been mentioned previously, the amount of chlorine and coagulant that must be added to the raw water changes depending on the flow rate of the plant; the change is necessary to keep the dose constant. More water flowing through the plant, more chlorine necessary to maintain the dose of chlorine in the treated water constant. For coagulant, there are also other factors that impact the required dose, including the turbidity of the water and the amount of organic matter in the water. This means that the operator must be able to change the dose of both coagulant and chlorine quickly and easily, and they must be able to know what the new dose they set is. The "Almost Linear" Flow Controller accomplishes this by having a large number of holes in the flow control pipe next to the constant head bottle. These large number of holes let the operator quickly adjust the flow of chemicals into the raw water by moving the end of the flexible tube from one hole to another.

## How it works
The idea behind this flow controller was to have a linear relationship between the elevation difference in the water level and the end of the flexible tube and the flow rate coming out of the flexible tube, $\Delta h \propto Q$.

As you remember from section 1.4), the summary of Fluids Review, $\Delta h \propto Q$ is only true for major losses and laminar flow. Therefore, we need to make sure that flow is always laminar in the flexible tube that goes between the CHT and the holes while also making sure that major losses far exceed minor losses.  
