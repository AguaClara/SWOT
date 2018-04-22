

```python
from aide_design.play import*
from aide_design import floc_model as floc
from pytexit import py2tex
```

# Applications of Fusion 360 for Automated Sedimentation Tank Design

Matthew Cimni, Chris Galantino, Ben Gassaway 
CEE Fall 2017 Final Capstone Design


# I. Introduction

In order to grow as quickly as possible, AguaClara has focused on building tools to help future designs of plants. These tools will automatically generate schematics of entire water filtration plants that adjust with given dimensions associated with a specific location. In order to improve the automated design process of AguaClara, the team began to transition away from old and outdated softwares, such as MathCAD, in the summer of 2017. One of the new softwares that Automated Infrastructure Design Engine (AIDE) will rely heavily on is Fusion 360, a program that AguaClara has no previous experience with. 

The goal of this team is to build a working, parameterized model of a sample sedimentation tank that may serve as a module for an entire plant's design to reference and manipulate accordingly. 

The first focus of the team was on the body of the sedimentation tank, as opposed to the channels on the outside. This is because these channels stretch across multiple tanks and are to be created as a separate template. This plant should be as detailed as possible and possess all functional components of a real sedimentation tank. These components should be able to change given an input of parameters and still work within an acceptable range of values. Fusion 360 is able to provide this flexibility.

The following hyperlink is the current model of the sedimentation tank developed by the team: http://a360.co/2B2z8dn


### Detailed Plan

The team will need a plan of various steps to complete by the end of the semester.
1. Consult others
 - There are other sources already tackling a similar problem and it will most likely prove useful to see what they know
 - Such resources include Ethan Keller (an AguaClara alum working as a field engineer in Honduras) and the AIDE Draw team.
2. Investigation of Sedimentation tank
 - The team must determine all of the criteria and components that go into making a sedimentation tank
 - By performing this essential step, the team is given a solid base for modeling in Fusion 360
3. Mastery of Fusion 360
  - In order to properly build a plant in Fusion, all team members will have to understand the software in all necessary areas
  - Important topics
  - Sketching
  - Dimensioning
  - Jointing
  - Parameterization
  - Ability to read data from external files
4. Building a standard model
  - This model will be the base for all future parameterized designs
  - It should have all components and pieces of a finalized design
  - The team will note whenever they put in a global parameter as opposed to one that is arbitrarily decided to serve as a filler until a parametrized method can be implemented.
5. Generalizing model 
  - Start to replace hard coded dimensions with data read from input files
  - Test whether or not given values accurately reflect dimensions in the plant

# II. Methods


### Approach to the Problem

The team intends to keep a similar approach as to the one laid out in the Detailed plan. Each member had to learn how to utilize Fusion 360 before the team could break out and model different parts of the sedimentation tank. This was accomplished through Ethan's AIDE tutorial on drawing AIDE templates and individual practice.

In between practising Fusion at home, the team works on figuring out the necessary dimensions needed to construct the first iteration of the 3D model. Fletcher has provided the team with AIDE's list of parameters that they have been basing their initial drawings on. This acts as a starting point for the team's build.

The team's general approach to the project was to develop a working model of the sedimentation tank in Fusion 360 to have visual context of the important geometry variables to be defined by either a user input or to be derived through an equation. From there, the team worked to complete a full glossary of parameters and equations that will be used to construct the full sedimentation tank. The team hopes to construct both a modular and a scalable sedimentation tank that may be used in a variety of plant sizes.

### List of Parameters

An important step to building the tank is the parameters of that will remain constant and which will have to be user input. The team created an Excel document outlining all the variables.
![](pi.jpg)

A hyperlink to the full Excel document can be found here: 

https://docs.google.com/a/cornell.edu/spreadsheets/d/1NyninGh-faCT_wgxtSdTaa9DOUzARAFkxYG6JBnjg5k/edit?usp=sharing

This document serves as a shared sheet that all team members can add to in order to cross reference expert inputs and variables. In this way, team members are able to see what values affect others and where parameters still need to be defined. 

The parameters used to define sedimentation tank design in Fusion 360 were derived through a variety of equations as presented in CEE 4540 lectures, through Aide Design's glossary of terms, and other archived AguaClara parameters. The team has distinguished between relevant parameters by organizing them in the following regard:

    1. Flows
    2. Sedimentation Tank
    3. Floc Hopper
    4. Reverser
    5. Diffuser
    6. Inlet Manifold
    7. Outlet Manifold (Launder)
    8. Plate Settlers
    9. Plate Settler Module
    
Intitial construction of the sedimentation tank design was established based on rough estimates of the tank's geometry guided by plant flow, upflow velocity, and capture velocity constraints. Once a working model was made, the estimated values were corrected through alignment with Aide Design's variable definitions relevant to the 20 L/s flow rate. Many variables are consitituently dependent upon user inputs and other equations that cascade through variable definitions. In a way, the 20 L/s values provide a sort of sanity check as we continue to develop the parametrized model.

The plate settlers are not individually placed and standalone, but rather produced in pre-set modules held together by spacers and internal piping. Therefore, the team needs to look into designing these parametrized modules of a set number of settlers and tie this in to the Python calculation of plate settler requirements and Fusion designation. 

Of course, there are potential minute details perhaps overlooked in the list of parameters the team is currently investigating. As the project's development continues to unfold, these facets will be acknowledged and incorporated into the final, fine-tuned product.  

### Use of AutoCAD

The dimensions for building a sedimentation have already been calculated and used to design models built into AutoCAD. The team intends on using these files' dimensions to ensure that the dimensions for the Fusion 360 model will be correct.

What is important to note is that there already exists a Fusion 360 CADed model for a sedimentation tank with detailed piping, plate settlers, depths, diameters, widths, and so on. However, the model was imported directly from its original AutoCAD file and is composed of a conglomeration of bodies specifically placed in their respective positions in order to represent the overall sedimentation tank. Although the components are to scale, none of them are in communication with eachother and therefore the model cannot simply be "scaled up" to size. Fusion 360 will serve to recreate this design, but by creating a smart model where items are in conversation with one another.

Aside from guiding the team in component proximity and location, the AutoCAD model helps the team determine the ratios of item placement for components not necessarily requiring iteration. For example, the pipes that connect plate settlers into a plate settler module are inserted at a region of the plate settler relative to the length. By analyzing the distances on the "dummy" Fusion model, an appropriate ratio may be applied to any plate settler module for any given capture velocity and upflow velocity. Measurements where this is not applicable include optimal holes for the inlet manifold or the number of plates that will fit in a sedimentation tank.

This approach mimics the modeling process currently used by the AIDE Draw team for the Chemical Dose Controller (CDC).



### Referencing Variables and Geometry
The team can incorporate variables into a working Fusion model once they have established a consistent basis for variable naming. This Fusion model will provide more utility than the current AutoCAD models; they have assemblies that reference other parts and are not purely placed by location with no regard to components surrounding it. The most important part of these Fusion models is keeping everything referenced to as few variables as possible. Just as previously stated, when finishing equations for parameters everything about the 3D model should be defined by what is put into it. For example, this can be seen in the plan view of the concrete tank of the sedimentation tank.

![](plan view tank.jpg )


As can be seen in the picture, above all of the dimensions there is the fx: prefix, indicating that these are parameter driven dimensions. So the width of the sketched rectangle is determined by the equation (SedTank_ActiveLength + 2 * SedTank_ThicknessDividingWall). Some other driven dimensions are determined by geometric properties. The channel in the middle that houses the jet reverser is one of these cases, where it moves position based on where the center line is.

This non-static method of CADing allows AIDE to create various dimensioned plants without having to individually create components every time.


### Fusion Models
The core components that make up the sedimentation tank consist of:

The Tank (SedTank):
![](Tank.jpg )

The Inlet Manifold (InletMan):
![](inlet man.jpg )

The Outlet Manifold (OutletMan):
![](outlet man.jpg )

The Diffuser (Diffuser):
![](diffuser.jpg )

The Plate Settler (PlateSettlers):
![](plate settler.jpg)

The Plate Settler Module (Module):
![](Module.jpg)

The Jet Reverser (Reverser):
![](Reverser.jpg)

### Use of the Shared Component Library
The sedimentation tank is also comprised of several pipes that are standard hardware. These are used in the support for the plate settlers, connection to the channels, as well as making plate settler units. The pipes that go into making these structures have already been CADed and can be found in a central library. These components will be used in the final assembly.

### Major Challenges and Constraints

The biggest hurdle that the seem will need to get over has to do with AguaClara subteam's inexperience with Fusion 360. Because the team does not know every single in and out of the software, it may prove difficult to do a project that requires a bit of out-of-the-box thinking. 

Building a parameterized model without being able to read parameters is a big challenge that we will have to continually think about when starting the first few sketches. It is possible that we will have to redo some of our work if it is discovered that geometry needs to be defined in a more relationed manner rather than hard coded.

Another major challenge to be addressed in this design are inconsistencies in naming conventions for system variables. This has made the transition from AIDE Design's parameter definitions into Fusion 360 a difficult matter. Communication with the Aide team has helped with these uncertainties. For future parameter glossaries, extensive variable descriptions in a note column would likely bring tremendous value.

The outlet manifold and overall height of the sedimentation tank have presented the most difficulty in parametrization of the model. The AguaClara literature on Confluence does not have explicit descriptors or sometimes lacks clarity on certain variables (lack of image) to address all aspects of the component's geometry. This includes water level height, plant freeboard, outlet manifold headloss, etc. Since the 4540 cirriculum does not put emphasis on the design of the outlet manifold and ultimate sedimentation tank height, understanding the relationships between upflow velocity, tank flow rate, and the desired intake rate of each hole in the outlet manifold is key to reducing user entered values. The team hopes to define these variables soon once they get in contact with Ethan and the AIDE team. Primary objectives in parameterization are first to define all relevant parameters while simultaneously bridging the gaps of information between teams to build a unified glossary of parameters.


# III. Results and Analysis

In order to organize the parametrization process, the team needed to break up inputs and variables into four different sections: Global, User, Python, and Fusion. 


Global includes values for items that are consistent throughout fluid mechanics, general plant design procedure, and expert inputs. User includes inputs that the person requesting designs is prompted to enter depending on their given situation. User inputs will eventually be incorporated into a revamped Graphic User Interface (GUI) for easy interaction. Python includes variables which are determined utilizing the Global and User inputs before sending information to Fusion 360. The method in which Fusion 360 reads Python output is yet to be determined.

Minimizing the amount of inputs and variables destined to be used by Fusion 360 is essential to the overall efficiency of the process. Fusion is strictly geometric, so relating flow rates and headlosses within Python and presenting desired measurements along with user and global inputs allows easy iteration and a dynamic model. 

Below is an example of how the height of the sedimentation tank is generated through interactions between global values, user inputs, python outputs, and Fusion generation.

![](SedTank.jpg )

![](SedTank frontal.jpg )

## Global

**Plant Characteristics**

 1. Upflow Velocity
     - *V_upflow*: 1.01 mm/s
 2. Capture Velocity
     - *V_capture*: 110 microm/s

**The Tank (SedTank)**
     
 1. Height of Free board
    - *SedTank_FreeBoard*: 10 cm
 2. Width of sedimentation
    - *SedTank_ActiveWidth*: 42 inches
 3. Angle of Bottom
    - *SedTank_AngleBot*: 50 degrees
 4. Thickness of underlying concrete slab
    - *SedTank_ThicknessBot*: 15 cm
 5. Width of Inlet Channel
    - *SedTank_Inlet* 
 6. Width of Exit Channel
    - *SedTank_Exit*
 7. Height of Between zone (distance from floc weir shelf to bottom of lamella)
    - *SedTank_Between*: 15 cm
 8. Height between top of settlers and bottom of launder
    - *SedTank_OutletManHeight*: 5 cm
    
**The Inlet Manifold (InletMan)**

 1. Hole of Inlet Manifold Spacing
    - *InletMan_SpacingHole*
 2. SDR of Inlet Manifold
    - *InletMan_SDR*: 26
 3. Max Length of Sed Upflow
    - *SedTank_MaxUpflowLength*: 5.8 m

**The Outlet Manifold (OutletMan)**

 1. Headloss of Outlet Manifold
    - *OutletMan_Headloss*: 5 cm
 2. Spacing of Outlet Manifold Holes
    - *OutletMan_SpacingHole*: 10 cm
 3. SDR of Outlet Manifold 
    - *OutletMan_SDR*
    
**The Diffuser (Diffuser)**

 1. Diameter of Diffuser Pipe
    - *Diffuser_OD*
 2. Diffuser Spacing
    - *Diffuser_Spacing*: 6 cm
 3. Width of Diffuser Opening
    - *Diffuser_WidthOpening*: 3.17 mm
 4. Length of Diffuser Opening
    - *Diffuser_LengthOpening*
 5. Length of Diffuser
    - *Diffuser_Length*: 15 cm
 6. SDR of Diffuser
    - *Diffuser_SDR*: 26
 7. Outer Length of Diffuser Opening
    - *Diffuser_OuterOpeningLength*
 8. Inner Length of Diffuser Opening
    - *Diffuser_InnerOpeningLength*
 
**The Plate Settler (PlateSettlers)**

 1. Angle of Plate Settlers
    - *PlateSettlers_Angle*: 60 degrees
 2. Width of Plate Settlers
    - *PlateSettlers_Width*: 1.06 m
 3. Perpendicular Spacing of Settlers (S)
    - *PlateSettlers_S*: 2.5 cm
 4. Thickness of Plate Settlers
    - *PlateSettlers_Thickness*: 2.0 mm
 5. Plate Settler Frame nominal diam
    - *PlateSettlers_NDFrame*
 
**The Plate Settler Module (Module)**

 1. SDR plate settler spacer
    - *Module_SDRSpacer*: 17
 2. Number of plates per module
    - *Module_PlateNumber*: 11

**The Jet Reverser (Reverser)**

 1. Diameter of Bottom Reverser
    - *Reverser_OD*
 2. SDR of Reverser
    - *Reverser_SDR*: 26

## User


**Plant Characteristics**

 1. Flow Rate
    - *Q_tank*: 20 L/s
    
    (*Important to note that the flow rate is set to 20 L/s for the sake of simplicity, but the flow rate is subject to change on a case-by-case basis for each plant. The flow rate will be uniquely optimized following plant calculations.*)
    
**The Tank (SedTank)**

 1. Thickness of Dividing Wall
    - *SedTank_ThicknessDividingWall*
 2. Thickness of Channel Wall
    - *SedTank_ThicknessChannelWall*
 3. Thickness of front/back wall
    - *SedTank_ThicknessFace*
 4. Height of vertical section of floc blanket (peak of slope to weir
    - *SedTank_FlocHeight*

## Python

**The Tank (SedTank):**
    
1. Length of Sedimentation Zone  $$SedTank_{SedLength} = \frac{Q_{tank}}{(V_{upflow})(SedTank_{ActiveWidth)}}$$

**The Inlet Manifold (InletMan):**

1. Max Inlet Manifold Flow $$InletMan_{FlowMax} = (SedTank_{SedLength})(V_{upflow})(SedTank_{ActiveWidth})$$
2. Max Inlet Manifold Velocity $$InletMan_{VelMax} = Diffuser_{Velocity}\sqrt{\left(\frac{2(1-InletMan_{PiFlow}^2)}{InletMan_{PiFlow}^2+1}\right)}$$
3. Diameter of Inlet Manifold $$InletMan_{ODPipe} = pc.diam_{circle}\left(\frac{InletMan_{FlowMax}}{InletMan_{VelMax}}\right)$$

**The Outlet Manifold (OutletMan):**

1. Diameter of Outlet Manifold (OutletMan_ODPipe) - unfinished

2. Orifice Diameter of Outlet Manifold (OutletMan_ODHole) - unfinished

**The Diffuser (Diffuser):**

1. Headloss of Sedimentation Tank Inlet (Headloss_Inlet) - unfinished

2. Diffuser Max Flow $$Diffuser_{FlowMax} = (V_{upflow})(SedTank_{ActiveWidth})(Diffuser_{Spacing})$$
3. Diffuser Velocity $$Diffuser_{Velocity} = \frac{Diffuser_{FlowMax}}{(Diffuser_{WidthOpening})(Diffuser_{LengthOpening})}$$

**The Plate Settler (PlateSettlers):**

1. Horizontal Spacing of Plate Settlers (Center to Center) $$PlateSettlers_{BH} = \frac{PlateSettlers_{S}+PlateSettlers_{Thickness}}{sin(PlateSettlers_{Angle})}$$


2. Length of Plate Settlers $$PlateSettlers_{Length} = \frac{(PlateSettlers_{S})((\frac{V_{upflow}}{V_{capture}}-1)+(PlateSettlers_{Thickness})(\frac{V_{upflow}}{V_{capture}})}{sin(PlateSettlers_{Angle}(cos(PlateSettlers_{Angle}}$$

3. OD of Plate Settler Frame Piping $$PlateSettlers_{ODFrame} = pipe.OD(PlateSettlers_{NDFrame})$$
4. Floc Blanket Top Area $$FlocBlanket_{TopArea} = \frac{Q_{tank}}{V_{upflow}}$$
5. Floc Blanket Length $$FlocBlanket_{Length} = \frac{FlocBlanket_{TopArea}}{SedTank_{ActiveWidth}}$$
6. Inactive Sedimentation Tank Length $$SedTank_{InactiveLength} = PlateSettlers_{Length}cos(PlateSettlers_{Angle})$$
7. Active Sedimentation Length $$SedTank_{ActiveLength} = FlocBlanket_{Length} - SedTank_{InactiveLength}$$
8. Height of Sedimentation Plate zone $$PlateSettlers_{Height} = PlateSettlers_{Length}sin(PlateSettlers_{Angle})$$

**The Plate Settler Module (Module):**

1. Python not needed for Plate Settler Module

**The Jet Reverser (Reverser):**

1. Diameter of Bottom Reverser $$Reverser_{OD} = pipe.OD(Reverser_{ND})$$

## Fusion

**The Tank (SedTank):**

1. Height of Sedimentation Tank $$SedTank_{WallHeight} = SedTank_{ThicknessBot}+\frac{1}{2}Reverser_{OD}+SedTank_{SlopeHeight}+SedTank_{FlocHeight}+SedTank_{Between}+PlateSettlers_{Height}+SedTank_{OutletManHeight}+OutletMan_{ODPipe}+OutletMan_{Headloss}+SedTank_{FreeBoard}$$

**The Inlet Manifold (InletMan)**

1. Length of Inlet Manifold - in progress $$InletMan_{Length}$$ 
2. Number of Holes in Inlet Manifold $$InletMan_{NumHoles} = floor\left(\frac{InletMan_{Length}}{Diffuser_{Spacing}}\right)-1$$


**The Outlet Manifold (OutletMan):**

1. Length of Outlet Manifold $$OutletMan_{Length} = SedTank_{Length} - 2(SedTank_{Inlet}) - SedTank_{ThicknessChannelWall}$$
2. Number of Holes in Outlet Manifold $$OutletMan_{NumHoles} = floor\left(\frac{OutletMan_{Length}}{OutletMan_{SpacingHole}}\right)-1$$

**The Diffuser (Diffuser):**

1. Fusion not needed for Plate Settler Module

**The Plate Settler (PlateSettlers):**

1. Number of Plate Settlers $$PlateSettlers_{Number} = \frac{SedTank_{ActiveLength}}{PlateSettlers_{BH}}$$
2. Width of Plate Settlers $$PlateSettlers_{Width} = SedTank_{ActiveWidth}$$

**The Plate Settler Module (Module):**

1. Starting Distance of 1st Module $$PlateSettlers_{Start} = PlateSettlers_{Length}cos(PlateSettlers_{angle})$$
2. Plate Settler Module Spacer Thickness $$Module_{SpacerThickness} = PlateSettlers_{S}$$
3. Number of Modules in the Sedimentation Tank $$Module_{Total} = \frac{PlateSettlers_{Number}}{Module_{PlateNumber}}$$
4. Length of Module Support Pipe $$Module_Tube = Module_{PlateNumber}(PlateSettlers_{S}+PlateSettlers_{Thickness})$$

and more work to be done

**The Jet Reverser (Reverser):**

Length of Bottom Reverser $$Reverser_{Length} = FlocBlanket_{Length}$$

# Conclusions

Throughout this project the team learned many aspects about the process of building a fully parameterized model. So many components inside the sedimentation tank must move or adjust depending on the change of single variable. This fact makes it difficult to reliably update such a complex system. However, through lots of iteration the current sedimentation tank assembly is ultimately able to handle a wide array of user inputs without rebuilding an entire model.

This advancement in flexibility should significantly improve future experiences of AIDE users and designers. Without the hassle of individually placing components into the appropriate x, y, and z locations, engineers can more easily modify subcomponents of the larger system. They will be able to freely change lengths, widths, or diameters without worrying about redefining locations of many different, mostly unrelated objects.


# Future Work

Future iterations of equations will still need to focus on the outlet manifold and length of sedimentation tank. The use of plate settler modules makes this dimension difficult to find and will need something more complicated than simple patterning. In addition to modfying some exisiting equations future teams will have to add more elements of the sedimentationt tank. This includes the floc hopper, piping, and entrance channel. The entrace channel is another interersting challenge becuase it must connect several copies of the same sedimentation tank.

# Additional Content

### Comments
I'd suggest building a simple drawing that includes the ability to scale and reviewing that with Ethan before even beginning to draw the sedimentation tank.You want to make sure that you understand the important steps in defining the sedimentation tank template drawing before you begin creating it because it is possible that the parametric scaling will require particular approach to creating the template.

### Responses to comments

We  agree that keeping in mind the idea that all the dimensions may have to be formatted in a specific manner is important. It is much better to do this early on if we discover that every dimension will have to be changed. 

Even if some dimensions will have to be changed later for global to user, we believe the parametric scaling will be fairly easy to implement because many features of the sedimentation tank are consistent throughout the various plant sizes. This means that many of the dimensions can be hard coded and will not need to be variable.

### Summary of Meeting with AguaClara AIDE Draw Team

Draw team is trying to accomplish a very similar goal to our team, although they are focusing on the CDC. They have not been able to find a way to take in inputs from external files yet. 

The Draw team suggested to focus on making a modeled version of the sedimentation tank without worrying too much about the parameterization since it is unclear how that will happen yet.
