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
\begin{multline} <label>eqn:neg</label>
        -\mu_i \frac{\partial}{\partial \tau} I_m(\tau,-\mu_i) +  I_m(\tau,-\mu_i) = \\ =        \frac{\omega}{2}\sum_{l=m}^L \beta_l P_l^m(-\mu_i)  \sum_{k=1}^N  w_k P_l^m(-\mu_k) [(-1)^{l-m}I_m(\tau,\mu_k) + I_m(\tau, -\mu_k)] +  \frac{\omega}{2} e^{-\tau/\mu_0} \sum_{l=m}^L \beta_l P_l^m(\mu_0)P_l^m(-\mu_i)
\end{multline}
where the Gauss-Legendre quadrature rule is used to evaluate the integral in the range \([0,1]\).\\ Equations \ref{eqn:pos}-\eqref{eqn:neg} with the constraints \eqref{eqn:const} are a set of $N$ linear first-order ODEs that we will solve via TFC.




























