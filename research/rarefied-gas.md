---
title:  "Rarefied-Gas Dynamics"
layout: single
permalink: /research/rarefied-gas/
author_profile: true
comments: true
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /assets/images/rarefied.png
---

<h1 style="text-align: center;"></h1>
<h2 style="text-align: center;">&nbsp;</h2>

<font size="2">
</font>


<h1>Physics-Informed Neural Networks for Rarefied-Gas Dynamics</h1>

<font size="3">Poiseuille, Couette, and Thermal Creep Flows in the BGK approximation</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> The Boltzmann equation with the Bhatnagar-Gross-Krook (BGK) collision model has been widely employed to describe the evolution of a gas through a kinetic theory. We propose a new Machine Learning approach to accurately and efficiently learn the solution of a class of problems in the transport theory of rarefied-gas dynamics, employing a particular Physics-Informed Neural Networks method called Extreme Theory of Functional Connections (X-TFC). According to X-TFC, the unknown function is approximated by the Constrained Expressions defined int the Theory of Functional Connections. Constrained Expressions are functionals (e.g., function of functions), which are the sum of a free function and a functional in which the constraints are analytically embedded. The constraints will therefore always be satisfied analytically, no matter what the free-chosen function is. In this work, a single-layer Neural Network trained with Extreme Learning Machine algorithm is employed. The proposed Machine Learning approach learns the solution of the Linear Boundary Value Problem arising from the Thermal Creep, Poiseuille, and Couette flow problems in the BGK approximation between two parallel plates of a channel, for a wide range of Knudsen numbers. The accuracy of X-TFC method is tested and compared with published benchmarks in literature.</div>
</font>


<hr>


<font size="6">Linearized Boltzmann Integro-Differential Equation</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> In this work, we look for a solution of following linear integro-differential equation:

\begin{equation}\label{pr1}
    u \frac{\partial Z(\tau,u)}{\partial \tau} + Z(\tau,u) = \int_{-\infty}^{\infty} \Psi(u') Z(\tau,u') du'
\end{equation}

where \(\tau \in [0,a]\) is the half-width of the channel (thanks to the spatial symmetry of the problem, which will ease the computational efforts), \(u\in(-\infty,\infty]\) is the cosine direction of the gas molecules, and \(Z(\tau,\mu)\) is the unknown function of the differential equation (DE), representing the velocity momentum. Depending on the boundary conditions, we can define three different flows, as shown in the following figure. The Thermal creep flow is a flow of a slightly rarefied gas caused by the temperature gradient along a wall, and when in the fluid the viscous forces dominate over inertial forces. The Poiseuille flow is a case of motion of a gas induced by a pressure gradient along the walls of the channel. The Couette flow is a case of motion of a gas induced by relative motion of two parallel plates with opposite velocities. The accommodation coefficient \(\alpha\) quantifies the interaction between a fluid and a solid (in this case the wall).


{% include figure image_path="/assets/images/flows.JPG" alt="this is a placeholder image" caption="Boundary conditions for the three different flows, with schematics of the physics of the problems." %}

The numerical results for <a href="https://doi.org/10.1007/s00033-022-01767-z"><i>Poiseuille flow</i></a> and <a href="https://doi.org/10.1063/5.0046181"><i>Thermal Creep flow</i></a> are published.






