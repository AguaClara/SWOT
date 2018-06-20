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
