# Appendix C: Examples

##Manzaragua Water Treatment Plant
The Mazaragua AguaClara plant consists of two 1 L/s plants operating in parallel. The plant is located in the municipality of Guinope, the department of El Paraiso, Honduras.

The plant performed very poorly from the first day of operation. The first attempted fix was to double the flocculator residence time by increasing the number of flocculator pipes (3 inch diameter by 1.5 m long) from 12 to 24. This improved performance, but the plant continued to perform poorly. A raw water sample was analyzed on May 30, 2018 and the following results were obtained.

<center><img src="https://raw.githubusercontent.com/AguaClara/CEE4540_Master/master/AguaClara%20Water%20Treatment%20Plant%20Design/Rapid%20Mix/Images/Manzaragua_Water_Analysis.jpg" width=600></center>


### Table 1. Water quality analysis
| Parameter | Units | Standard | Results |
| - | - | :-: | :-: |
| Turbidity | NTU | 5 | 71 |
| Color | color units | 15 | 150 |
| pH | pH | 6.5 - 8.5 | 5.91 |
| Conductivity | $\mu s/cm$ | 400 | 69.15 |
| Alkalinity | $mg/L$ as $CaCO_3$ | - | 24.5 |
| Bicarbonates | $mg/L$ as $CaCO_3$ | - | 24.5 |
| Carbonates | $mg/L$ as $CaCO_3$ | - | 0 |
| Hardness | $mg/L$ as $CaCO_3$ | 400 | 15.68 |

This water has high color which suggests a high concentration of dissolved organic matter. The pH is a clear problem because the pH is too low for the coagulant nanoparticles to precipitate. As this pH a significant fraction of the coagulant will remain soluble.

Our goal is to determine how much $Na_2CO_3$ will need to be added to raise the pH. <font color="red">We do not have data on the optimal pH for treating high color water with PACl and so we will use pH 7 as the target. </font> We will need a separate calculation to estimate how much additional $Na_2CO_3$ will need to be added to balance the PACl acidity.

At circumneutral pH (pH close to 7) the buffering capacity of the water is dominated by carbonate chemistry and specifically by the equilibrium between ${H_2}CO_3^{\star}$ and $HCO_3^- $. From the water analysis the total concentration of carbonates is 24.5 mg/L as $CaCO_3$.


Equations describing carbonate chemistry are given below.

### Carbonate Chemistry
Carbonic acid and bicarbonate
$${H_2}CO_3^{\star} \overset {K_1} \longleftrightarrow {H^+} + HCO_3^- $$

$${K_1} = \frac{{\left[ {{H^ + }} \right]\left[ {HCO_3^ - } \right]}}{{\left[ {{H_2}CO_3^{\star} } \right]}}$$ $$p{K_1} = 6.3$$

bicarbonate and carbonate $$HCO_3^ - \overset {{K_2}} \longleftrightarrow {H^ + } + CO_3^{ - 2}$$ $${K_2} = \frac{{\left[ {{H^ + }} \right]\left[ {CO_3^{ - 2}} \right]}}{{\left[ {HCO_3^ - } \right]}}$$ $$p{K_2} = 10.3$$

Total concentration of carbonates

$${C_T} = \left[ {{H_2}CO_3^{\star} } \right] + \left[ {HCO_3^ - } \right] + \left[ {CO_3^{ - 2}} \right]$$

Alpha notation

$$\left[ {{H_2}CO_3^{\star} } \right] = {\alpha_0}{C_T}$$

$$\left[ {HCO_3^ - } \right] = {\alpha_1}{C_T}$$

 $$\left[ {CO_3^{ - 2}} \right] = {\alpha_2}{C_T}$$

Acid Neutralizing Capacity (ANC) $${\text{ANC}} = [HCO_3^ - {\text{] + 2[CO}}_3^{ - 2}{\text{] + [O}}{{\text{H}}^{\text{ - }}}{\text{] - [}}{{\text{H}}^{\text{ + }}}{\text{]}}$$ ANC in alpha notation $$ANC = {C_T}({\alpha_1} + 2{\alpha_2}) + \frac{{{K_w}}}{{\left[ {{H^ + }} \right]}} - \left[ {{H^ + }} \right]$$

Alpha equations for the carbonate system
$${\alpha_{\text{0}}} = \frac{1}{{1 + \frac{{{K_1}}}{{[{H^ + }]}} + \frac{{{K_1}{K_2}}}{{{{[{H^ + }]}^2}}}}}$$

$${\alpha_{\text{0}}} = \frac{1}{{1 + \frac{{{K_1}}}{{[{H^ + }]}}\left( {1 + \frac{{{K_2}}}{{[{H^ + }]}}} \right)}}$$

$${\alpha_{\text{1}}} = \frac{1}{{\frac{{[{{\rm H}^ + }]}}{{{{\rm K}_1}}} + 1 + \frac{{{{\rm K}2}}}{{[{{\rm H}^ + }]}}}}$$

$${\alpha{\text{2}}} = \frac{1}{{\frac{{{{[{{\rm H}^ + }]}^2}}}{{{{\rm K}_1}{{\rm K}_2}}} + \frac{{[{{\rm H}^ + }]}}{{{{\rm K}_2}}} + 1}}$$

$${\alpha_{\text{2}}} = \frac{1}{{1 + \frac{{[{{\rm H}^ + }]}}{{{{\rm K}_2}}}\left( {1 + \frac{{[{{\rm H}^ + }]}}{{{{\rm K}_1}}}} \right)}}$$

Acid neutralizing capacity for the case where the system is not exchanging $CO_2$ with the atmosphere

$$ANC = {C_T}({\alpha_1} + 2{\alpha_2}) + \frac{{{K_w}}}{{\left[ {{H^ + }} \right]}} - \left[ {{H^ + }} \right]$$

Acid neutralizing capacity for the case where the system is in equilibrium with atmospheric $CO_2$

$$ANC = \frac{{{P{C{O_2}}}{K_H}}}{{{\alpha_0}}}({\alpha_1} + 2{\alpha_2}) + \frac{{{K_w}}}{{\left[ {{H^ + }} \right]}} - \left[ {{H^ + }} \right]$$

# Solution steps to find the required $Na_2CO_3$ dose
We will use the acid neutralizing capacity (reported as calcium carbonate alkalinity) and the pH from the sample analysis to estimate the total concentration of carbonates. We will not use the sample analysis carbonate concentrations because they can not be correct given that the pH is not equal to 7.

1) Find total carbonate concentration of the sample using the ANC equation for the case where the system is not exchanging $CO_2$ with the atmosphere.
1) Find the required ANC to achieve a pH of 7
1) Take the difference between the sample ANC and the ANC at pH 7 to find how much base must be added.

For step 1 we need to solve the ANC equation for the carbonate concentration.

$$ C_T = \frac{ANC  - \frac{{{K_w}}}{{\left[ {{H^ + }} \right]}} + \left[ {{H^ + }} \right]}{\alpha_1 + 2\alpha_2}  $$


```Python
m_Ca = 40*u.g/u.mol
m_C = 12*u.g/u.mol
m_O = 16*u.g/u.mol
m_Na = 23*u.g/u.mol
m_H = 1*u.g/u.mol
m_CaCO3 = m_Ca+m_C+3*m_O
m_Na2CO3 = 2*m_Na+m_C+3*m_O
ANC_Raw = 
from aide_design.play import*
from aguaclara_research.play import*
import aguaclara_research.Environmental_Processes_Analysis as epa

epa.ANC_closed
def Total_Carbonates(ANC,pH):
  return (ANC - 1 * u.eq/u.mol * Kw/invpH(pH) + 1 * u.eq/u.mol * invpH(pH)) / (epa.alpha1_carbonate(pH) + 2 * epa.alpha2_carbonate(pH))

C_T_Raw = Total_Carbonates(ANC,pH)
```
