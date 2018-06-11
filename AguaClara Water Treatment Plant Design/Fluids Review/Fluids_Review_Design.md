# Fluids Review Summary Sheet
Welcome to the **first** summary sheet of CEE 4540! These documents will be guides and references for you throughout the semester. Since Professor Monroe's class time is limited, so too is the amount of material he can fit on the slides while ensuring that they remain understandable. Thus, these summary sheets will supplement the powerpoints by going into further detail on the course concepts introduced in the slides.

Equations, universal constants, and other helpful goodies can be found in the [aide_design repository on GitHub](https://github.com/AguaClara/aide_design/tree/master/aide_design "aide_design"). Most equations and constants you find in these summary sheets will already have been coded into aide_design, and will be shown here in the following format:  

Variable: `pc.gravity`  
Function: `pc.area_circle(DiamCircle)`.

The letters before the `.`, in this case `pc`, indicate the file within aide_design where the variable or function can be found. In the examples above, `pc.gravity` and `pc.area_circle(DiamCircle)` show that the variable `gravity` and function `area_circle(DiamCicle)` are located inside the [physchem.py](https://github.com/AguaClara/aide_design/blob/master/aide_design/physchem.py) (`pc`) file. You are strongly recommended to look up any aide_design equations you plan to use within in their aide_design file before using them, even if they are given here in this summary sheet. This is because each equation has comments in its original file describing what the specific conditions are to using it.

For the most part, [hyperlinks in these documents will contain supplementary information](http://likethis.com/ "This link does not go anywhere"). The information contained in the linked external sites is there in case you don't feel completely comfortable with a concept, but is not necessary to learn thoroughly and will not be tested.

<br>
<br>


---


<br>
<br>

## Table of Contents
Please use this table to control/command find the sections you are looking for.

#### **Section: Fluids Review**
**The Bernoulli and Energy Equations**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;The Bernoulli Equation  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;The Energy Equation  
**Head Loss**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Major losses  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Minor losses  
**Head Loss = Elevation Difference Trick**  
**The Orifice Equation**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Vena Contracta    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - &nbsp;Origin  
**Section Summary**  


<br>
<br>


---

<br>
<br>

## Section: Fluids Review
This section is meant to be a brief refresher on fluid mechanics. It will only cover the topics of fluids mechanics that will be used heavily in the course.

If you wish to review fluid mechanics in (much) more detail, please refer to [this guide](https://github.com/AguaClara/CEE4540_Master/wiki/Fluids-Review-Guide "CEE 4540 Fluids Review"). If you wish to review from the textbook used in  CEE 3310, the intro to fluid mechanics course at Cornell, you can find a pdf of the book [here](https://hellcareers.files.wordpress.com/2016/01/fluid-mechanics-seventh-edition-by-frank-m-white.pdf "CEE 3310 textbook").

### Important Terms
1. Head
2. Streamline
3. Head loss
4. Laminar
5. Turbulent
6. Moody Diagram
7. Viscosity
8. Driving head
9. Vena Contracta/Coefficient of Contraction

### Important Equations
1. Bernoulli equation
2. Energy equation
3. Darcy-Weisbach equation
4. Reynolds number
5. Swamee-Jain equation
6. Hagen-Poiseuille equation
7. Orifice equation

## The Bernoulli and Energy Equations
As explained in CEE 3310 with more details than most of you wanted to know, the Bernoulli and energy equations are incredibly useful in understanding the transfer of the fluid's energy throughout a [**streamline**](https://en.wikipedia.org/wiki/Streamlines,_streaklines,_and_pathlines "Streamline wikipedia") or through a control volume. The Bernoulli equation applies to two different points along one streamline, whereas the energy equation applies across a control volume. The energy of a fluid has three forms: pressure, potential (deriving from elevation), and kinetic (deriving from velocity).
### The Bernoulli Equation
These three forms of energy expressed above make up the Bernoulli equation:

$$\frac{p_1}{\rho g} + {z_1} + \frac{v_1^2}{2g} = \frac{p_2}{\rho g} + {z_2} + \frac{v_2^2}{2g}$$

Such that:  
$p$ = pressure,  $\frac{[M]}{[L] \cdot [T]^2}$  
$\rho$ = fluid density, $\frac{[M]}{[L]^3}$    
$g$ = acceleration due to gravity,  $\frac{[L]}{[T]^2}$, in aide_design as `pc.gravity`  
$z$ = elevation relative to a reference, $[L]$  
$v$ = fluid velocity, $\frac{[L]}{[T]}$  
Where letters in brackets specify units:  
$[M]$ = mass  
$[L]$ = length  
$[T]$ = time   

Notice that each term in this form of the Bernoulli equation has units of $[L]$, even though the terms represent the energy of water, which has units of $\frac{[M] \cdot [L]^2}{[T]^2}$. When energy of water is described in units of length, the term used is called **head**.

There are two important distinctions to keep in mind when using head to talk about energy. First is that head is dependent on the density of the fluid under consideration. Take mercury, for example, which is around 13.6 times more dense than water. 1 meter of mercury head is therefore equivalent to around 13.6 meters of water head. Second is that head is independent of the amount of fluid being considered, *as long as all the fluid is the same density*. Thus, raising 1 liter of water up by one meter and raising 100 liters of water up by one meter are both equivalent to giving the water 1 meter of water head, even though it requires 100 times more energy to raise the hundred liters than to raise the single liter. Since we are concerned mainly with water in this class, we will refer to 'water head' simply as 'head'.

Going back to the Bernoulli equation, the $\frac{p}{\rho g}$ term is called the pressure head, $z$ the elevation head, and $\frac{v^2}{2g}$ the velocity head. The following diagram shows these various forms of head via a 1 meter deep bucket (left) and a jet of water shooting out of the ground (right).

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Different_forms_of_head.jpg?raw=true" width=550></center>

#### Assumption in using the Bernoulli equation  
Though there are [many assumptions needed to confirm that the Bernoulli equation can be used](https://en.wikipedia.org/wiki/Bernoulli%27s_principle#Incompressible_flow_equation "Bernoulli wikipedia"), the main one for the purpose of this class is that energy is not gained or lost throughout the streamline being considered. If we consider more precise fluid mechanics terminology, then "friction by viscous forces must be negligible." Energy can only be transferred between its three forms if this equation is to be used, it can't be gained or lost.

#### Example problems

[Here is a simple worksheet with very straightforward example problems using the Bernoulli equation.](https://www.teachengineering.org/content/cub_/lessons/cub_bernoulli/cub_bernoulli_lesson01_bepworksheetas_draft4_tedl_dwc.pdf "Bernoulli worksheet") Note that the solutions use the pressure-form of the Bernoulli equation. This just means that every term in the equation is multiplied by $\rho g$, so the pressure term is just $P$. The form of the equation does not affect the solution to the problem it helps solved.

### The Energy Equation
The assumption necessary to use the Bernoulli equation, which is stated above, represents the key difference between the Bernoulli equation and the energy equation for the purpose of this class. The energy equation accounts for the (L)oss of energy from both the fluid flowing, $h_L$, and the charging of a (T)urbine, $h_T$, as well as energy gain provided by a (P\)ump, $h_P$.

$$\frac{p_{1}}{\rho g} + z_{1} + \alpha_{1} \frac{\bar v_{1}^2}{2g} + h_P = \frac{p_{2}}{\rho g} + z_{2} + {\alpha_{2}} \frac{\bar v_{2}^2}{2g} + h_T + h_L$$

You'll also notice the $\alpha$ term attached to the velocity head. This is a correction factor for kinetic energy, and will be neglected in this class. If you wish to learn more about the correction factors, [click here to sate your curiosity](http://nptel.ac.in/courses/105106114/pdfs/Unit6/6_1.pdf "Correction factor pdf"). In the Bernoulli equation, the velocity of the streamline of water is considered, $v$. The energy equation, however compares control surfaces instead of streamlines, and the velocities across a control surface many not all be the same. Hence, $\bar v$ is used to represent the average velocity. Since AguaClara does not use pumps nor turbines, $h_P = h_T = 0$. With these simplifications, the energy equation can be written as follows:

$$\frac{p_{1}}{\rho g} + z_{1} + \frac{\bar v_{1}^2}{2g} = \frac{p_{2}}{\rho g} + z_{2} + \frac{\bar v_{2}^2}{2g} + h_L$$  

**This is the form of the energy equation that you will see over and over again in CEE 4540.** To summarize, the main difference between the Bernoulli equation and the energy equation for the purposes of this class is energy loss. The energy equation accounts for the fluid's loss of energy over time while the Bernoulli equation does not. So how can the fluid lose energy?

**Important Note:** Many images will be used over the course of this class to show hydraulic systems. A standardized system of lines will be used throughout them all to distinguish reference elevations from control volumes from streamlines. This system is described in the image below.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Image_control_volumes.jpg?raw=true" width=550></center>

## Head Loss
**Head (L)oss**, $h_L$ is a term that is ubiquitous in both this class and fluid mechanics in general. Its definition is exactly as it sounds: it refers to the loss of energy of a fluid as it flows through space. There are two components to head loss: major losses caused by pipe-fluid (f)riction, $h_{\rm{f}}$, and minor losses caused by fluid-fluid friction resulting from flow (e)xpansions, $h_e$, such that $h_L = h_{\rm{f}} + h_e$.

### Major Losses
These losses are the result of friction between the fluid and the surface over which the fluid is flowing. A force acting parallel to a surface is referred to as [shear](https://en.wikipedia.org/wiki/Shear_force "Shear wikipedia"). It can therefore be said that major losses are the result of shear between the fluid and the surface it's flowing over. To help in understanding  major lo
sses, consider the following example: imagine, as you have so often in physics class, pushing a large box across the ground. Friction is what resists your efforts to push the box. The farther you push the box, the more energy you expend pushing against friction. The same is true for water moving through a pipe, where water is analogous to the box you want to move, the pipe is similar to the floor that provides the friction, and the major losses of the water through the pipe is analogous to the energy _**you**_ expend by pushing the box.

In this class, we will be dealing primarily with major losses in circular pipes, as opposed to channels or pipes with other geometries. Fortunately for us, Henry Darcy and Julius Weisbach came up with a handy equation to determine the major losses in a circular pipe _under both [**laminar**](https://en.wikipedia.org/wiki/Laminar_flow "Laminar flow wikipedia") and [**turbulent**](https://en.wikipedia.org/wiki/Turbulence "Turbulent flow wikipedia") flow conditions_. Their equation is logically but unoriginally named the [**Darcy-Weisbach equation**](https://en.wikipedia.org/wiki/Darcy%E2%80%93Weisbach_equation "Darcy-Weisbach wikipedia"). If you would like a refresher on laminar vs turbulent flow, please watch [this video](https://www.youtube.com/watch?v=qtvVN2qt968) and note that AguaClara uses a transition number of 2,100, instead of the 2,300 shown in the video; this concept is discussed a few paragraphs below this. Here is the Darcy-Weisbach equation:

$$h_{\rm{f}} \, = \, {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$$

Substituting the continuity equation $Q = \bar vA$ in the form of $\bar v^2 = \frac{16Q^2}{\pi^2 D^4}$ gives another, equivalent form of Darcy-Weisbach which uses flow, $Q$, instead of velocity, $\bar v$:

$$h_{\rm{f}} \, = \,{\rm{f}} \frac{8}{g \pi^2} \frac{LQ^2}{D^5}$$

Such that:  
$h_{\rm{f}}$ = major loss, $[L]$  
$\rm{f}$ = Darcy friction factor, dimensionless   
$L$ = pipe length, $[L]$  
$Q$ = pipe flow rate, $\frac{[L]^3}{[T]}$  
$D$ = pipe diameter, $[L]$  


**Function in aide_design:** `pc.headloss_fric(FlowRate, Diam, Length, Nu, PipeRough)` Returns only major losses. Works for both laminar and turbulent flow.

Darcy-Weisbach is wonderful because it applies to both laminar and turbulent flow regimes and contains relatively easy to measure variables. The one exception is the Darcy friction factor, $\rm{f}$. This parameter is an approximation for the magnitude of friction between the pipe walls and the fluid, and its value changes depending on the whether or not the flow is laminar or turbulent, and varies with the [**Reynolds number**](https://en.wikipedia.org/wiki/Reynolds_number "Reynolds number wikipedia"), $\rm{Re}$, in both regimes of flow. Recall that the Reynolds number is a dimensionless value used to quantify and distinguish laminar and turbulent flow. The equation for Reynolds number *in a circular pipe* is as follows (note that the length dimension used in the equation changes depending on the cross sectional area that the water is flowing through):

$${\rm{Re}}=\frac{4Q}{\pi D\nu} = \frac{\rho \bar vD}{\mu} = \frac{\bar vD}{\nu}$$

Where the three forms simply substitute $Q = \bar v \frac{\pi D^2}{4}$ and $\nu = \frac{\mu}{\rho}$  

Such that:  
$Q$ = pipe flow rate, $\frac{[L]^3}{[T]}$  
$D$ = pipe diameter, $[L]$    
$\bar v$ = fluid velocity $\frac{[L]}{[T]}$  
$\nu$ = fluid kinematic viscosity, $\frac{[L]^2}{[T]}$    
$\mu$ = fluid dynamic viscosity, $\frac{[M]}{[L][T]}$  

**Function in aide_design:** `pc.re_pipe(FlowRate, Diam, Nu)` Returns the Reynolds number *in a circular pipe*. Functions for finding the Reynolds number through other conduits and geometries can also be found in [physchem.py](https://github.com/AguaClara/aide_design/blob/master/aide_design/physchem.py) within aide_design.

[There is a transition between laminar and turbulent flow which is not yet well understood](https://en.wikipedia.org/wiki/Laminar%E2%80%93turbulent_transition "Transitional flow wikipedia"). To simplify this phenomenon and make it possible to code for laminar or turbulent flow, we will assume that the transition occurs at $\rm{Re}$ = 2100. The flow regime is assumed to be laminar below this value and turbulent above it. This variable is coded into aide_design as `pc.RE_TRANSITION_PIPE`.

For laminar flow, the friction factor can be determined from the following equation:

$${\rm{f}} = \frac{64}{\rm{Re}}$$

For turbulent flow, the friction factor is more difficult to determine. In this class, we will use the [Swamee-Jain equation](https://en.wikipedia.org/wiki/Darcy_friction_factor_formulae#Swamee%E2%80%93Jain_equation "Swamee-Jain wikipedia"):

$${\rm{f}} = \frac{0.25} {\left[ \log \left( \frac{\epsilon }{3.7D} + \frac{5.74}{{\rm Re}^{0.9}} \right) \right]^2}$$

Such that:  
$\epsilon$ = pipe roughness, $[L]$  
$D$ = pipe diameter, $[L]$

**Function in aide_design:** `pc.fric(FlowRate, Diam, Nu, PipeRough)` Returns $\rm{f}$ for laminar *or* turbulent flow. For laminar flow, use '0' for the `PipeRough` input.

The simplicity of the equation for $\rm{f}$ during laminar flow allows for substitutions to create a very useful, simplified equation for major losses during laminar flow. This simplification combines the Darcy-Weisbach equation, the equation for the Darcy friction factor during laminar flow, and the Reynold's number formula:

$$h_{\rm{f}} \, = \,{\rm{f}} \frac{8}{g \pi^2} \frac{LQ^2}{D^5}$$

$${\rm{f}} = \frac{64}{\rm{Re}}$$

$${\rm{Re}}=\frac{4Q}{\pi D\nu}$$

To form the [**Hagen-Poiseuille equation**](https://en.wikipedia.org/wiki/Hagen%E2%80%93Poiseuille_equation "Hagen-Poiseuille wikipedia") for major losses during laminar flow, and *only* during laminar flow:

$$h_{\rm{f}} = \frac{128\mu L Q}{\rho g\pi D^4}$$

$$h_{\rm{f}} = \frac{32\nu L\bar v}{ g D^2}$$

The significance of this equation lies in its relationship between $h_{\rm{f}}$ and $Q$. Hagen-Poiseuille shows that the terms are directly proportional ($h_{\rm{f}} \propto Q$) during laminar flow, while Darcy-Weisbach shows that $h_{\rm{f}}$ grows with the square of $Q$ during turbulent flow ($h_{\rm{f}} \propto Q^2$). As you will soon see, minor losses, $h_e$, will grow with the square of $Q$ in both laminar and turbulent flow. This has implications that will be discussed later, in the flow control section.

In 1944, Lewis Ferry Moody plotted a ridiculous amount of experimental data, gathered by many people, on the Darcy-Weisbach friction factor to create what we now call the [**Moody diagram**](https://en.wikipedia.org/wiki/Moody_chart "Moody wikipedia"). This diagram has the friction factor $\rm{f}$ on the left-hand y-axis, relative pipe roughness $\frac{\epsilon}{D}$ on the right-hand y-axis, and Reynolds number $\rm{Re}$ on the x-axis. The Moody diagram is an alternative to computational methods for finding $\rm{f}$.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Moody.jpg?raw=true" width=500></center>



### Minor Losses

Unfortunately, there is no simple 'pushing a box across the ground' example to explain minor losses. So instead, consider a [hydraulic jump](https://www.youtube.com/watch?v=5spXXZX55C8 "What an amazingly made video, but sorry for the 3310 PTSD"). In the video, you can see lots of turbulence and eddies in the transition region between the fast, shallow flow and the slow, deep flow. The high amount of mixing of the water in the transition region of the hydraulic jump results in significant friction *between water and water* (the measure of a fluid's resistance to internal, fluid-fluid friction is called [**viscosity**](https://en.wikipedia.org/wiki/Viscosity "Viscosity wikipedia")). This turbulent, eddy-induced, fluid-fluid friction results in minor losses, much like fluid-pipe friction results in major losses.

As is the case in a hydraulic jump, a flow expansion (from shallow flow to deep flow) creates the turbulent eddies that result in minor losses. This will be a recurring theme in throughout the course: _**minor losses are caused by flow expansions**_. Imagine a pipe fitting that connects a small diameter pipe to a large diameter one, as shown in the image below. The flow must expand to fill up the entire large diameter pipe. This expansion creates turbulent eddies near the union between the small and large pipes, and these eddies cause minor losses. You may already know the equation for minor losses, but understanding where it comes from is very important for effective AguaClara plant design. For this reason, you are strongly recommended to read through the full derivation, which can be found [here](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Derivation_minor_loss_equation.md "Remember to check this link").

There are three forms of the minor loss equation that you will see in this class:

$$ {\rm{ \mathbf{First \, form:} }} \,\,\, h_e = \frac{\left( \bar v_{in}  - \bar v_{out} \right)^2}{2g}$$

$$ {\rm{ \mathbf{Second \, form:} }} \,\,\, h_e = \frac{\bar v_{in}^2}{2g}{\left( {1 - \frac{A_{in}}{A_{out}}} \right)^2} = \,\,\, \frac{\bar v_{in}^2}{2g} \mathbf{K_e^{'}}$$

$$ {\rm{ \mathbf{Third \, form:} }} \,\,\, h_e = \frac{\bar v_{out}^2}{2g}{\left( {\frac{A_{out}}{A_{in}}} -1 \right)^2} = \,\,\,\, \frac{\bar v_{out}^2}{2g} \mathbf{K_e}$$

Such that:  
$K_e^{'}, \,\, K_e$ = minor loss coefficients, dimensionless

**Function in aide_design:**    
`pc.headloss_exp_general(Vel, KMinor)` Returns $h_e$. Can be either the second or third form due to user input of both velocity and minor loss coefficient. It is up to the user to use consistent $\bar v$ and $K_e$.    
`pc.headloss_exp(FlowRate, Diam, KMinor)` Returns $h_e$. Uses third form, $K_e$.  

The $in$ and $out$ subscripts in each of the three forms refer to the diagram that was used for the derivation:

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Minor_loss_pipe.jpg?raw=true" width=650></center>

The second and third forms are the ones which you are probably most familiar with. The distinction between them, however, is critical. First, consider the magnitudes of $A_{in}$ and $A_{out}$. $A_{in}$ can never be larger than $A_{out}$, because the flow is expanding. When flow expands, the cross-sectional area it flows through must increase. As a result, both $\frac{A_{out}}{A_{in}} > 1$ and $\frac{A_{in}}{A_{out}} < 1$ must always be true. This means that $K_e^{'}$ can never be greater than 1, while $K_e$ technically has no upper limit.

If you have taken CEE 3310, you have seen tables of minor loss coefficients [like this one](https://www.engineeringtoolbox.com/minor-loss-coefficients-pipes-d_626.html "engineeringtoolbox is the best site ever"), and they almost all have coefficients greater than 1. This implies that these tables use the third form of the minor loss equation as we have defined it, where the velocity is $\bar v_{out}$. There is a good reason for using the third form over the second one: $\bar v_{out}$ is far easier to determine than $\bar v_{in}$. Consider flow through a pipe elbow, as shown in the image below.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Minor_loss_elbow.jpg?raw=true" width=400></center>

In order to find $\bar v_{out}$, we first need to know which point is $out$ and which point is $in$. A simple way to distinguish the two points is that $in$ occurs when the flow is most contracted, and $out$ occurs when the flow has fully expanded after that maximal contraction. Going on these guidelines, point 'B' above would be $in$, since it represents the most contracted flow in the elbow-pipe system. Therefore point 'C' would be $out$, as it is the point where the flow has fully expanded after its compression in 'B.'

$\bar v_{out}$ is easy to determine because it is the velocity of the fluid as it flows through the entire area of the pipe. Thus, $\bar v_{out}$ can be found with the continuity equation, since the flow through the pipe and its diameter are easy to measure, $\bar v_{out} = \frac{4 Q}{\pi D^2}$. On the other hand, $\bar v_{in}$ is difficult to find, as the area of the contracted flow is dependent on the exact geometry of the elbow. This is why the third form of the minor loss equation, as we have defined it, is the most common.

## Head Loss = Elevation Difference Trick  
This trick, also called the 'control volume trick,' or more colloquially, the 'head loss trick,' is incredibly useful for simplifying hydraulic systems and is used all the time in this class.

Consider the following image, which was taken from the Flow Control and Measurement powerpoint.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Head_loss_trick.jpg?raw=true" width=500></center>


In systems like this, where an elevation difference is causing the flow of water, the elevation difference is called the **driving head**. In the system above, the driving head is the elevation difference between the water level and the end of the tubing. Usually driving head is written as $\Delta z$ or $\Delta h$, though above it is labelled as $h_L$.

 This image is violating the energy equation by saying that the elevation difference between the water in the tank and the end of the tube is $h_L$. It implies that all of the driving head, $\Delta z$, is lost to head loss and therefore that no water is flowing out of the tubing, which is not true. Let's apply the energy equation between the two red points. Pressures are atmospheric at both points and the velocity of water at the top of tank is negligible.

$$\rlap{\Bigg/}\frac{p_{1}}{\rho g} + z_{1} + \rlap{\Bigg/}\frac{\bar v_{1}^2}{2g} = \rlap{\Bigg/}\frac{p_{2}}{\rho g} + z_{2} + \frac{\bar v_{2}^2}{2g} + h_L$$  

We now get:

$$\Delta z = \frac{\bar v_2^2}{2g} + h_L$$

This contradicts the image above, which says that $\Delta z = h_L$ and neglects $\frac{\bar v_2^2}{2g}$. The image above is correct, however, if you apply the head loss trick. The  trick incorporates the $\frac{\bar v_2^2}{2g}$ term _into_ the $h_L$ term as a minor loss. See the math below:

$$\Delta z = \frac{\bar v_2^2}{2g} + h_e + h_f$$

$$\Delta z = \frac{\bar v_2^2}{2g} + \left( \sum K_e \right) \frac{\bar v_2^2}{2g} + h_f$$

$$\Delta z = \left( 1 + \sum K_e \right) \frac{\bar v_2^2}{2g} + h_f$$

This last step incorporated the kinetic energy term of the energy equation, $\frac{\bar v_2^2}{2g}$, into the minor loss equation by saying that its $K_e$ is 1. From here, we reverse our steps to get $\Delta z = h_L$

$$\Delta z = h_e + h_f$$

$$\Delta z = h_L$$

By applying the head loss trick, you are considering the entire flow of water out of a control volume as lost energy. This is just an algebraic trick, the only thing to remember when applying this trick is that $\sum K_e$ will always be at least 1, even if there are no 'real' minor losses in the system.


## The Orifice Equation

This equation is one that you'll see again and again throughout this class. Understanding it now will be invaluable, as future concepts will use and build on this equation.

### Vena Contracta

Before describing the equation, we must first understand the concept of a [**vena contracta**](https://en.wikipedia.org/wiki/Vena_contracta "Vena Contracta wikipedia"). Refer once more to this image of flow through a pipe elbow.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Minor_loss_elbow.jpg?raw=true" width=400></center>

The flow contracts as the fluid moves from point 'A' to point 'B.' This happens because the fluid can't make a sharp turn at the corner of the elbow. Instead, the streamline closest to the sharp turn makes a slow, gradual change in direction, as shown in the image. As a result of this gradual turn, the cross-sectional area the fluid is flowing through at point 'B' is less than the cross-sectional area it flows through at points 'A' and 'C'. Written as an equation, $A_{csB} < A_{csA} = A_{csC}$, where the $_{csA}$ stands for 'control surface $A$' subscript  

The term 'vena contracta' describes the phenomenon of contracting flow due to streamlines being unable to make sharp turns. $\Pi_{vc}$ is a ratio between the flow area at the vena contracta, $A_{csB}$, which is when the flow is *maximally* contracted, and the flow area *before* the contraction, $A_{csA}$. In the image above, the equation for the vena contracta coefficient would be:

$$\Pi_{vc} = \frac{A_{csB}}{A_{csA}}$$  

Note that what this class calls $\Pi_{vc}$ is often referred to as a 'Coefficient of Contraction,' $C_c$, in other engineering courses and settings. When the most extreme turn a streamline must make is 90°, the value of the vena contracta coefficient is close to 0.62. This parameter is in aide_design as `pc.RATIO_VC_ORIFICE`. The vena contracta coefficient value is a function of the flow geometry.

_**A vena contracta coefficient is not a minor loss coefficient.**_ Though the equations for the two both involve contracted and non-contracted areas, these coefficients are not the same. Refer to the flow through a pipe elbow image above. The minor loss coefficient equation uses the areas of points 'B' and 'C,' while the vena contracta coefficient uses the areas of points 'A' and 'B.' Additionally, the equations to calculate the coefficients themselves are not the same. Confusing the two coefficients is common mistake that this paragraph will hopefully help you to avoid.


### Origin
The orifice equation is derived from the Bernoulli equation as applied to the red points in the following image:

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Hole_in_a_bucket.jpg?raw=true" width=350></center>

At point A, the pressure is atmospheric and the instantaneous velocity is negligible as the water level in the bucket drops slowly. At point B, the pressure is also atmospheric. We define the difference in elevations between the two points, $z_A - z_B$, to be $\Delta h$. With these simplifications ($p_A = \bar v_A = p_B = 0$) and assumptions ($z_A - z_B = \Delta h$), the Bernoulli equation becomes:

$$\Delta h = \frac{\bar v_B^2}{2g}$$

Substituting the continuity equation $Q = \bar v A$ in the form of $\bar v_B^2 = \frac{Q^2}{A_{vc}^2}$, the vena contracta coefficient in the form of $A_{vc} = \Pi_{vc} A_{or}$ yields:

$$\Delta h = \frac{Q^2}{2g \Pi_{vc}^2 A_{or}^2}$$

Which, rearranged to solve for Q gives **The Orifice Equation:**

$$Q = \Pi_{vc} A_{or} \sqrt{2g\Delta h}$$

Such that:  
$\Pi_{vc}$ = 0.62 = vena contracta coefficient, in aide_design as `pc.RATIO_VC_ORIFICE`  
$A_{or}$ = orifice area- NOT contracted flow area  
$\Delta h$ = elevation difference between orifice and water level

**Equations in aide_design:**  
`pc.flow_orifice(Diam, Height, RatioVCOrifice)` Returns flow through a horizontal orifice.  
`pc.flow_orifice_vert(Diam, Height, RatioVCOrifice)` Returns flow through a vertical orifice. The height parameter refers to height above the center of the orifice.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Fluids%20Review/Images/Vertical_and_Horizontal_Orifices.jpg?raw=true" width=500></center>

There are two configurations for an orifice in the wall of a reservoir of water, horizontal and vertical, as the image above shows. The orifice equation shown in the previous section is for a horizontal orifice, but for a vertical orifice the equation requires integration to return the correct flow. You will explore this in the Flow Control and Measurement Design Challenge.

## Section Summary
1. **Bernoulli vs energy equations:** The Bernoulli equation assumes that energy is conserved throughout a streamline or control volume. The Energy equation assumes that there is energy loss, or head loss $h_L$. This head loss is composed of major losses, $h_{\rm{f}}$, and minor losses, $h_e$.

Bernoulli equation:
$$\frac{p_1}{\rho g} + {z_1} + \frac{\bar v_1^2}{2g} = \frac{p_2}{\rho g} + {z_2} + \frac{\bar v_2^2}{2g}$$

Energy equation, simplified to remove pumps, turbines, and $\alpha$ factors:
$$\frac{p_{1}}{\rho g} + z_{1} + \frac{\bar v_{1}^2}{2g} = \frac{p_{2}}{\rho g} + z_{2} + \frac{\bar v_{2}^2}{2g} + h_L$$

2. **Major losses:** Defined as the energy loss due to shear between the walls of the pipe/flow conduit and the fluid. The Darcy-Weisbach equation is used to find major losses in both laminar and turbulent flow regimes. The equation for finding the Darcy friction factor, $\rm{f}$, changes depending on whether the flow is laminar or turbulent. The Moody diagram is a common graphical method for finding $\rm{f}$. During laminar flow, the Hagen-Poiseuille equation, which is just a combination of Darcy-Weisbach, Reynolds number, and ${\rm{f}} = \frac{64}{\rm{Re}}$, can be used

Darcy-Weisbach equation:  
$$h_{\rm{f}} = {\rm{f}} \frac{L}{D} \frac{\bar v^2}{2g}$$
For water treatment plant design we tend to use plant flow rate, Q, as our master variable and thus we have.
$$h_{\rm{f}} = {\rm{f}} \frac{8}{g \pi^2} \frac{LQ^2}{D^5}$$

$\rm{f}$ for laminar flow:

$${\rm{f}} = \frac{64}{\rm{Re}} = \frac{16 \pi D \nu}{Q} = \frac{64 \nu}{\bar v D}$$

$\rm{f}$ for turbulent flow:

$${\rm{f}} = \frac{0.25} {\left[ \log \left( \frac{\epsilon }{3.7D} + \frac{5.74}{{\rm Re}^{0.9}} \right) \right]^2}$$

Hagen-Poiseuille equation for laminar flow:
$$h_{\rm{f}} = \frac{32\mu L \bar v}{\rho gD^2} = \frac{128\mu Q}{\rho g\pi D^4}$$

3. **Minor losses:** Defined as the energy loss due to the generation of turbulent eddies when flow expands. Once more: minor losses are caused by flow expansions. There are three forms of the minor loss equation, two of which look the same but use different coefficients ($K_e^{'}$ vs $K_e$) and velocities ($\bar v_{in}$ vs $\bar v_{out}$). _Make sure the coefficient you select is consistent with the velocity you use_.

First form:
$$h_e = \frac{\left( \bar v_{in}  - \bar v_{out} \right)^2}{2g}$$

Second form:
$$h_e = \frac{\bar v_{in}^2}{2g}{\left( {1 - \frac{A_{in}}{A_{out}}} \right)^2} = \,\,\, \frac{\bar v_{in}^2}{2g} \mathbf{K_e^{'}}$$

Third and most common form:
$$h_e = \frac{\bar v_{out}^2}{2g}{\left( {\frac{A_{out}}{A_{in}}} -1 \right)^2} = \,\,\,\, \frac{\bar v_{out}^2}{2g} \mathbf{K_e}$$


4. **Major and minor losses vary with flow:** While it is generally important to know how increasing or decreasing flow will affect head loss, it is even more important for this class to understand exactly how flow will affect head loss. As the table below shows, head loss will always be proportional to flow squared during turbulent flow. During laminar flow, however, the exponent on $Q$ will be between 1 and 2 depending on the proportion of major to minor losses.

| Head loss scales with: | Major Losses | Minor Losses |
|:----------------------:|:------------:|:------------:|
|        Laminar         |     $Q$      |    $Q^2$     |
|       Turbulent        |    $Q^2$     |    $Q^2$     |


5. The **head loss trick**, also called the control volume trick, can be used to incorporate the 'kinetic energy out' term of the energy equation, $\frac{\bar v_2^2}{2g}$, into head loss as a minor loss with $K_e = 1$, so the minor loss equation becomes $\left( 1 + \sum K_e \right) \frac{\bar v^2}{2g}$. This is used to be able to say that $\Delta z = h_L$ and makes many equation simplifications possible in the future.

6. **Orifice equation and vena contractas:** The orifice equation is used to determine the flow out of an orifice given the elevation of water above the orifice. This equation introduces the concept of a vena contracta, which describes flow contraction due to the inability of streamlines to make sharp turns. The equation shows that the flow out of an orifice is proportional to the square root of the driving head, $Q \propto \sqrt{\Delta h}$. Depending on the orientation of the orifice, vertical (like a hole in the side of a bucket) or horizontal (like a hole in the bottom of a bucket), a different equation in aide_design should be used.

The Orifice Equation:
$$Q = \Pi_{vc} A_{or} \sqrt{2g\Delta h}$$
