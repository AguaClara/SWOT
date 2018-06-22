# Textbook Guidelines and Convention

***
## Document Headings
A document should always begin with the biggest size heading (#) stating the name of the document. First comes the chapter name, then a line break using < / br >, then the chapter section all in the same line. For example:
# Chapter <br> Section
Each subsequent header begins with ## and continues hierarchically, ###, then ####, and so on.
***

## Figures and Tables
When writing, embed figures with html convention for more flexibility:  
`<img src="figure_name.com/things/stuff.jpg" width="600">` instead of markdown convention:  
`![Figure Referral](figure_name.com/things/stuff.jpg)`  
html convention allows you to change the figure's size by changing the value of `width=600`.
### Centering
Using html code also allows you more flexibility when aligning an image.  
Centering:
`<center><img src="figure_name.com/things/stuff.jpg" width="600"></center>`
Left align: `<img src="figure_name.com/things/stuff.jpg" width="600" style="float: left">`  
***


## Equations
Whenever a new equation is introduced, it should be followed by a list explaining its parameters. If the equation has a counterpart in aide design, that should be included after the parameter explanation. In the example equation below, taken from 'Fluids_Review_Design.md', $Q$ and $g$ where introduced in previous equations and did not need to be reintroduced

$$Q = \Pi_{vc} A_{or} \sqrt{2g\Delta h}$$

Where:  
$\Pi_{vc}$ = 0.62 = vena contracta coefficient, in aide_design as `pc.RATIO_VC_ORIFICE`  
$A_{or}$ = orifice area- NOT contracted flow area  
$\Delta h$ = elevation difference between orifice and water level

**Equations in aide_design:**  
[`pc.flow_orifice(Diam, Height, RatioVCOrifice)`](https://github.com/AguaClara/aide_design/blob/e2e092605698adca8c8903e3c3a555e069027f1e/aide_design/physchem.py#L385) Returns flow through a horizontal orifice.  
`pc.flow_orifice_vert(Diam, Height, RatioVCOrifice)` Returns flow through a vertical orifice. The height parameter refers to height above the center of the orifice.

This example should be closely followed when presenting equations, including the word 'Where:' with a colon to introduce the parameters and the format used to introduce the equations in aide_design.
***

## Text Coloring
### <font color="red">Red is Uncertain</font>
Red coloring indicates that there is more research to be done on the topic under consideration. Any concept colored red will be further discussed in the 'Uncertainties' section of each chapter.

### <font color="purple">Purple is Final Equation in a Derivation or Control Volumes/Streamlines</font>
A purple colored equation indicates that a final equation is being presented. This is most often found at the end of equation derivations within the 'Derivations' section of a chapter.  
When purple is seen in an image, it indicates a streamline or a control volume

### <font color="blue">Blue is ... Do we need another color? If so what should we assign to it? </font>


## Parameters
For parameters to use in Python code, [follow this convention](https://github.com/AguaClara/aide_design/wiki/Variable-Naming "aide naming convention page").

Units should not be _italicized_. For example, 3 meters should be written as $3 \, {\rm m}$ instead of $3 \, m$ to firmly distinguish units from parameters/variables.

Once more textbook sections are done, we should consider reorganizing this into easier to follow sections. Perhaps have a list of frequently used parameters (like $Q$, $h_L$ $v$, etc) along with parameters specific to each unit process ($\Pi_{Error}$, $\Pi_{\bar \varepsilon}^{\varepsilon_{Max}}$, $\Pi_{\bar G}^{G_{Max}}$), and have them neatly separated and ennumerated.

Base units

| Dimension | Abbreviation | Base Unit |
|:---------:|:------------:|:---------:|
|  Length   |    $[L]$     |   meter   |
|   Time    |    $[T]$     |  second   |
|   Mass    |    $[M]$     | kilogram  |

Parameters

|                  Parameter                   |                           Description                           |          Units           |
|:--------------------------------------------:|:---------------------------------------------------------------:|:------------------------:|
|                     $m$                      |                              Mass                               |          $[M]$           |
|                     $z$                      |                            Elevation                            |          $[L]$           |
|                     $L$                      |                             Length                              |          $[L]$           |
|                     $W$                      |                              Width                              |          $[L]$           |
|                     $H$                      |                             Height                              |          $[L]$           |
|                     $D$                      |                            Diameter                             |          $[L]$           |
|                     $r$                      |                             Radius                              |          $[L]$           |
|                     $A$                      |                              Area                               |         $[L]^2$          |
|                 $\rlap{-} V$                 |                             Volume                              |         $[L]^3$          |
|                     $v$                      |                            Velocity                             |    $\frac{[L]}{[T]}$     |
|                     $Q$                      |                            Flow rate                            |   $\frac{[L]^3}{[T]}$    |
|                     $n$                      |                         Number, Amount                          |            -             |
|                     $C$                      |                          Concentration                          |   $\frac{[M]}{[L]^3}$    |
|                     $p$                      |                            Pressure                             |  $\frac{[M]}{[L][T]^2}$  |
|                     $g$                      |                   Acceleration due to Gravity                   |   $\frac{[L]}{[T]^2}$    |
|                    $\rho$                    |                             Density                             |   $\frac{[M]}{[L]^3}$    |
|                    $\mu$                     |                        Dynamic viscosity                        |   $\frac{[M]}{[T][L]}$   |
|                    $\nu$                     |                       Kinematic viscosity                       |   $\frac{[L]^2}{[T]}$    |
|                     $h$                      |                         Head, Elevation                         |          $[L]$           |
|                    $h_L$                     |                            Headloss                             |          $[L]$           |
|                 $h_{\rm f}$                  |                      Major Loss (friction)                      |          $[L]$           |
|                  $\epsilon$                  |                        Surface roughness                        |          $[L]$           |
|                   $\rm{f}$                   |                 Darcy-Weisbach friction factor                  |            -             |
|                  ${\rm Re}$                  |                         Reynolds Number                         |            -             |
|                    $h_e$                     |                     Minor Loss (expansion)                      |          $[L]$           |
|                     $K$                      |                     Minor Loss coefficient                      |            -             |
|                    $\Pi$                     |               Dimensionless Proportionality Ratio               |            -             |
|                  $\Pi_{vc}$                  |                    Vena Contracta Area Ratio                    |            -             |
|                $\Pi_{Error}$                 |                      Linearity Error Ratio                      |            -             |
|                     $M$                      |                         Fluid Momentum                          |  $\frac{[M][L]}{[T]^2}$  |
|                     $F$                      |                              Force                              |  $\frac{[M][L]}{[T]^2}$  |
|                     $t$                      |                              Time                               |          $[T]$           |
|                   $\theta$                   |                         Residence Time                          |          $[T]$           |
|                     $G$                      |               Velocity Gradient/Fluid Deformation               |     $\frac{1}{[T]}$      |
|                $\varepsilon$                 |                     Energy Dissipation Rate                     |  $\frac{[L]^2}{[T]^3}$   |
|           $\Pi_{\bar G}^{G_{Max}}$           |           $\frac{G_{Max}}{\bar G}$ Ratio in a Reactor           |            -             |
| $\Pi_{\bar \varepsilon}^{\varepsilon_{Max}}$ | $\frac{\varepsilon_{Max}}{\bar \varepsilon}$ Ratio in a Reactor |            -             |
|                  $\Pi_{HS}$                  |            Height to Baffle Spacing in a Flocculator            |            -             |
|                    $H_e$                     |         Height Between Flow Expansions in a Flocculator         |          $[L]$           |
|                     $S$                      |                   Spacing Between Two Objects                   |          $[L]$           |
|                     $B$                      |          Center-to-Center Spacing Between Two Objects           |          $[L]$           |
|                     $T$                      |                        Object Thickness                         |          $[L]$           |
|                     $P$                      |                              Power                              | $\frac{[M][L]^2}{[T]^3}$ |
|                   $\eta_K$                   |                     Kolmogorov Length Scale                     |          $[L]$           |
|                $\lambda_\nu$                 |                   Inner Viscous Length Scale                    |          $[L]$           |
|                 $\Pi_{K\nu}$                 | Ratio of Inner Viscous Length Scale to Kolmogorov Length Scale  |            -             |
|                  $\Lambda$                   |                   Distance Between Particles                    |          $[L]$           |
|                                              |                                                                 |                          |
|                                              |                                                                 |                          |
|                                              |                                                                 |                          |
|                                              |                                                                 |                          |
