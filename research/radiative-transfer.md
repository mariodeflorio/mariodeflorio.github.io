---
title:  "Radiative Transfer"
layout: single
permalink: /research/radiative-transfer/
author_profile: true
comments: true
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /assets/images/radiative.png
feature_row1:
  - image_path: /assets/images/slab.JPG
    excerpt: 'A physics-informed neural network method for solving parametric differential equations.'
---


<h1>Solutions of Chandrasekhar's Basic Problem in Radiative Transfer</h1>

<font size="3">via Theory of Functional Connections</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> We present a novel approach to solving Chandrasekhar's problem in radiative transfer using the recently developed <a href="https://doi.org/10.3390/math5040057"><i>Theory of Functional Connections</i></a>}. The method is designed to elegantly and accurately solve the Linear Boundary Value Problem from the angular discretization of the integrodifferential Boltzmann equation for Radiative Transfer. The proposed algorithm falls under the category of numerical methods for the solution of radiative transfer equations. This new method's accuracy is tested via comparison with the published benchmarks for Mie and Haze L scattering laws.</div>
</font>




<hr>


<font size="6">Radiative Transfer Equation: Problem formulation</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> In this <a href="https://doi.org/10.1016/j.jqsrt.2020.107384">work</a>, we aim to solve the Chandrasekhar's basic problem for Radiative Transfer for an incoming beam at \(x = 0\), as shown in the follwing figure.
<p><br></p>



{% include figure image_path="/assets/images/slab.JPG" alt="this is a placeholder image" caption="Geometry of the 1D slab for the considered Radiative Transfer Problem." %}





By following the notation used by <a href="https://doi.org/10.1016/S0022-4073(98)00144-7">Siewert</a>, the radiative transfer equation is written as
$$
\mu \frac{\partial}{\partial \tau} I(\tau,\mu,\phi) + I(\tau,\mu,\phi) = \frac{\omega}{4\pi} \int_{-1}^1 \int_0^{2\pi} p(\cos\Theta) I(\tau,\mu',\phi')\,d\phi'\,d\mu'
$$
where \(\Theta\) is the scattering angle, \(\mu \in [-1,1]\) is the cosine of the polar angle, \(\tau \in [0,\tau_0]\) is the optical variable, \(\tau_0\) is the optical thickness, \(\phi \in [0,2\pi]\) is the azimuthal angle, and \(\omega \in [0,1]\) is the single scattering albedo.

The addition theorem to express the phase function in terms of Legendre polynomials:
$$
p(\cos\Theta) = \sum_{l=0}^L \beta_l P_l (\cos\Theta)
$$
where the \(\beta_l\) are the Legendre coefficients in the \(L^{th}\) order expansion of scattering law.<br>
The problem is subject to the following constraints/boundary conditions:
$$
\begin{cases} 
   I(0,\mu,\phi) = S_0 \pi \delta(\mu - \mu_0)\delta(\phi - \phi_0)    & \qquad   \text{for} \quad \mu > 0 \\
   I(\tau_0,\mu,\phi) = 0   & \qquad  \text{for} \quad \mu < 0
\end{cases}
$$
where \(S_0 \pi\) represents the flux carried by a source beam across a plane normal to the direction of incidence, and \(\mu_0\) and \(\phi_0\) determine the inclination of the source beam. The solution is defined as the sum of collided (or diffuse) term and uncollided term:
$$
I(\tau,\mu,\phi) = I^*(\tau,\mu,\phi) + I^o(\tau,\mu,\phi),
$$
where the superscript \(^*\) refers to the collided beam, and the superscript \(^o\) refers to the uncollided beam. The problem is therefore split into two parts. The uncollided term solves the following first order PDE:
$$
\mu \frac{\partial}{\partial \tau} I^o(\tau,\mu,\phi) + I^o(\tau,\mu,\phi) = 0
$$
subject to:
$$
\begin{cases}
    I^o(0,\mu,\phi) = S_0 \pi \delta(\mu - \mu_0)\delta(\phi - \phi_0) & \qquad   \text{for} \quad \mu > 0 \\
     I^o(0,\mu,\phi) = 0  & \qquad  \text{for} \quad \mu < 0
\end{cases}
$$
where \(\mu \in (0,1]\). This problem has the following analytical solutions:
$$
\begin{cases}
    I^o(\tau,\mu,\phi) = S_0 \pi \delta(\mu - \mu_0)\delta(\phi - \phi_0) e^{-\tau / \mu} & \qquad   \text{for} \quad \mu > 0 \\
     I^o(\tau,\mu,\phi) = 0 & \qquad   \text{for} \quad \mu < 0
\end{cases}
$$
Plugging into the the unkown solution, we obtain the following:
$$
I(\tau,\mu,\phi) = I^*(\tau,\mu,\phi) +  S_0 \pi \delta(\mu - \mu_0)\delta(\phi - \phi_0) e^{-\tau / \mu}
$$
The relation of the phase function and the scattering angle can be expressed using the <i>Addition Theorem of the Spherical Harmonics</i>:
$$
    p(\cos\Theta) = \sum_{m=0}^L (2-\delta_{0,m}) \sum_{l=m}^L \beta_l P_l^m(\mu')P_l^m(\mu)\cos[m(\phi'-\phi)]
$$
where the following expression is used to denote the normalized function:
$$
    P_l^m(\mu) = \Biggl[\frac{(l-m)!}{(l+m)!}\Biggr](1-\mu^2)^{m/2}\frac{d^m}{d\mu^m}P_l(\mu)
$$
Thus, we can express the diffuse component as a Fourier expansion with \(L\) terms. That is:
$$
     I^*(\tau,\mu,\phi) = \frac{1}{2} \sum_{m=0}^{L} (2-\delta_{0,m})  I_m(\tau,\mu) \cos[m(\phi - \phi_0)] 
$$
The $m^{th}$ Fourier component satisfies the following linear integro - $1^{st}$ order PDE:
$$
\mu \frac{\partial}{\partial t} I_m(\tau,\mu) + I_m(\tau,\mu) = \frac{\omega}{2}\sum_{l=m}^L \beta_l P_l^m(\mu) \int_{-1}^1 P_l^m(\mu')I_m(\tau,\mu')d\mu' + Q^m(\tau,\mu),
$$
where \(Q\) is the inhomogeneous source term:
$$
Q^m(\tau,\mu) = \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu)
$$
Thus, the problem to solve is the following:
$$
    \mu \frac{\partial}{\partial t} I_m(\tau,\mu) + I_m(\tau,\mu)  = \frac{\omega}{2}\sum_{l=m}^L \beta_l P_l^m(\mu) \int_{-1}^1 P_l^m(\mu')I_m(\tau,\mu')d\mu' + \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu)
$$
Subject to:
$$
  \begin{cases} 
   I_m(0,\mu) = 0  & \qquad   \text{for} \quad \mu > 0 \\
   I_m(\tau_0,\mu) = 0   & \qquad  \text{for} \quad \mu < 0
  \end{cases}
$$
Via discretizing the angle \(\mu\) into \(N\) points in the interval \((0,1]\) according to the Gauss-Legendre quadrature scheme:
$$
    \mu \quad \longrightarrow \quad \mathbf{\mu} = \{ \mu_i \}_{i=1}^N
$$
it follows that:
$$
I_m(\tau,\mu) \quad \longrightarrow \quad \mathbf{I}_m(\tau) = \{ I_m(\tau,\mu_i)\}_{i=1}^N \qquad
$$
By suppressing some of the \(m\) indexes, and splitting the problem into two equations, for positive and negative values of \(\mu\), we get the following set of equations:
$$
\begin{multline} \label{eqn:pos}
        \mu_i \frac{\partial}{\partial \tau} I_m(\tau,\mu_i) +  I_m(\tau,\mu_i)  =     \\ =\frac{\omega}{2}\sum_{l=m}^L \beta_l P_l^m(\mu_i)  \sum_{k=1}^N w_k P_l^m(\mu_k) [I_m(\tau,\mu_k) +(-1)^{l-m} I_m(\tau, -\mu_k)] +  \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu_i)
\end{multline}
$$
\begin{multline}
        -\mu_i \frac{\partial}{\partial \tau} I_m(\tau,-\mu_i) +  I_m(\tau,-\mu_i) = \\ =        \frac{\omega}{2}\sum_{l=m}^L \beta_l P_l^m(-\mu_i)  \sum_{k=1}^N  w_k P_l^m(-\mu_k) [(-1)^{l-m}I_m(\tau,\mu_k) + I_m(\tau, -\mu_k)] +  \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(-\mu_i)
\end{multline}
where the Gauss-Legendre quadrature rule is used to evaluate the integral in the range \([0,1]\). Now we got a set of \(N\) linear first-order ODEs that we will solve via TFC.

<hr>


<font size="6">TFC Formulation of the Problem</font>
<p><br></p>


In our case, we assume to have one constraint in one point; hence, according to \eqref{eqn:conexp}, \(y(\tau)\) can be expressed as following:
\begin{equation}
    y(\tau) = g(\tau) + \eta  p(\tau)
\end{equation}
We set \(p(\tau) = 1\) and the function \(g(\tau)\) as an expansion of Chebyshev polynomials as follows:
\begin{equation}
    g(\tau) =  {h}^T(\tau)   {\xi}
\end{equation}
Since Chebyshev Polynomials are used as basis functions, we need to define a new variable \(x\) that ranges in \([-1,1]\). The new \(x\) variable is defined as \(x = c\tau -1\), where \(c\) is the mapping coefficient:
\begin{equation*}
    c = \frac{x_f - x_0}{\tau_f - \tau_0}
\end{equation*}
Considering the new independent variable, we have:
\begin{equation}
\begin{cases}
    I_m(\tau,\mu) = I_m(x,\mu) \\
    \dfrac{\partial}{\partial \tau} I_m(\tau,\mu) = c \dfrac{\partial}{\partial x} I_m(x,\mu) 
\end{cases}
\end{equation}
To simplify the notation, for the remainder of this manuscript, we give for granted the \(x\) and \(\mu\) dependency and write the terms for the forward and backward flux as \(I_m^+\) and \(I_m^-\), respectively. Thus, our problem becomes:
\begin{equation}
        c\mu_i \frac{\partial}{\partial x} I_m^+ + I_m^+ =  \frac{\omega}{2} \sum_{l=m}^L \beta_l P_l^m(\mu_i) \sum_{k=1}^N w_k P_l^m(\mu_k) [I_m^+ +(-1)^{l-m} I_m^-] + \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu_i)
\end{equation}
\begin{equation}
        -c\mu_i \frac{\partial}{\partial x} I_m^- + I_m^- =  \frac{\omega}{2} \sum_{l=m}^L \beta_l P_l^m(-\mu_i) \sum_{k=1}^N w_k P_l^m(-\mu_k) [(-1)^{l-m}I_m^+ + I_m^-] + \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(-\mu_i)
\end{equation}
Subject to:
\begin{equation} 
  \begin{cases} 
   I_m^+(0) = I_0^+ =0  \\
   I_m^-(\tau_0) = I_f^- = 0   
  \end{cases}
\end{equation}
Our constrained expressions, for forward and backward terms, are:
\begin{equation}
    I_m^{\pm}(x) = g^{\pm}(x) + \eta^{\pm}
\end{equation}
Therefore, by using the boundary conditions to calculate $\eta^+$ and $\eta^-$, we obtain:
\begin{equation*}
   I_0^+ = 0 = g^+_0 + \eta^+   \qquad   \longrightarrow \quad \eta^+ = -g^+_0 
\end{equation*}
\begin{equation*}
   I_f^- = 0 = g^-_f + \eta^-   \qquad   \longrightarrow \quad  \eta^- = -g^-_f
\end{equation*}
and then:
\begin{equation*}
    I_m^+(x) = g^+(x) - g^+_0
\end{equation*}
\begin{equation*}
    I_m^-(x) = g^-(x) - g^-_f
\end{equation*}
Finally, we get the CEs for the fluxes in the following form:
\begin{equation} \label{sol}
    I_m^+ = ( {h}^T -  {h_0}^T)   {\xi}^+  \qquad ;  \qquad I_m^- = ( {h}^T -  {h_f}^T)   {\xi}^-,
\end{equation}
where \( {\xi}^+\) and \( {\xi}^-\) are the unknowns to be computed via LS.
Plugging \eqref{sol} into our DEs, we get:
\begin{multline}
        c\mu_i    {h'}^T  {\xi}_i^+ + ( {h} - {h_0} )^T   {\xi}_i^+ = \\ =
        \frac{\omega}{2} \sum_{l=m}^L \beta_l P_l^m(\mu_i) \sum_{k=1}^N w_k P_l^m(\mu_k)  [( {h} - {h_0} )^T   {\xi}_k^+ +(-1)^{l-m} ( {h} - {h_f})^T   {\xi}_k^-]  + \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu_i)
\end{multline}
\begin{multline}
        - c\mu_i     {h'}^T  {\xi}_i^- + ( {h} - {h_f} )^T    {\xi}_i^- = \\ =
        \frac{\omega}{2} \sum_{l=m}^L  \beta_l P_l^m(-\mu_i) \sum_{k=1}^N  w_k  P_l^m(-\mu_k)  [(-1)^{l-m}( {h} - {h_0} )^T   {\xi}_k^+ + ( {h} - {h_f} )^T   {\xi}_k^-] +  \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(-\mu_i)
\end{multline}
Reorganizing all the terms we get:
\begin{multline}
        (c\mu_i  {h'} +   {h} - {h_0} )^T   {\xi}_i^+  - \frac{\omega}{2} \sum_{l=m}^L   \beta_l  P_l^m(\mu_i)  \sum_{k=1}^N w_k P_l^m(\mu_k)  [( {h} - {h_0} )^T   {\xi}_k^+ +(-1)^{l-m}  ( {h} - {h_f} )^T   {\xi}_k^-]  =   \\  = \frac{\omega}{2} e^{-\tau/\mu_0}  \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu_i)
\end{multline}
\begin{multline}
        (-c\mu_i  {h'} +  {h} - {h_f} )^T   {\xi}_i^- - \frac{\omega}{2} \sum_{l=m}^L  \beta_l  P_l^m(-\mu_i)  \sum_{k=1}^N w_k P_l^m(-\mu_k) [(-1)^{l-m}( {h} - {h_0} )^T   {\xi}_k^+ +  ( {h} - {h_f} )^T   {\xi}_k^-]  =  \\  =  \frac{\omega}{2} e^{-\tau/\mu_0}  \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(-\mu_i)
\end{multline}
For the sake of simplicity, we write the inhomogeneous term as:
\begin{equation*}
    \qquad  { {b_i^+}} = \frac{\omega}{2}e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(\mu_i) \qquad \qquad \qquad \qquad    { {b_i^-}} = \frac{\omega}{2}e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(-\mu_i)
\end{equation*}
So, the two problems become:
\begin{equation} \label{probp}
        (c\mu_i  {h'} +  {h} - {h_0} )^T    {\xi}_i^+   - \frac{\omega}{2} \sum_{l=m}^L   \beta_l P_l^m(\mu_i) \sum_{k=1}^N w_k P_l^m(\mu_k)  [( {h} - {h_0} )^T   {\xi}_k^+ +(-1)^{l-m} ( {h} - {h_f} )^T   {\xi}_k^-] =    {b_i^+}
\end{equation}
\begin{equation}\label{probn}
        (-c\mu_i  {h'} +  {h} - {h_f} )^T    {\xi}_i^-   - \frac{\omega}{2} \sum_{l=m}^L  \beta_l P_l^m(-\mu_i) \sum_{k=1}^N w_k P_l^m(-\mu_k)  [(-1)^{l-m}( {h} - {h_0} )^T   {\xi}_k^+ + ( {h} - {h_f} )^T   {\xi}_k^-] =     {b_i^-}
\end{equation}

which is a problem of the type:
\begin{equation}
     {A}   {\xi} =  {B}
\end{equation}

That is, the original Linear BVP has been reformulated as an <i>unconstrained</i> optimization problem. In this case, $ {\xi}$ is calculated with only one direct pass via LS methods. That is:
\begin{equation}\label{eq:LS}
     {\xi} = \left(  {A}^T  {A} \right)^{-1}  {A}^T  {B}
\end{equation}
Once \( {\xi}\) are computed, the final solutions are built according to the constrained expressions. After finding the solutions for all \(m^{th}\) Fourier components (with \(m = 0,1,...,L\)), we can compute the diffuse terms expressed as:
\begin{equation}
    I(\tau,\mu, \phi) = \frac{1}{2} \sum_{m=0}^L (2-\delta_{0,m}) {I_m}(\tau,\mu) \cos[m(\phi - \phi_0)]
\end{equation}
\begin{equation}
    I(\tau,-\mu, \phi) = \frac{1}{2} \sum_{m=0}^L (2-\delta_{0,m}) {I_m}(\tau,-\mu) \cos[m(\phi - \phi_0)]
\end{equation}
For the convenience of the reader, the all process described in this section is summarized in the schematic of the following figure.
\begin{figure}[H]
    \centering\includegraphics[width=1\linewidth]{diagrams_imagines.jpg}
    \caption{Schematic of the Theory of Functional Connections algorithm to solve Chandrasekhar's Basic Problem in Radiative Transfer.}
    \label{rte_summary}
\end{figure}


























