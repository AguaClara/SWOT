Name:
# Prelim 1 CEE 4520
Open book, open internet. No discussion boards, no posting issues, no conversation with anyone other than Monroe, Matt, or Jillian about anything on this exam! You may send questions to Monroe, Matt, and Jillian.

Note that total points for the exam = 106

# Multiple choice (4 points each)

**Bold** the correct answer

 1) How far away from the location where the chemical dose is set is the flocculator in an AguaClara plant (pick the answer that is the best approximation)?

    a) 1 m

    b) 5 m

    c) 10 m

    d) 20 m

2) Which equation can be used when there is a loss (or increase) of mechanical energy?

    a) Energy Equation

    b) Bernoulli Equation

3) What happens to the maximum energy dissipation rate in a plane jet if velocity is held constant and the width of the jet is increased?

    a) The maximum energy dissipation rate increases

    b) The maximum energy dissipation rate remains constant

    c) The maximum energy dissipation rate decreases

4) Which type of head loss increases linearly with flow rate?

    a) Laminar flow major loss

    b) Laminar flow minor loss

    c) Turbulent flow major loss

    d) Turbulent flow minor loss

# Short Answer (4 points each)

1) What is the dimensionless *vena contracta* coefficient a ratio of?



2) Identify a location in an AguaClara entrance tank where the Bernoulli equation can be used to describe the flow. Explain WHY the Bernoulli equation can be used.



3) What happens to the coagulant dose (assuming the operator doesn't change anything) in an AguaClara plant when the flow rate through the plant changes from the plant maximum design flow to 50% of the maximum design flow?



4) What is Monroe's hypothesis for why primary particles such as clay and pathogens can't attach to flocs in a flocculator?



5)  Give one example each of a minor loss and a major loss in AguaClara plants





# Design Challenges
Document your work. Show any equations that you use in latex. Then do the calculation in python. Simplify the units to something that is easy to understand (SI metric system please!). Print your answer in python and copy that answer and paste it into markdown so your answer is shown without needing to run the code.

Here are some import statements that will likely be helpful. You may, of course, import other packages if needed!

```Python
from aguaclara.core.units import unit_registry as u
from aguaclara.core import utility as ut
from aguaclara.core import physchem as pc
import aguaclara.design.floc as floc
from aguaclara.research import floc_model as fm
import matplotlib.pyplot as plt
import numpy as np
```

1) Water at $15^\circ C$ flows through a straight, smooth tube that is 1/8th inch in inner diameter, 2 m long, has a head loss of 20 cm, and has total minor loss coefficients for entrance and exit of 4.
a) (5 points) What is the flow rate?
b) (5 points) Is this flow laminar or turbulent?

```Python


```


2) (10 points) A mechanical hydraulic mix unit for a 3 mgd (million gallon per day) water treatment plant has a residence time of 30 seconds and a $G_{CS}$ of 1000 Hz. Estimate the cost of this energy per year.  You may neglect the fact that the designer had to round up to next available motor size. You may assume that the rapid mix unit is 80% efficient at converting electricity into fluid shear. The temperature ranges from $0 \circ C$ to $30 \circ C$. The unit was designed to deliver the target fluid deformation for the worst case temperature. The cost of electricity is 0.15 USD/(kW hr).


```python

```

3) A flocculator designed using the AguaClara code has a design flow of 20 L/s and a design temperature of $15^\circ C$.  You may use the flocculator code to check you answer, but do the calculation using an equation that you derive.

   a) (5 points) Calculate the Camp Stein velocity gradient, $G_{CS}$, for the flocculator based on the flow characteristics and geometry of one flow expansion.

   b) (5 points) Calculate the residence time for one flow expansion based on the flow characteristics and geometry of that expansion.

   c) (5 points) Calculate the $G_{CS}\theta$ for one flow expansion

   d) (5 points) Calculate the number of flow expansions required given the design goal of $G_{CS} = 37,000 $.

```Python

Q_design=20 * u.L/u.s
temp=15 * u.degC
myF = floc.Flocculator(Q=Q_design, temp=15 * u.degC)

```



4) (15 points) Plot $G_{CS}\theta$ for the flocculator in problem 3 if it is built and then operated over a range of flows from 25% to 100% of the design flow. Start by deriving an equation for $G_{CS}\theta$ that accounts for the fact that the flocculator is built (geometry is constant) and the flow rate is varying.


```Python

```

5) One of our goals it to produce water that is dramatically cleaner than regulations require.

    a) (5 points) How far apart will clay particles (equivalent spherical diameter of $5 \mu m$ and density of $2650 \frac{kg}{m^3}$) be if their concentration is 0.01 mg/L?

    b) (5 points) What is the mass of a clay particle?

    c) (5 points) How many clay particles would there be in a 250 mL glass of water?


```Python

```
