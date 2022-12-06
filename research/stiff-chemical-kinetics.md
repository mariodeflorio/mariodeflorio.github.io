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

<font size="4">ROBER problem</font>
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
The values of the reaction rate constants are \(k_1 = 0.04\), \(k_2=3 \times 10^7\), and \(k_3 = 10^4\), thus varying in a range of 9 orders. This large variation of the parameters is the cause of the strong stiffness of the problem. 

In Table \ref{tab:table_rober} the solutions over $t = [0,4000]$ are reported. The results for $t = 0.4,40,4000$ are obtained with $L=11,9,10$, and $n_x = 11,9,10$, respectively, fixed step size $h=0.001$, and tolerance of $10^{-12}$. The training points are uniformly spaced in a linear time scale. The computational times for $t = 0.4,40,4000$ are $\approx 0.06$ , $6.7,$ and $580$ seconds, respectively. The average training errors for the three time instants are $7.3 \times 10^{-16}$,  $7.1 \times 10^{-17}$, and $3.2 \times 10^{-13}$, respectively.\\
In this table we can appreciate a good compatibility with the hybrid method presented in Ref. \cite{mehdizadeh2019new}, the MEBDF code \cite{mebdf}, and LSODE method presented by Shampine \cite{shampine2018numerical}, up to the $11^{th}$ significant digit.
\begin{table*}[h]
\begin{ruledtabular}
\begin{tabular}{ccccccccc}
$\boldsymbol{t}$ &$\qquad$ & $\boldsymbol{y_i}$ & & \makecell{X-TFC } &  Hybrid method & \makecell{MEBDF}  & \makecell{LSODE} \\ 
\hline
  $0.4$ & &  \makecell{ $y_1$ \\ $y_2$ \\ $y_3$ } & &  \makecell{ 
  9.85172113860984E-01 \\
  3.38639537897481E-05\\
  1.47940221852260E-02
  } & \makecell{
 9.85172113863231E-01 \\
 3.38639537890947E-05\\
 1.47940221854882E-02
  } & \makecell{
9.85172113861E-01 \\
3.38639737897E-05  \\
1.47940221854E-02   } & \makecell{
 9.8517E-01 \\
  3.3864E-05 \\
 1.4794E-02 
  }   \\
 \midrule
  $40$ & &  \makecell{$y_1$ \\ $y_2$ \\ $y_3$ } & &  \makecell{ 
7.15827068708193E-01\\
9.18553476412204E-06 \\
2.84163745757042E-01
  }  & \makecell{
7.15827068718994E-01 \\
9.18553476456752E-06\\
2.84163745746361E-01
  }   & \makecell{
7.15827068782E-01  \\
9.18553476564E-06 \\
2.84163745733E-01  } & \makecell{
 7.1582E-01 \\
  9.1851E-06 \\
  2.8417E-01 } \\
 \midrule
  $4000$ & &  \makecell{$y_1$ \\ $y_2$ \\ $y_3$  } & &  \makecell{ 
1.83202257727415E-01 \\
8.94237125021386E-07 \\
8.16796848001225E-01
  }  & \makecell{
 1.83202041873152E-01 \\
8.94235840002591E-07\\
8.16797063891367E-01
 } & \makecell{
 1.83202281848E-01 \\
 9.94237268115E-07  \\
 8.16794145152E-01
  } & \makecell{
 1.8320E-01  \\
 8.9423E-07  \\
 8.1680E-01
 }  
\end{tabular}
\caption{Species concentrations at times $t = 0.4,40,4000$ of X-TFC, Ref. \cite{mehdizadeh2019new}, MEBDF, and SDMM, for the ROBER problem.}
\label{tab:table_rober}
\end{ruledtabular}
\end{table*}






