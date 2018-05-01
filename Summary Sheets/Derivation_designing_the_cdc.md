# Deriving the Design Equations for the Linear Dose Controller/Chemical Dose Controller
This document will include the equation derivations required to design a CDC system. The most important restriction in this design process is maintaining linearity between head $h$ and flow $Q$, which is the entire purpose of the CDC. Recall that major losses under laminar flow scale with $Q$ and minor losses always scale with $Q^2$ Since it is impossible to remove minor losses from the system entirely, we will simply try to make minor losses very small compared to major losses by minimizing $\rm{\frac{minor \, losses}{major \, losses}}$. We will use the 'head loss trick' that was introduced in the Fluids Review section. Therefore, the elevation difference between the water level in the constant head tank and the end of the tube connected to the slider, $\Delta h$, is equal to the head loss between the two points, $h_L$. Therefore, $\Delta h = h_L = h_e + h_f$.

<img src="https://github.com/AguaClara/CEE4540_Master/blob/master/Summary%20Sheets/Images/CDC_derivation.jpg?raw=true" width=650>


$\color{red}{C^2}$  
$\color{blue}{C^2}$  
$\color{green}{C^2}$
