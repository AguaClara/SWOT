Potential Conceptual Design Questions as existed previously in DC's
1. General Flow:  
a.  Why doesn't the flow change much in a plant over a wide range of temperatures even though the viscosities change greatly over  10-30 degree C range?
    - The flow is turbulent so viscosity doesn't matter
2. LFOM Failure:  
a.
  Describe at least two failure modes where the design produces very inaccurate flow measurements.
    - For very high flow rates (100 L/s) that the LFOM doesn't reach the target flow until half of the LFOM is submerged.
    - For very low flow rates (1 L/s) the algorithm overshoots with too many orifices in the bottom row.  

    b.
  Explain why all LFOMs perform poorly when the water depth is in the first row of orifices.
   - The relationship between head and flow is nonlinear for a single row of orifices. Thus it is impossible for the LFOM to be accurate when there is only one row of orifices.  

    c.
  Explain why all of the bottom several rows have the same number of orifices for flows about 30 L/s. (Hint: What constrains the maximum number of orifices that can be in a row?)
    - The number of orifices in a row is limited by the circumference of the LFOM. For high flow rates the ideal number of orifices in the first row exceeds the space and thus the flow target is not met for the first several rows. Each of these rows simply has the maximum number that can fit around the pipe.
3. What control the flow? What measures the flow? How are they related?
4. For each unit process what is the main design constraint/most important aspect to consider?
5. Rapid Mix:  
  a. Would a mechanical rapid mix unit take less power when the water is warmer?  
    - You might think that the rapid mix unit will take less electrical power when the water is warmer. But that isn't the case because the Reynolds number for the rapid mix propeller is quite high and thus the drag coefficient is independent of Re. This means that the torque required to spin the propeller doesn't change as the viscosity of the water changes. It would be possible to run the propeller slower when the water is warmer because the required energy dissipation rate is lower, but that would require a variable speed drive. You could add a variable speed motor controller to take advantage of this. However, the bigger problem is that we don't yet have a good model explaining what rapid mix does.  
    b.
    Write a paragraph describing what you learned from this design challenge. Include reflections on the temptation to use a standard design, the low capital cost of energy wasting designs, and the long term implications of engineering that isn't guided by a goal of sustainability.  
    c. What is the relation of flow expansion/dissipation from a jet to the goal of the rapid mix section? (Flow expansions are mentioned in the problem statement but vaguely and without explanation)
6.

-------
Notes for future DC:

<div class="alert alert-info" role = "alert">

## **A brief programming guide**
1.	Do not use a numerical or iterative solution when an analytical solution is easily available.
2.	Whenever a function has the potential to be used multiple times, create a function call that includes the parameters that could potentially change.
3.	Do not break dependency. That means that if I change an input parameter at the top of your notebook, that I should get the correct answers for the new parameter for all related calculations in the notebook.
4.	Always use dimensions (units). All calculations involving physical units must include those units.
5.	Document your design process with comments.
6.  Do not redefine your variables in subsequent problems. This loses valuable digits of precision on your numbers and can cause a lot of trouble and frustration.
7.  For everyone's sake, use logical and reasonable variable names. [Here is AguaClara variable naming convention](https://github.com/AguaClara/aide_design/wiki/Variable-Naming)
</div>

## A brief Design Challenge guide
1.  Read the Problem statement in its entirety before beginning a problem. If you don't immediately know what to do, read it again, thoroughly. If you are getting stuck, read it a third time. If you have a good understanding of what the problem is asking and are still having trouble, TAs can help through email or office hours.
2.  If you decide to email a TA, make sure the other two are CC'ed. This minimizes the time you will have to wait until one responds.
3.  When in doubt, re-run all code sections from the beginning
4.  Play around! Print arrays, test inputs, and ask yourself if your answers are reasonable. Should flow have units of km*mg/s?
5. Make sure to review convention and syntax standards, which can be found here:
    * [Standards Page](https://github.com/AguaClara/aide_design/wiki/Standards) for naming standards.
    * [Variable Naming Guide](https://github.com/AguaClara/aide_design/wiki/Variable-Naming) for creating variable names.

<div class="alert alert-block alert-danger">

Before you begin this assignment, you must download the latest version of aide_design. Follow the instructions on the 4540 Wiki, at the bottom of the [Anaconda](https://confluence.cornell.edu/display/cee4540/Anaconda) subpage. Step 4 specifically gives direction for updating the aide_design package
</div>
--------------------
Flow control graph question: (vertical and horizontal orifice graph)
### 3)
Write a paragraph about what the graph means by explaining the following two items:
  - Explain why the vertical orifice equation predicts more flow when the water level is below the center of the orifice and predicts less flow when the water level is above the center of the orifice. It might help to draw a picture of what the equations are describing to understand what is happening here!
  - Explain how the horizontal orifice equation function from `physchem.py` predicts the flow rate for submergence depths that are negative. You will need to find the function and look at the code.

### Explanation

The vertical orifice has the lower part of the orifice partially submerged before the horizontal orifice has any part submerged. This explains why the vertical orifice has more flow than the horizontal orifice between -0.5 and 0.

The horizontal orifice has higher flow rates between 0 and 0.5 because it is fully submerged when the vertical orifice is still not fully submerged.

At the elevation where the vertical orifice is first fully submerged the flow rate through the vertical orifice is less than the flow rate through the horizontal orifice. This is a result of the nonlinear relationships between depth of submergence and velocity.

The difference between the two equations becomes negligible for submergence greater than 1 diameter.

For negative depths of submergence the horizontal orifice function uses an if statement to set the flow rate through the orifice equal to zero.
### 7)

Using the code in Example XX in the LFOM chapter of the book:

Play with the value for the plant flow rate, `Flow` by trying a bunch of different flows over the range 1 to 100 L/s. Comment on something that you notice and that you think could be improved in the design of the LFOM.

The flow rates seem to exceed the target flow by a tiny factor over the majority of the range. This means there is a systemic error in the algorithm that sets the number of orifices in each row.
The LFOM isn't accurate for the first couple of rows.

### 20)
From Chemical dosing example in section XX and table XX.
Which option do you think is best? You can simply set the array index to your choice and then display your solution by using that index value on your arrays for number of tubes, flow rates, tube diameters, and length of tubes.


```python
MYPICK = 1
print('The number of dosing tubes I will need is',ut.sig(NDosingTubes[MYPICK],1))
print('The flow through each tube is', ut.sig(FlowDosingTubeArray[MYPICK],3))
print('The inner diameter of the tube is', DiamTubeArray[MYPICK])
print('The length of each tube is', ut.sig(LengthDosingTube[MYPICK].to(u.m),3))
```

    The number of dosing tubes I will need is 1
    The flow through each tube is 1.95 ml/s
    The inner diameter of the tube is 0.125 inch
    The length of each tube is 2.43 m


### 21)
What physical constraints might you use to select the best solution? How did you make your selection in Problem 19?

The ideal solution will have
- a "reasonable" number of tubes and thus one possibility is to select the smallest diameter of tubing that uses a single tube. However, this won't work for plants with high flow rates of chemicals.
- tubes that are short enough to mount in the water treatment plant

### 22)
AguaClara has coded these dosing tube size functions in the CDC Functions (cdc_functions). Find the function calls for the length, diameter, and number of dosing tubes and use those functions to calculate the values for the problem that you solved above. Compare your answers. Your answers should agree!



```python

EnChem = 2
#see the viscosity_kinematic_chem(conc_chem, temp, en_chem): to see how EnChem is used, as a way to give chemical parameters
# The maximum tube length constraint might be based on the length of the available wall where the
# dosing tube will be mounted. You might change this depending on which solution
# you picked in step 20. Here the wall length is LengthTubeMax.

LengthTubeMax = 5*u.m

LengthTubeCheck = cdc.len_cdc_tube(FlowPlant, DoseCl2, StockCl2,  DiamTubeArray, HeadlossDosingTubeMax, LengthTubeMax, T, EnChem, KMinor)

print('The length of the CDC tube is ', ut.sig(LengthTubeCheck,3))

DiamTubeCheck = cdc.diam_cdc_tube(FlowPlant, DoseCl2, StockCl2, DiamTubeArray,  HeadlossDosingTubeMax, LengthTubeMax, T, EnChem, KMinor)

print('The diameter of the CDC tube is', ut.sig(DiamTubeCheck.to(u.inch),3))

NTube = cdc.n_cdc_tube(FlowPlant, DoseCl2, StockCl2, DiamTubeArray, HeadlossDosingTubeMax,  LengthTubeMax, T, EnChem, KMinor)

print('The number of CDC tubes is ', ut.sig(NTube,1))
```

    The length of the CDC tube is  2.43 m
    The diameter of the CDC tube is 0.125 in
    The number of CDC tubes is  1.0
