# DC Python Tutorial

TEST TEST TEST Hint: If you are typing a function name and want to know what the options are for completing what you are typing, just hit the tab key for a menu of options.

Hint: If you want to see the source code associated with a function, you can do the following
import inspect
inspect.getsource(foo)

Where "foo" is the function that you'd like to learn about.

Each section in Atom is either code or markdown. Markdown allows you to create very nicely formatted text including LaTeX equations, when certain packages are installed and the view is toggled on. An example:

$$c = \sqrt{a^2 + b^2}$$

You work can be previewed in real time using ctrl+shift+m, which opens up a second window that shows your work formatted nicely. To preview the LaTeX use ctrl + shift + x, if you have the markdown-preview-plus package installed (which you should)

Each code section within the markdown file needs to begin with the header line:

**```python**

and end with :

 **```**

Each code block will need to be run separately when you want to run your code. To run your code highlight the section between (but not including!) the heading and ending lines and click ctrl + enter. You can also place your cursor on a line and ctrl + enter to run one line at a time.

Variables and functions run while the file is open in Atom are saved by the program while it remains open, however if certain cells are not run any parameter contained in them will not be evaluated and those values won't be able to be used if referenced elsewhere in the code. Additionally if you delete a section of code after it was run, the parameters it created will still exist until the file is closed and reopened.

It is good practice to close, reopen, and rerun any assignment file after you've completed it to make sure it all runs as expected and that you haven't deleted an essential line of code!

---
```python
#Here we import packages that we will need for this assignment. You can find out about these packages in the Help menu.
# although math is "built in" it needs to be imported so it's functions can be used.
import math
from scipy import constants, interpolate
#see numpy cheat sheet https://www.dataquest.io/blog/images/cheat-sheets/numpy-cheat-sheet.pdf
#The numpy import is needed because it is renamed here as np.
import numpy as np
#Pandas is used to import data from spreadsheets
import pandas as pd
import matplotlib.pyplot as plt
# sys and os give us access to operating system directory paths and to sys paths.
import sys, os
# If you place your GitHub directory in your documents folder and
# clone both the design challenge file and the AguaClara_design repo, then this code should all work.
# If you have your GitHub directory at a different location on your computer,
# then you will need to adjust the directory path below.
# add the path to your GitHub directory so that Python can find files in other contained folders.

path1 = '~'
path2 = 'Documents'
#path3 = 'GitHub'
path3 = 'github'
#path4 = os.path.join(path1, path2, path3)
path4 = os.path.join(path1,path3)
myGitHubdir = os.path.expanduser(path4)
if myGitHubdir not in sys.path:
    sys.path.append(myGitHubdir)

myGitHubdir

print(os)
print(sys)
# add imports for AguaClara code that will be needed
# physchem has functions related to hydraulics, fractal flocs, flocculation, sedimentation, etc.
from aide_design import physchem as pc

# pipedatabase has functions related to pipe diameters
from aide_design import pipedatabase as pipe

# units allows us to include units in all of our calculations
from aide_design.units import unit_registry as u

from aide_design import utility as ut

```

---

## Resources in getting started with Python
Here are some basic [Python functions](http://docs.python.org/3/library/functions.html) that might be helpful to look through.

## Transitioning From Matlab To Python

**Indentation** - When writing functions or using statements, Python recognizes code blocks from the way they are indented.  A code block is a group of statements that, together, perform a task. A block begins with a header that is followed by one or more statements that are indented with respect to the header. The indentation indicates to the Python interpreter, and to programmers that are reading the code, that the indented statements and the preceding header form a code block.

**Suppressing Statements** - Unlike Matlab, you do not need a semi-colon to suppress a statement in Python;

**Indexing** - Matlab starts at index 1 whereas Python starts at index 0.

**Functions** - In Matlab, functions are written by invoking the keyword "function", the return parameter(s), the equal to sign, the function name and the input parameters. A function is terminated with "end".

`function y = average(x)
if ~isvector(x)
    error('Input must be a vector')
end
y = sum(x)/length(x);
end`

In Python, functions can be written by using the keyword "def", followed by the function name and then the input parameters in parentheses followed by a colon. A function is terminated with "return".

`def average(x):
   if ~isvector(x)
       raise VocationError("Input must be a vector")
   return sum(x)/length(x); `

**Statements** - for loops and if statements do not require the keyword "end" in Python. The loop header in Matlab varies from that of Python. Check examples below:

Matlab code

`s = 10;
H = zeros(s);
for c = 1:s
    for r = 1:s
        H(r,c) = 1/(r+c-1);
    end
end`

Python code

`s = 10
H = []
for (r in range(s)):
    for (c in range(s)):
        H[r][c].append(1/(r+c-1)`


**Printing** - Use "print()" in Python instead of "disp" in Matlab.

**Helpful Documents**

[Numpy for Matlab Users](https://docs.scipy.org/doc/numpy-dev/user/numpy-for-matlab-users.html)

[Stepping from Matlab to Python](http://stsievert.com/blog/2015/09/01/matlab-to-python/)

[Python for Matlab Users, UC Boulder](http://researchcomputing.github.io/meetup_fall_2014/pdfs/fall2014_meetup13_python_matlab.pdf)

---

## Arrays and Lists

Python has no native array type. Instead, it has lists, which are defined using [ ]:


```python
a = [0,1,2,3]
```

Python has a number of helpful commands to modify lists, and you can read more about them [here](https://docs.python.org/2/tutorial/datastructures.html).

In order to use lists as arrays, numpy (numpy provides tools for working with **num** bers in **py** thon) provides an array data type that is defined using ( ).

```python
a_array = np.array(a)
```

```python
a_array
```
    array([0, 1, 2, 3])

Pint, which adds unit capabilities to Python, (see section on units below) is compatible with NumPy, so it is possible to add units to arrays and perform certain calculations with these arrays. We recommend using NumPy arrays rather than lists because NumPy arrays can handle units. Additionally, use functions from NumPy if possible instead of function from the math package when possible because the math package does not yet handle units. Units are added by multiplying the number by the unit raised to the appropriate power. The pint unit registry was imported above as "u" and thus the units for milliliters are defined as u.mL.

The complete registry for units available for Pint can be found [here](https://github.com/hgrecco/pint/blob/master/pint/default_en.txt), though more details on units are below.


```python
a_array_units = a_array * u.m
```

```python
a_array_units

```
\[\begin{pmatrix}0 & 1 & 2 & 3\end{pmatrix} meter\]

In order to make a 2D array, you can use the same [NumPy array command](https://docs.scipy.org/doc/numpy/reference/generated/numpy.array.html).

```python
b = np.array([[0,1,2],[3,4,5],[6,7,8]])*u.mL
b
```

\[\begin{pmatrix}0 & 1 & 2\\
3 & 4 & 5\\
6 & 7 & 8\end{pmatrix} milliliter\]

Indexing is done by row and then by column. To call all of the elements in a row or column, use a colon. As you can see in the following example, indexing in python begins at zero. So `b[:,1]` is calling all rows in the second column

```python
b[:,1]

```

\[\begin{pmatrix}1 & 4 & 7\end{pmatrix} milliliter\]

If you want a specific range of values in an array, you can also use a colon to slice the array, with the number before the colon being the index of the first element, and the number after the colon being **one greater** than the index of the last element.

```python
b[1:3,0]
```

\[\begin{pmatrix}3 & 6\end{pmatrix} milliliter\]

For lists and 1D arrays, the `len()` command can be used to determine the length. Note that the length is NOT equal to the index of the last element because the indexes are zero based. The len function can be used with lists and arrays. For multiple dimension arrays the `len()` command returns the length of the first dimension.

```python
len(a)
```
4

```python
len(b)
```
    3

For any higher dimension of array, `numpy.size()` can be used to find the total number of elements and `numpy.shape()` can be used to learn the dimensions of the array.

```python
np.size(b)
```
    9

```python
np.shape(b)
```
    (3, 3)

For a listing of the commands you can use to manipulate numpy arrays, refer to the [scipy documentation](https://docs.scipy.org/doc/numpy/reference/routines.array-manipulation.html).

Sometimes, it is helpful to have an array of elements that range from zero to a specified number. This can be useful, for example, in creating a graph. To create an array of this type, use [numpy.arange](https://docs.scipy.org/doc/numpy/reference/generated/numpy.arange.html).

```python
crange = np.arange(10)
```

```python
crange
```
    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

```python
cdetailedrange = np.arange(5,10,0.1)
```

```python
cdetailedrange
```
    array([ 5. ,  5.1,  5.2,  5.3,  5.4,  5.5,  5.6,  5.7,  5.8,  5.9,  6. ,
            6.1,  6.2,  6.3,  6.4,  6.5,  6.6,  6.7,  6.8,  6.9,  7. ,  7.1,
            7.2,  7.3,  7.4,  7.5,  7.6,  7.7,  7.8,  7.9,  8. ,  8.1,  8.2,
            8.3,  8.4,  8.5,  8.6,  8.7,  8.8,  8.9,  9. ,  9.1,  9.2,  9.3,
            9.4,  9.5,  9.6,  9.7,  9.8,  9.9])
---

## Units

Units are essential to engineering calculations. Units provide a quick check on all of our calculations to help reduce the number of errors in our analysis. Getting the right dimensions back from a calculation doesn't prove that the answer is correct, but getting the wrong dimensions back does prove that the answer is wrong! Unit errors from incorrect conversions are common when using apps that don't calculate with units. Engineering design work should always include units in the calculations.

We use the [pint package](https://pint.readthedocs.io/) to add unit capabilities to our calculations in Python. We have imported the `pint.UnitRegistry` as 'u' and thus all of pint's units can be used by placing a 'u.' in front of the unit name. Meters are `u.m`, seconds are `u.s`, etc. Most units are simple values that can be used just like other terms in algebraic equations. The exception to this are units that have an offset. For example, in the equation PV=nRT, temperature must be given with units that have value of zero at absolute zero. We would like to be able to enter 20 degC into that equation and have it handle the units correctly. But you can't convert from degC to Kelvin by simply multiplying by a conversion factor. Thus for temperature the units have to be handled in a special way.

Temperatures require use of the u.Quantity function to enter the value and the units of temperature separated by a ',' rather than by a multiplication symbol. This is because it doesn't make sense to multiply by a temperature unit because temperatures (that aren't absolute temperatures) have both a slope and a nonzero intercept.

You can find [constants that are defined in pint](https://github.com/hgrecco/pint/blob/master/pint/constants_en.txt) at the github page for pint.

Below is a simple calculation illustrating the use of units to calculate the flow through a vertical pipe given a velocity and an inner diameter. We will illustrate how to calculate pipe diameters further ahead in the tutorial.


```python
V_up = 1*u.mm/u.s
D_reactor = 1*u.inch
A_reactor = pc.area_circle(D_reactor)
Q_reactor = V_up*A_reactor
Q_reactor
```
0.0005067074790974977 meter<sup>2</sup> millimeter/second

The result isn't formatted very nicely. We can select the units we'd like to display by using the `.to` method.

```python
Q_reactor.to(u.mL/u.s)
```
0.5067074790974977 milliliter/second

We can also force the display to be in the metric base units


```python
Q_reactor.to_base_units()
```

5.067074790974977e-07 meter<sup>3</sup>/second

If you need to strip units from a quantity (for example, for calculations using functions that don't support units) you can use the `.magnitude` method. It is important that you force the quantity to be in the correct units before stripping the units.


```python
Q_reactor.to(u.mL/u.s).magnitude
```
    0.5067074790974977

### Significant digits
Python will happily display results with 17 digits of precision. We'd like to display a reasonable number of significant digits so that we don't get distracted with 14 digits of useless information. We created a [sig function in the AguaClara_design repository](https://github.com/AguaClara/AguaClara_design/blob/master/utility.py) that allows you to specify the number of significant digits to display. You can couple this with the print function to create a well formatted solution to a calculation. The sig function also displays the accompanying units.

The sig function call is `ut.sig(value, sigfig)`.

### Example problem and solution.
Calculate the number of moles of methane in a 20 L container at 15 psi above atmospheric pressure with a temperature of 30 C.

```python
# First assign the values given in the problem to variables.
P = 15 * u.psi + 1 * u.atm
T = u.Quantity(30,u.degC)
V = 20 * u.L
# Use the equation PV=nRT and solve for n, the number of moles.
# The universal gas constant is available in pint.
nmolesmethane = (P*V/(u.R*T.to(u.kelvin))).to_base_units()
print('There are '+ut.sig(nmolesmethane,3)+' of methane in the container.')
nmolesmethane
```

    There are 1.62 mol of methane in the container.


1.6246299433154001 mole

---

## Functions

When it becomes necessary to do the same calculation multiple times, it is useful to create a function to facilitate the calculation in the future.

- Function blocks begin with the keyword def followed by the function name and parentheses ( ).
- Any input parameters or arguments should be placed within these parentheses.
- The code block within every function starts with a colon ( \: ) and is indented.
- The statement return [expression] exits a function and returns an expression to the user. A return statement with no arguments is the same as return None.
- (Optional) The first statement of a function can the documentation string of the function or docstring, written with apostrophes ' '.

Below is an example of a function that takes three inputs, pressure, volume, and temperature, and returns the number of moles.

```python
# Creating a function is easy in Python
def nmoles(P,V,T):
    return (P*V/(u.R*T.to(u.kelvin))).to_base_units()
```
Try using the new function to solve the same problem as above. You can reuse the variables. You can use the new function call inside the print statement.


```python
print('There are '+ut.sig(nmoles(P,V,T),3)+' of methane in the container.')
```

    There are 1.62 mol of methane in the container.


---

## Density Function
We will create and graph functions describing density and viscosity of water as a function of temperature. We will use the [scipy 1D interpolate function](https://docs.scipy.org/doc/scipy/reference/tutorial/interpolate.html#d-interpolation-interp1d) to create smooth interpolation between the known data points to generate a smooth function.

`density_water`, defined in [`physchem`](https://github.com/AguaClara/AguaClara_design/blob/master/physchem.py), is a function that returns a fluid's density at a given temperature. It has one input parameter, temperature (in Celsius).


```python
# Here is an example of how you could define the function yourself if you chose.

# Below are corresponding arrays of temperature and water density with appropriate units attached.

# The 1d interpolation function will use a cubic spline.
Tarray = u.Quantity([0,5,10,20,30,40,50,60,70,80,90,100],u.degC)
rhoarray = [999.9,1000,999.7,998.2,995.7,992.2,988.1,983.2,977.8,971.8,965.3,958.4]*u.kg/u.m**3
def DensityWater(T):

    rhointerpolated=interpolate.interp1d(Tarray, rhoarray, kind='cubic')
    rho=rhointerpolated(T.to(u.degC))
    return rho*u.kg/u.m**3

# You can get the density of water for any temperature using this function call.
print('The density of water at '+ut.sig(u.Quantity(20,u.degC),3) +' is '+ut.sig(DensityWater(u.Quantity(20,u.degC)),4)+'.')
```

    The density of water at 20.0 Celsius is 998.2 kg/m³.

---

## Pipe Database

The [`pipedatabase`](https://github.com/AguaClara/AguaClara_design/blob/master/pipedatabase.py) file in the `AguaClara_design` has many useful functions concerning pipe sizing. It provides functions that calculate actual pipe inner and outer diameters given the nominal diameter of the pipe. Note that nominal diameter just means the diameter that it is called (hence the descriptor "nominal") and thus a 1 inch nominal diameter pipe might not have any dimensions that are actually 1 inch!


```python
# The OD function in pipedatabase returns the outer diameter of a pipe given the nominal diameter, ND.
pipe.OD(6*u.inch)
```




6.625 inch



The ND_SDR_available function returns the nominal diameter of a pipe that has an inner diameter equal to or greater than the requested inner diameter [SDR, standard diameter ratio](http://www.engineeringtoolbox.com/sdr-standard-dimension-ratio-d_318.html). Below we find the smallest available pipe that has an inner diameter of at least 7 cm


```python
IDmin = 7 * u.cm
SDR = 26
ND_my_pipe = pipe.ND_SDR_available(IDmin,SDR)
ND_my_pipe
```

3.0 inch

The actual inner diameter of this pipe is


```python
ID_my_pipe = pipe.ID_SDR(ND_my_pipe,SDR)
print(ut.sig(ID_my_pipe.to(u.cm),2))
```

    8.2 cm

We can display the available nominal pipe sizes that are in our database.


```python
pipe.ND_all_available()
```

\[\begin{pmatrix}0.5 & 1.0 & 2.0 & 3.0 & 4.0 & 6.0 & 8.0 & 10.0 & 12.0 & 16.0 & 18.0 & 24.0 & 30.0 & 36.0 & 48.0 & 60.0 & 72.0\end{pmatrix} inch\]

---

## Physchem
The 'AguaClara_design' [physchem](https://github.com/AguaClara/AguaClara_design/blob/master/physchem.py) has many useful fluids functions including Reynolds number, head loss equation, orifice equations, viscosity etc.

---

## Viscosity Functions


```python
#Define the temperature of the fluid so that we can calculate the kinematic viscosity
temperature = u.Quantity(20,u.degC)
#Calculate the kinematic viscosity using the function in physchem which we access using "pc"
nu=pc.viscosity_kinematic(temperature)
print('The kinematic viscosity of water at '+ut.sig(temperature,2)+' is '+ut.sig(nu,3))
```

    The kinematic viscosity of water at 20 celsius is 1.00e-6 m²/s

---

## Our First Graph!

We will use [matplotlib](https://matplotlib.org/) to create a graph of water density as a function of temperature. [Here](https://matplotlib.org/users/pyplot_tutorial.html) is a quick tutorial on graphing.


```python
# Create a list of 100 numbers between 0 and 100 and then assign the units of degC to the array.
# This array will be the x values of the graph.
# Note: when running sections of graphing code, the result only looks nice if it is run as a block rather than line by line.
GraphTarray = u.Quantity(np.arange(100),u.degC)

#Note the use of the .to method below to display the results in a particular set of units.
plt.plot(GraphTarray, pc.viscosity_kinematic(GraphTarray).to(u.mm**2/u.s), '-')
plt.xlabel('Temperature (degrees Celcius)')
plt.ylabel('Viscosity (mm^2/s)')
plt.title('Viscosity vs Temperature')
plt.show()
plt.savefig('viscosity_vs_temperature.png')
```

![png](DC_Python_Tutorial_Solution_files/DC_Python_Tutorial_Solution_61_0.png)


### Reynolds number
We will use the physchem functions to calculate the Reynolds number for flow through a pipe.


```python
Q = 5*u.L/u.s
D = pipe.ID_SDR(4*u.inch,26)

Reynolds_pipe = pc.re_pipe(Q,D,nu)
Reynolds_pipe
```

    60124.953167297012



Now use the sig function to display calculated values to a user specified number of significant figures.


```python
print('The Reynolds number is '+ut.sig(pc.re_pipe(Q,D,nu),3))
```

    The Reynolds number is 6.01e+4


Here is a table of a few of the equations describing pipe flow and their physchem function counterparts. (If you haven't already tested your LaTeX viewing capacity, now is the perfect time to try it with ctrl + shift + x)

| Equation Name|  Equation   |    Physchem function  |
|----------|:-------:|:-------:|
| Reynolds Number |  $Re= \frac{{4Q}}{{\pi D\nu }}$  | `re_pipe(FlowRate, Diam, Nu)`                |
| Swamee-Jain Friction factor           |                ${\rm{f}} = \frac{{0.25}}{{{{\left[ {\log \left( {\frac{\varepsilon }{{3.7D}} + \frac{{5.74}}{{{{{\mathop{\rm Re}\nolimits} }^{0.9}}}}} \right)} \right]}^2}}}$                |             `fric(FlowRate, Diam, Nu, PipeRough)`            |
| Hagen Pousille laminar flow head loss |                                                   ${h_{\rm{f}}} = \frac{{32\mu LV}}{{\rho g{D^2}}} = \frac{{128\mu LQ}}{{\rho g\pi {D^4}}}$                                                   |                                                              |
| Darcy Weisbach head loss              |                                                             ${h_{\rm{f}}} = {\rm{f}}\frac{8}{{g{\pi ^2}}}\frac{{L{Q^2}}}{{{D^5}}}$                                                            |    `headloss_fric(FlowRate, Diam, Length, Nu, PipeRough)`    |
| Swamee-Jain equation for diameter                              | $0.66\left ( \varepsilon ^{1.25}\left ( \frac{LQ^{2}}{gh_{f}} \right )^{4.75}+\nu Q^{9.4}\left ( \frac{L}{gh_{f}} \right )^{5.2} \right )^{0.04}$| `diam_swamee(FlowRate, HeadLossFric, Length, Nu, PipeRough)` |


```python
# create a plot that shows both the original data values (plotted as points)
# and the smooth curve that shows the density function.
# Note that Tarray and rhoarray were defined much earlier in this tutorial.

#We will plot the data points using circles 'o' and the smooth function using a line '-'.

plt.plot(Tarray, rhoarray, 'o', GraphTarray, (DensityWater(GraphTarray)), '-')
# For an x axis log scale use plt.semilogx(Tarray, rhoarray, 'o', xnew, f2(xnew), '-')
# For a y axis log scale use plt.semilogy(Tarray, rhoarray, 'o', xnew, f2(xnew), '-')
# For both axis log scale use plt.loglog(Tarray, rhoarray, 'o', xnew, f2(xnew), '-')


#Below we create the legend and axis labels
plt.legend(['data', 'cubic'], loc='best')
plt.xlabel('Temperature (degrees Celcius)', fontsize=20)
plt.ylabel('Density (kg/m^3)', fontsize=20)
plt.title('Density vs Temperature')

#Now we show the graph and we are done!
plt.show()
plt.savefig('desity_vs_temperature.png')
```


![png](DC_Python_Tutorial_Solution_files/DC_Python_Tutorial_Solution_68_0.png)
