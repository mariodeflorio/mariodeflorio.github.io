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


{% include figure image_path="/assets/images/stiff_domain.jpg" alt="this is a placeholder figure" caption="Decomposition of time domain in subintervals of length h." %}

Thus, this decomposition into time steps leads to the solution of several consecutive IVPs: 
\begin{equation}
    \begin{cases}
        \dfrac{d y_i^{(k)}(t)}{d t} = f_i(t, y_1^{(k)},y_2^{(k)},...,y_m^{(k)}) \\
        y_i^{(k)}(0) = {y_i}_0^{(k)}
    \end{cases}
\end{equation}
with \(i = 1,2,...,m\). Initially, we solve the system of ODEs in the time step 1 by using the initial conditions \(y_i(t) = {y_i}_0\) given by the problem, thus finding the unknown solutions at time \(t_1\), which become the new initial conditions for the next step, and so on:
\begin{equation}
    {y_i}_0^{(k)} = {y_i}_f^{(k-1)}(t_k)
\end{equation}
Thus, the CE for the \(k\)-th time step is:
\begin{equation}
    y_i^{(k)}(t_k) = g(t_k) + \left( {y_i}_f^{(k-1)}(t_k) - g_0^{(k)} \right).
\end{equation}

<p><br></p>

Four chemical kinetics benchmark problems are analyzed, and numerically solved, and the solutions are compared with state-of-art methods' results. All the problems tackled in this manuscript have been coded in Matlab R2021a and run with an Intel Core i7 - 9700 CPU PC with 64 GB of RAM. Four benchmark problems in Chemical Kinetics are used for our simulations: the Robertson's chemical reaction model, as known as the ROBER problem, the Chemical Akzo Nobel problem, the Belousov-Zhabotinsky reaction, an air pollution problem, as known as POLLU problem. In the X-TFC framework, several hyperparameters can be adjusted to obtain accurate solutions, such as the number of training points, \(n_x\), the number of neurons, \(L\), the type of activation function, and the probability distribution where input weights and bias are sampled. For all the problems we have used a hyperbolic tangent (tanh) as a activation function, and the weights and biases are randomly sampled from  \(\mathcal{U}[-1,1]\). 


<hr>


<font size="5">ROBER problem</font>
<p><br></p>
<font size="3">

The first test case is given by the Robertson's system of equations, denoted as ROBER problem by Wanner and Hairer. This model has been developed to describe the chemical kinetics of the following autocatalytic reaction:
\begin{align*}
    A  & \qquad \xrightarrow{k_1} \qquad B , \\
    B + B  & \qquad \xrightarrow{k_2} \qquad C + B , \\
    B + C & \qquad \xrightarrow{k_3} \qquad A + C ,
\end{align*}
where \(k_1, k_2,\) and \(k_3\) are the reaction rate constants, and \(A\), \(B\), and \(C\) are the chemical species, whose evolution of concentrations \((y_1, y_2, y_3)\) is governed by the following system of 3 non-linear ODEs:
\begin{equation}
    \begin{cases}
      y_1' = - k_1 y_1 + k_3 y_2 y_3 \\
      y_2' = k_1 y_1 - k_2 y_2^2 - k_3 y_2 y_3 \\
      y_3' =  k_2 y_2^2
    \end{cases} \;  \text{s.t.}  \qquad
    \begin{cases}
        {y_1}(0) = 1 \\
         {y_2}(0) = 0 \\
          {y_3}(0) = 0
    \end{cases}
    \label{eq:rober}
\end{equation}
The values of the reaction rate constants are \(k_1 = 0.04\), \(k_2=3 \times 10^7\), and \(k_3 = 10^4\), thus varying in a range of 9 orders. This large variation of the parameters is the cause of the strong stiffness of the problem. In the figure below, we report X-TFC solutions compared with those obtained by the MATLAB stiff ode solver <i>ode15s</i>, which we consider here the true solution for our qualitative and quantitative comparison. The time span for producing this plot is \(t\in[10^{-5},10^5]\), and the training points are uniformly spaced in a logarithmic time scale. The step size used is \(h = 2000\), which allows us to obtain these results in a computational time of about \(0.015\) seconds. The average training error is \(8.5 \times 10^{-12}\). In the top three subplots, we can see how our solutions overlap with those computed by <i>ode15s</i>, with absolute error in the order of \(10^{-15} \div 10^{-05}\) (bottom subplots). This proves that X-TFC method is much more reliable in solving the ROBER problem than the regular PINN, which fails in this task, even if artifacts to reduce the stiffness of the ODE system are employed.

{% include figure image_path="/assets/images/rober.jpg" alt="this is a placeholder image" caption="Species concentration of ROBER problem computed with MATLAB ode15s and X-TFC (top) and absolute values of the errors between the two methods (bottom)." %}


<hr>


<font size="5">Belousov-Zhabotinsky reaction</font>
<p><br></p>
<font size="3">


Another test case we consider here is the Belousov-Zhabotinsky reaction mechanism, which can be represented by the following scheme of homogeneous chemical reactions in symbolic form:
\begin{equation}
    \begin{aligned}
    A + Y\qquad & \xrightarrow{k_1} \qquad X ,\\
    X + Y\qquad & \xrightarrow{k_2} \qquad P, \\
    B + X\qquad & \xrightarrow{k_3} \qquad 2X + Z, \\
    2X\qquad & \xrightarrow{k_4} \qquad Q, \\
    Z\qquad & \xrightarrow{k_5} \qquad Y, 
    \end{aligned}
\end{equation}
where the reaction rate constants are \(k_1 = 4.72\), \(k_2 = 3 \times 10^9\), \(k_3 = 1.5 \times 10^4\), \(k_4 = 4 \times 10^7\), and \(k_5 = 1\) \(\left[\frac{L}{mol \cdot s }\right]\). The letters denote the species taking part of the reactions, and the initial concentrations at time \(t=0\) (expressed in \(\frac{mol}{L}\)) are:
\begin{equation*}
    Y = X = P = Q = 0, \qquad  A = B = 0.066, \qquad  Z = 0.002 \quad .
\end{equation*}
The system of ODEs modeling the Belousov-Zhabotinsky reaction is
\begin{equation}
    \begin{cases}
      y_1' =  - k_1 y_1 y_2 \\
      y_2' = - k_1 y_1 y_2 - k_2 y_3 y_2 +  k_5 y_6 \\
      y_3' = - k_2 y_3 y_2 +  k_3 y_3 y_5 - 2k_4 y_3^2 + k_1 y_1 y_2 \\
      y_4' =  k_2 y_3 y_2 \\
      y_5' =  -  k_3 y_5 y_3 \\
      y_6' =    k_3 y_5 y_3 - k_5 y_6  \\
      y_7' =  k_4 y_3^2
    \end{cases}
\end{equation}
subject to \(y_i(0) = \left( 0.066, 0 , 0,0,0.066,0.002,0  \right)^T\), for \( t \in [0,40]\). The following figure shows the simulation results obtained using X-TFC with \(L=20\), \(n_x = 20\), fixed step size \(h=0.01\), and tolerance of \(10^{-9}\), for three different integration times. The training points are uniformly spaced in a linear time scale, and the computational times for \(t =[0,40]\) is \(\approx 3\) seconds. One can clearly see the rapid "jumps" in the solutions with a period of approximately \(16 s\). The qualitative analogy with the converged solutions presented by the Gear's method and the Almost Runge-Kutta and Aluffi-Pentini methods (obtained with CPU times of \(\approx 9 s.\)) is evident. As one can see from the figure below (c), we can extend the integration time to a very large range (e.g., 5000 seconds) while continuing to obtain accurate solutions without negative values.

{% include figure image_path="/assets/images/belusov.JPG" alt="this is a placeholder image" caption="Species concentrations (Y,P,Z,Q) of Belousov-Zhabotinsky reaction computed with X-TFC for integration time of 40 seconds (a) and 120 seconds (b). A simulation for integration time of 5000 seconds shows the robustness of X-TFC method for very large time domains (c)." %}



Two MATLAB functions, <i>ode15s</i> and <i>ode15i</i> have been implemented to compare their results with X-TFC framework. The solutions of the three methods for all the 7 species reacting in the chemical process are reported in the following figures, for the integration times of 40 seconds and 120 seconds, respectively. Both solutions of <i>ode15s</i> and <i>ode15i</i> have been obtained with time step \(h=0.0001\) and tolerance of \(10^{-9}\). We can see that <i>ode15s</i> is able to find the solution only for the first jump, after which it fails, keeping the species concentrations constant in time. From the figure for \(40 s\) domain, we can note that <i>ode15i</i> captures the solutions for the first jump, but with a delay of about 1 second for the second jump and about 3 seconds for the third jump. By extending the time interval to \(120 s\), we see that after the third jump, it stops working, keeping the species concentrations constant in time.

{% include figure image_path="/assets/images/belusov40.jpg" alt="this is a placeholder image" caption="Species concentrations of Belousov-Zhabotinsky reaction computed with X-TFC, ode15i, and ode15s, for integration time of 40 seconds." %}

{% include figure image_path="/assets/images/belusov120.jpg" alt="this is a placeholder image" caption="Species concentrations of Belousov-Zhabotinsky reaction computed with X-TFC, ode15i, and ode15s, for integration time of 120 seconds." %}










