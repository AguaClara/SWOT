# Logbook for Spring 2018 CEE 4540 Updates

This file will contain weekly updates into my work. All changes will be pushed to a non-master branch, and I will only have one branch at a time for whatever project I am working on. Every week (the day depends on my work schedule that week), I will send Monroe an email containing a link to this file's page on GitHub in addition to supplementary material. For example, this first week I will send him the example of the 'extra' slides for his viewing pleasure (or displeasure).

***
## List of Big Ideas and Big Concerns
1. It is not ideal to have both a confluence and a GitHub page that contain course resources. This will confuse students very much, they will be unable to find or unwilling to look for the simple things, and they will pester the TAs.  
**¡DONE! Ambitious idea: Move everything to GitHub ¡DONE!**  
Confluence, in all its glory, is not well liked by students and has a tendency to get very messy. Despite the fact that it seems like the perfect tool, I've only every heard complaints from students, both in AguaClara and 4540. Documents and information are oftentimes difficult to find
    - Is it possible to make a good looking syllabus on GitHub? Will investigate. Shouldn't be too difficult with table functionality in markdown
2.

***

## First Progress Report: Arrived in Argentina 2/7/18

### Done
1. Installed and played with atom until comfortable
1. Looked into how to handle extra slides, input from Cynthia and Zoe. Small example ready
1. Simplified a few slides- notably one on Darcy-Weisbach
1. Began to transfer equations in the powerpoints to LaTeX from MathType
    - `Flow Control and Measurement` and  `Rapid Mix` are done and uploaded to my branch.
    - Looked into changing the LaTeX math font, as I like the MathType font far more. I wasn't able to find any good options in a couple hours of searching
    - I've only got 14 more days left of MathType

### To Do
1. Finish transferring all equations to IguanaTeX before MathType runs out
1. Once all equations are transferred, branch point (my preference bolded):
    - **Update/simplify/clarify slides,** OR
    - Begin to create summary sheets for each unit process/course topic OR
    - Look into skeleton structure for textbook (equation numbering and citations)

***

## Second Progress Report: Last day in Argentina 2/14/18

### Done
1. Completed transferring equations to LaTeX from MathType in `Flocculation Model`. Took more time than the previous topics due to its heaftier equation volume and the following bullet.
1. Began to understand the huge difficulty with work-life-family balance. As I work and my grandpa just looks at me somewhat sadly. Short-term productivity suffered.

### To Do
1. Finish transferring equations for `Flocculation Design`, `Sedimentation`, and `Filtration` powerpoints, along with the scattered extras.
    - `Sedimentation` and `Filtration` powerpoints don't appear to be in the `CEE_4540` repo. I'll take them from the 4540 syllabus. I imagine Monroe didn't change them too much since last semester.
    - I will need to purchase Mathtype, or download another free trial. I can use another email and wipe Mathtype from my computer before re-installing? I'll try that
1. Look into changing the font color on IguanaTeX. Learn more about LaTeX and IguanaTeX in general.

***

## Third Progress Report: 3 productive days in Abu Dhabi 2/21/18

### Done
1. Figured out how to add color to the IguanaTeX equations. Not too tough, but it took longer than I would have liked.
1. Finished transferring equations for:
    - `Flocculation Model`
    - `Flocculator Extras`
    - `Sedimentation`
    - `Filtration`
    - `Disinfection`
    - `Disinfection Extras`
    - `Prelim 1 Review`
    - `Prelim 2 Review`
    - Presentations that haven't been transferred to LaTeX: `Sedimentation Extras`, `Filtration Extras`, `Open Channel Flow`, `Manifolds`, and `Floc Blanket Model`, which is just a collection of slides from the Flocculation slides.
    - MathType ran out :( but I finished everything I intended to and more :D
1. Went back and labeled all the equations that were off the slides for future clarity
1. Reorganized the `Lectures` folder in GitHub. I think it is a lot more clear now.
1. Beginning to edit presentations for clarity while reformatting the extra slides. Extra slides will now be a separate powerpoint.
Extra slides finished for:
    - `Introduction`
1. Created functional "Overviews" for the following presentations:
    - `State of the planet`
    - `AguaClara Slideshow`
    - `Flow Control and Measurement`
    - `Introduction` halfway done- does it make sense to have such structure for the non-technical presentations?




### To-Do
1. Continue to edit and clarify technical presentations. This will take a long time. I will begin sequentially, with `Flow Control and Measurement`.
1. Talk to Monroe about the `Drinking Water Contaminants` presentation structure

<div class="alert alert-block alert-info">

**Non-imminent action item for Monroe**
<br>
Please go back over the non-physics/math/engineering presentations to make sure that they are of adequate length. Those presentations are, in a way, the most important ones of the course, as they inspire people. Their delivery should not be rushed. If some slides have to become 'extras' to ensure that each remaining slide is given the time and gravity it deserves, that's ok.

<br>

For the following presentations, let me know what slides you want to be considered extras, if any. You can simply add/remove the oh-so-common `extra` tag to them and push them to GitHub (once you've pulled my changes! I've made some minor edits to the non-technical presentations), I'll create the extra slide decks for them. I imagine you have a way better feel for how long the presentations should be than I do!
- `State of the planet`
- `Drinking Water Contaminants`
- `AguaClara Slideshow`
- `Public Health`
- `Last Lecture`
</div>

***
## Fourth Progress Report: Return from Japan, beginning of long-term, stable working period! 4/5/2018

### Done
1. Began `Flow Control and Measurement.md` cheat sheet. There are many, many ways of writing a guide. The more eyes that look at this and offer advice, the better. I'm planning on sending it out to many people to (hopefully) look at it and offer advice on what is good, what is bad, and what could be different.
    - This is a significant project!
2. Made consistent Bernoulli/energy equation variables in slides ($\rho g$ vs $\gamma$, $v$ vs $V$)
3. Continuing to clarify the `Flow Control and Measurement` powerpoint.

### To Do, all in `Flow Control and Measurement.md`
1. Find a good site to link to 'head'.
2. Find the 'AguaClara standard unit convention' that's floating around somewhere and add it to the introduction.
3. Figure out how to get markdown in atom to download/read the \cancel package in MikTex for math.
4. Include control volumes into the streamline assumption of the Bernoulli equation section
5. Solicit feedback from people on the cheat sheet.

***
## Fifth Progress Report: 4/12/2018
### Done
1. Finished first drafts of [minor loss equation derivation](https://github.com/AguaClara/CEE4540_DC/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Summary%20Sheets/Derivation_minor_loss_equation.md "Minor loss equation derivation document") and [flow through a simple hypochlorinator](https://github.com/AguaClara/CEE4540_DC/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Summary%20Sheets/Derivation_flow_through_simple_hypoclorinator.md).
2. Finished Fluids Review in `Flow Control and Measurement.md` summary sheet first draft. Sent it out to Fletcher and Clare to look over and provide feedback.
3. Edited `Flow Control and Measurement.pptx` slides up to slide 33. Eliminated derivations, removed clutter from slides. Will send out new version for review.

### To Do
1. Find a good site to link to 'head.'
2. Keep going. Review feedback from Fletcher and Clare when they respond. Begin on Section 2 'Introduction to Flow Control: The Search for Constant Head.'



***
## Sixth Progress Report: 4/17/2018  
This interim progress report is due to 2 factors. My family and I are going on vacation from the 18th until the 21st of April, and I will only be able to work a few hours on those days, if at all. On the 17th, the [Green Business Summit 2018](https://events.economist.com/events-conferences/emea/Greenbusinesssummit) is being held two blocks from where I live. I signed up and am going to learn about things and see if I can schmooze with  businessmen and pitch AguaClara. That is why this week will be light on work.

### Done
1. I need to be a bit more organized and broaden my scope to consider more than just the summary sheets at any given time. One day out of every week, I will zoom out of my current project, which will be summary sheets/powerpoints in the near future, and look at the general organization/structure of the class.
2. Is it a problem that we are presumably using the same repo to give subsequent years of students their DCs? Is it possible for them to checkout a previous commit to get the DC solutions from previous years?
    - I think that it is not a huge deal. There are so many ways to cheat in any class if a student tries hard enough. Most students won't have any prior knowledge of github anyways, and will be unlikely to even know this is possible.
3. I have checked out the possibility of moving everything from confluence to github. Not only is it possible, but it wouldn't even be that difficult. The only concern would be the locations of certain images and files, but that is not a legitimate reason not to do the switch. It would take me 10 hours MAX and probably a lot less. Organizing the file structure on github would be the only tricky part.
    - I have made the first line of the sample syllabus via a markdown table, you may find it [here](https://github.com/AguaClara/CEE4540_DC/blob/Flow_Control_and_Measurement_v2/Sample_Syllabus.md). The raw file is still a mess exactly like the confluence one, but I believe that is unavoidable. By expanding the atom window/shrinking the text size each row can take up one line, which makes the table begins to look normal and navigable.

### To Do
1. Umm... everything. Summary sheet making is a slow process if a quality product is desired. Which of course it is.
2. **Should I begin to make the switch from confluence to github?**



***
## Seventh Progress Report: 4/26/2018  
### Done  
1. Transfer from confluence to GitHub is more or less done (Thanks Monroe!). Anything else that was forgotten can be easily moved later on.
2. New repo structure has been established. [CEE4540_Master](https://github.com/AguaClara/CEE4540_Master) for class material, [CEE4540_DC_2018](https://github.com/AguaClara/CEE4540_DC_2018) for Design Challenges, and a separate, private repository for solutions.
3. Have advanced to the AguaClara tech section of Flow Control and Measurement summary sheet. Incorporated feedback from Clare and Fletcher.

### To Do
1. Finish the Flow Control and Measurement cheat sheet and powerpoint by the end of next week.
2. Re-evaluate my work priorities, considering time. Perhaps I should prioritize creating derivation sheets to remove derivations from powerpoints, and then spruce up the powerpoints before returning to the summary sheets. The summary sheets take a very, very long time to do well :/
I think that will greatly improve the chance that some things are completely done and what _is_ done is done very well by the beginning of the semester.



***
## Eigth Progress Report: 5/7/2018  
### Done  
1. Change image insertion from markdown style to html to allow for resizing- silly markdown
2. Added the head loss trick to fluids Review
3. Reorganized CEE4540_Master repo by chapter to make organizing a book easier and avoid enormous image folders.
4. Cleaned up the 4 intro powerpoints. Added clickable overviews to all of them and organized their extras.
5. Finished the FCM summary sheet, powerpoint, powerpoint extras, and derivations. Definitely, definitely need another pair of eyes or two, but I think it looks pretty good :D
6. Starting to look at rapid mix... oh boy

### To Do
1. Questions/confirmations for Monroe
    1. In [this minor loss equation derivation](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%201_Fluids%20Review/Derivation_minor_loss_equation.md), why is $p_{in}$ with $A_{out}$ instead of $A_{in}$?
    The control surface 1 is drawn in the fluid so that the only solid surfaces inside the control volume are normal to the two control surfaces. In the x direction the only forces on the solid surfaces are shear and that is negligible. The area of control surface 1 is the same as the area of control surface 2. The pressure on control surface 1 is assumed to be uniform (or hydrostatic).
    2. When [deriving the CDC equations](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Derivation_designing_the_cdc.md#designing-for-the-error-constraint-pi_error), why do you take the limit as Q approaches 0? Is that when the difference between the actual head loss and the linearized model is the greatest, percentage-wise?
    The error is zero at Max Q because we've calibrated at max flow rate. The ratio of actual flow/target flow is maximum as Q approaches zero.
    3. Revise step 6 in the [CDC design algorithm](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Summary_Sheet_Flow_Control_and_Measurement.md#how-it-works-2). I thought that Stock Concentration was set in the beginning? I can understand why it makes sense to set at the end, but everything document I've looked at does it at the beginning. High student-confusion-potential
    You are right. Remove stock concentration from the final step.
    4. In the powerpoint 'Drinking Water Contaminants,' what is the blue star in the corner of the slides supposed to represent? Extras? There are a lot of them.
    Great question. I'm not sure. It almost looks like the opposite of extras.
2. Should the flow control summary sheet include constant head devices?? If so, see the [TOO LONG](https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%202_Flow%20Control%20and%20Measurement/Summary_Sheet_TOOLONG_Flow_Control.md#22-constant-head-devices) version. Should these be included as is or changed? If they should be included as is, I think we need some more advantages and disadvantages.
The text should definitely include the constant head devices. Given that we don't use them in our designs it might not be necessary to have a summary sheet on them
3. I will now begin to make derivations sheets for flocculation/sedimentation/flocculation while clearing up the powerpoint slides that contain those derivations. Having looked at rapid mix, I think it now makes sense to communicate with Monroe on what should go in the intro vs the summary sheets for each unit processes. This would be best done with a voice/video call. Earliest possible date: May 11th.
I suggest putting all effort into the text book. There is some chance that the text will rapidly become the primary source of information and the lectures will become more discussion focused. I'm going to be exploring options for how to more effectively teach this material in the coming weeks.



***
## Ninth Progress Report: 5/15/2018  
### Done
1. Got to the end of Flocculation design. By no means finished, needs lots of polishing, reordering, rewriting, and all that.


### To Do
1. Questions for Monroe: Oh man I got lots
    1. What is our basis for using 37,000 as collision potential?

        - Tradition? This is approximately the value we have used for design for the past 8? years or so. We are also experimenting with a $G\theta$ of 20,000 for the 1 L/s plant. We are far from the ability to create an optimized design for a water treatment plant and thus this value will undoubtedly change. For now it is providing reasonable plant performance especially given that it is followed by a floc blanket.

    2. Baffle modules for flocculators: What are they called? Do they have a commonly used name?

        - We have to invent the nomenclature. As far as I know we invented baffle modules. Now is a great opportunity to name them.

       Potential names
        - Baffle modules
        - you idea here

    3. Where did the equations for $G$ and $\varepsilon$ come from? Without knowing how these came to be, I can't fully wrap my head around flocculation- $\bar G = \sqrt{ \frac{\bar \varepsilon}{\nu}}$ and $\bar \varepsilon = \frac{g h_L}{\theta}$

        - $\bar \varepsilon = \nu\bar G^2$  I don't know how to argue for this equation from first principles. See [this paper](https://www.tandfonline.com/doi/pdf/10.1080/19942060.2009.11015267) for the equation. This relationship is the basis of mechanical flocculator design. Perhaps this is best viewed as the definition of  $\bar G$. There would be more than one way to define an average for the velocity gradient and this is the simple definition that we use.
        - $\bar \varepsilon \theta = g h_L$ This states that the rate of conversion of mechanical energy to heat * the time over which that conversion is happening is equal to the total amount of mechanical energy that is converted.

    4. How thoroughly have we tested/confirmed that the minor loss coefficient of a baffle is 2.56? Do we have sources to cite? Do we have sources to cite for the VC being 0.384? [What you cited for that in a slide's comments](https://confluence.cornell.edu/display/AGUACLARA/Validation+Studies+for+ANSYS+Fluent+Turbulence+Model+Simulations) has been taken over by Michel Kors ads, somehow.

        - We have not yet been able to do a good measurement in the field to confirm this value. The measured head loss may very well be different than this value because of the complicated effect of the interactions between sequential flow expansions
        - Shulz and Okun give a wide range for this number. I don't know of a good reference. I invented the approach to estimate the vena contracta based on the angle of the change in flow direction. That has not been confirmed with experimentation.

    5. Where did we get the 'Jets expand in width at the rate of approximately 1 unit in width per 10 units forward' rule? How sure are we that the flow fully expands in our flocculators?  Based on the jet expansion rule, how does $\frac{H_e}{S} = 3$ allow for full jet expansion?   
    <img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%204_Flocculation/Images/I_need_some_clarity.JPG?raw=true" width=400>    

        -  b = 0.107 s where b is the jet width and s is the distance along the centerline of the jet. I've added a powerpoint on Jets & plumes into the "other and previous" lectures. This reference is on slide 16 and comes from course notes from Gerhart Jirka who studied jets and plumes at Cornell.
        - The flocculator design goal is to create uniform velocity gradients. Thus we don't want the flow to fully expand because at that point turbulence generation is over, energy dissipation falls off quickly, and velocity gradients decrease.
        - Thus we want to avoid high $\frac{H_e}{S}$ values. We estimate full expansion by $\frac{H_e}{S}$ of 6. We also need a range of acceptable values of $\frac{H_e}{S}$ because our tank depth is set by other constraints and thus we can't specify an exact value of $\frac{H_e}{S}$. It turns out that we need a range that is over a factor of 2 so that we can go from 1 flow expansion to 2 flow expansions per flocculator depth (and 2 is 2*1!).

    6. AguaClara flocculators have a Max/ave EDR of 1?!?!?! How can this be true?? That seems impossible in just about any reactor. This again points to my question number 4., do we have any data for how these baffles or baffles with obstacles are performing when compared to our models/predictions?   
    <img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%204_Flocculation/Images/Max_ave_EDR_of_1.JPG?raw=true" width=400>    

        - NO. Max/ave EDR is 2 for a well designed hydraulic flocculator. That means that Gmax/Gave is $\sqrt{2}$   
        - See [Harhoff Figure 8](https://www.environmental-expert.com/Files/5302/articles/9777/Towardsoptimaldesignparametersforaround-the-end.pdf)  where they find the minimum value of Gmax over Gave to be 1.4.
        - The slide that you show was addressing the question of efficiency of energy use for creating collisions. If the Gmax/Gave value is very large, then energy is not being used efficiently. The most energy efficient reactor has a uniform energy dissipation rate throughout the reactor. With a Gmax/Gava of 1.4 we get very close to the ideal efficiency and so we ignore this effect. We previously designed inefficient flocculators with high H/s ratios and thus we used to account for this inefficiency. Now we design all flocculators to be efficient with 3<H/s<6 and thus we can ignore this efficiency factor.

    7. should we transition everything from saying $G \theta$ over to $\bar G \theta$? It is more correct and eliminates another potential source of confusion.

        - Yes. let's switch to $\bar G$  

    8. Is the minimum width for fitting a human into the flocculator channel 45 cm?

        - yes  

    9. Why do we solve for $H_{e_{Max}}$ and round $H_e$ down instead of solving for $H_{e_{Min}}$ and roundin $H_e$ up? Is it because getting $\frac{H_e}{S}$ closer to 5 or 6 is closer to full expansion and we don't know the physics yet?

        - No. We are simply minimizing the number of expansions that we have to build. There is little difference between H/s of 3 and 6 and thus we are happy with an H/s anywhere in that range. Using an H/s closer to 6 reduces the number of obstacles that we build.   

    10. How tall should the baffles be? Should there be $S$ distance between the floor of the flocculator and the bottom of a top baffle? How does the 40 cm of head loss affect this for the flow over and around a bottom baffle?

        - I think our current design is to have 1.5s of space below the bottom of the upper baffle. My understanding is that there is little performance difference between an opening of 1s and 1.5s. We don't currently have any method of efficiently using the added triangle of water that builds up due to head loss. We have to keep our bottom baffles well below this so that the plant works under low flow conditions when head loss is dramatically reduced. Thus the water in the triangle may be relatively stagnant and we don't assume that the residence time in that triangle is helpful.  



***
## Tenth Progress Report: 6/??/2018  
### Done
1. Meeting with Monroe, Clare, Zoe, and Fletcher. Discussed the structure of the textbook, design challenges, and work for this summer. Textbook is top priority. I am to continue working on the summary sheets, which are being renamed to `Design` since that is the role that they occupy within the textbook.
2. Finish standardizing the images for control volume vs streamline notation (arrows vs dotted lines). Red lines imply energy/bernoulli, black is just reference.
3. Get rid of chapter number scetions
4. change all velocities to small v instead of big V

### To Do
1. Re do the opening lines of the summary sheets, which are now to be called the 'design' section of textbooks

2. Get a better reference for the b = 0.107s jet expansion. Gerhart Jirka's notes are the basis for this, but I think we need a better reference than one of Monroe's powerpoints

3. Haarhoff (the South African guy) actually recommends a slot width of 1S. He also mentions that slot widths used vary depending on the part of the world. 1.5 is common in South America, 1 in South Africa, and 0.5 in India.  
  <img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Chapter%204_Flocculation/Images/Slot_width_uncertainty.JPG?raw=true" width=400>
4. Discuss textbook structure Thursday May 31st
    - References? Equation numbering?
    -
5. Link Shultz and Okun-- also brings into consideration citations
6. Make sure that the flocculator design check is correct.
    - Should we account for head loss in the final residence time check? Monroe mentioned some time ago that the volume of water that is in the 'head loss triangle' doesn't contribute any meaningful shear.
7. Think meaningfully about the ordering of the flocculator design sheet. Where to introduce the physical flocculator parameters? $H$ vs $H_e$? efficiency? Obstacles? Do obstacles _have_ to go after efficiency?
