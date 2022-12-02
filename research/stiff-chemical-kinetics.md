---
title:  "Stiff Chemical Kinetics"
layout: single
permalink: /research/stiff-chemical-kinetics/
author_profile: true
comments: true
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /assets/images/chemical.png
---


<h1>Physics-Informed Neural Networks and Functional Interpolation for Stiff Chemical Kinetics</h1>

<font size="3">ROBER, Chemical Akzo Nobel, Belousov–Zhabotinsky, and POLLU problems</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> This work presents a recently developed approach based on Physics-Informed Neural Networks (PINNs) for the solution of Initial Value Problems (IVPs), focusing on stiff chemical kinetic problems with governing equations of stiff ordinary differential equations (ODEs). The framework developed by the authors combines PINNs with the Theory of Functional Connections and Extreme Learning Machines in the so-called <a href="https://doi.org/10.1016/j.neucom.2021.06.015"><i>Extreme Theory of Functional Connections</i></a> (X-TFC). While regular PINN methodologies appear to fail in solving stiff systems of ODEs easily, we show how our method, with a single layer Neural Network (NN), is efficient and robust to solve such challenging problems without using artifacts to reduce the stiffness of problems. The accuracy of X-TFC is tested against several state-of-the-art methods, showing its performance both in terms of computational time and accuracy. A rigorous upper bound on the generalization error of X-TFC frameworks in learning the solutions of IVPs for ODEs is here provided for the first time. A significant advantage of this framework is its flexibility to adapt to various problems with minimal changes in coding. Also, once the NN is trained, it gives us an analytical representation of the solution at any desired instant in time outside the initial discretization. Learning stiff ODEs opens up possibilities of using X-TFC in applications with large time ranges, such as chemical dynamics in energy conversion, nuclear dynamics systems, life sciences, and environmental engineering.</div>
</font>


