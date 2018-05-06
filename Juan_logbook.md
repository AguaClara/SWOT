# Logbook for Spring 2018 CEE 4540 Updates

This file will contain weekly updates into my work. All changes will be pushed to a non-master branch, and I will only have one branch at a time for whatever project I am working on. Every week (the day depends on my work schedule that week), I will send Monroe an email containing a link to this file's page on GitHub in addition to supplementary material. For example, this first week I will send him the example of the 'extra' slides for his viewing pleasure (or displeasure).

***
##List of Big Ideas and Big Concerns
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
2. Re-evaluate the my work priorities, considering time. Perhaps I should prioritize creating derivation sheets to remove derivations from powerpoints, and then spruce up the powerpoints before returning to the summary sheets. The summary sheets take a very, very long time to do well :/
I think that will greatly improve the chance that some things are completely done and what _is_ done is done very well by the beginning of the semester.



***
## Eigth Progress Report: 5/??/2018  
### Done  
1. Make sure to check for consistency in these things in the final read-through:  
    1. Consistency in $Q \propto h$ vs $h \propto Q$
    2. Consistency in $h$ vs $\Delta h$ vs $z$

2. Change image insertion from markdown style to html to allow for resizing- silly markdown
3. Added the head loss trick to fluids Review
    - REMEBER TO CHANGE THE DERIVATION sheets for this and also the $\rlap{\Bigg/}x$ to things
4. Reorganized CEE4540_Master repo by chapter to make organizing a book easier and avoid enormous image folders.

### To Do
1. Questions/confirmations for Monore
    1. In [this minor loss equation derivation](https://github.com/AguaClara/CEE4540_Master/blob/Juan_summary_sheets/Summary%20Sheets/Derivation_minor_loss_equation.md), why is $p_{in}$ with $A_{out}$ instead of $A_{in}$?
    2. When [deriving the CDC equations](https://github.com/AguaClara/CEE4540_Master/blob/Juan_summary_sheets/Summary%20Sheets/Derivation_designing_the_cdc.md), why do you take the limit as Q approaches 0? Is that when the difference between the actual head loss and the linearized model is the greatest, percentage-wise?
    3.
