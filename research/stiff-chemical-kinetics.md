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


<hr>


<font size="6">Chemical Kinetics Equations and Time-Domain Decomposition</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> The recently developed Physics-Informed Neural Networks (PINN) is attracting a lot of attention among the numerical methods for solving Differential Equations. Despite its many advantages, its failure in solving stiff systems of Ordinary Differential Equations has been demonstrated. This study shows as merging PINN with the Theory of Functional Connections allows to obtain highly accurate solutions for Stiff non-linear Chemical Kinetics problems. The initial conditions are always analytically satisfied via particular expressions called Constrained Expressions, and the boundary-free solution is expanded with a Single-Layer Forward Neural Network, trained via Extreme Learning Machine algorithm. The proposed method is tested by solving classic, challenging chemical kinetics problems from the literature, and it can be applied to many chemical, biological, and nuclear systems subject to stiffness. The stiff Chemical Kinetics systems of equations we aim to solve in this <a href="https://doi.org/10.1063/5.0086649">work</a>, are IVPs of ODEs, having the following form:
\begin{equation}
    \begin{cases}
        \dfrac{d y_i(t)}{d t} = f_i(t, y_1,y_2,...,y_m) \\
        y_i(0) = {y_i}_0
    \end{cases}  
\end{equation}
with \(i = 1,2,...,m\), where the unknowns are the functions \(y_i(t)\), representing the time-dependent chemical species concentrations. The non-linear functions \(f_i\) and the initial conditions \({y_i}_0\) are known. The computational challenge for numerical methods with this kind of problem lies in the complex behavior and existence of sharp gradients in the unknown solution. This particular behavior is the so-called stiffness of a problem whose complete and precise definition has not yet been formulated. A problem can be considered stiff when a solution varies very slowly, but other nearby solutions can present steep changes. If a numerical method used to solve IVPs of ODEs is forced to decompose the time domain into multiple excessively small sub-intervals in relation to the smoothness of the exact solution in that domain, then that system of ODEs is stiff in that domain. Or even, a problem is considered being stiff if explicit methods are not capable of solving it.
<p><br></p>
For the convenience of the reader, the schematic of the figure below summarizes the all X-TFC process used in this work.

{% include figure image_path="/assets/images/stiff_scheme.jpg" alt="this is a placeholder image" caption="Schematic of the X-TFC algorithm to solve the Chemical Kinetics Equations." %}



Since we are facing long-time domain problems, a decomposition of the temporal domain into sub-intervals was performed to minimize the carryover of the error during the chemical reactions between the species. The temporal domain (whose decomposition is pictured in the following figure is divided into \(n\) time steps of equal size \(h = t_k - t_{k-1}\) for \(k=1,...,n\), each of which is discretized into \(n_x\) points.


{% include figure image_path="/assets/images/stiff_domain.jpg" alt="this is a placeholder image" caption="Decomposition of time domain in subintervals of length h." %}





