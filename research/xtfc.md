---
title:  "X-TFC"
layout: single
permalink: /research/xtfc/
author_profile: true
comments: true
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /assets/images/xtfc.png
---

<h1>Extreme Theory of Functional Connections</h1>

<font size="3">A physics-informed neural network method for solving parametric differential equations </font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> We present a novel, accurate, fast, and robust physics-informed neural network method for solving problems involving differential equations (DEs), called <i>Extreme Theory of Functional Connections</i>, or X-TFC. The proposed method is a synergy of two recently developed frameworks for solving problems involving DEs: the <i>Theory of Functional Connections</i> TFC, and the <i>Physics-Informed Neural Networks</i> PINN. Here, the latent solution of the DEs is approximated by a TFC constrained expression that employs a Neural Network (NN) as the free-function. The TFC approximated solution form always analytically satisfies the constraints of the DE, while maintaining a NN with unconstrained parameters. X-TFC uses a single-layer NN trained via the <i>Extreme Learning Machine</i> (ELM) algorithm. This choice is based on the approximating properties of the ELM algorithm that reduces the training of the network to a simple least-squares, because the only trainable parameters are the output weights. The proposed methodology was tested over a wide range of problems including the approximation of solutions to linear and nonlinear ordinary DEs (ODEs), systems of ODEs, and partial DEs (PDEs). The results show that, for most of the problems considered, X-TFC achieves high accuracy with low computational time, even for large scale PDEs, without suffering the curse of dimensionality. </div>
</font>

<hr>


<font size="6">X-TFC Solutions of Differential Equations</font>
<p><br></p>
<font size="3">
<div style="text-align: justify;"> Differential Equations are a powerful tool used for the mathematical modelling of various problems arising in scientific fields such as physics, engineering, finance, biology, chemistry, and oceanography, to name  few. We can express DEs, in their most general implicit form, as 
$$ \gamma f_t + \mathcal{N}\left[f;\lambda\right] = 0 $$
subject to certain constraints, where \( f(t,x)  \) represents the unknown solution, \( \mathcal{N}\left[ f ; \lambda \right] \) is a linear or nonlinear operator acting on \(f \) and parameterized by \( \lambda \), and the subscript \( t \) refers to the partial derivative of \(f \) with respect to \(t \).
<br>
The first step in our general physics-informed framework is to approximate the latent solution \(f \) with a constrained expression that analytically satisfies the constraints as follows,
$$
f(x; \Theta ) = f_{CE}(x, g(x); \Theta) = A(x; \Theta) + B(x, g(x); \Theta)
$$

where \(x = [t,x]^T \in \Omega \subseteq \mathbb{R}^{n+1}\) with \(t \geq 0\), \(\Theta = [\gamma, \lambda]^T \in \mathbb{P} \subseteq \mathbb{R}^{m+1}\),\(A (x; \Theta)\) analytically satisfies the constraints, and \(B(x, g (x); \Theta)\) projects the free-function \(g(x)\), which is a real valued function, onto the space of functions that vanish at the constraints. According to the X-TFC method, the free-function, \(g(x)\), is chosen to be a single layer feed forward NN, in particular, an ELM, that is
$$ g(x) = \sum_{j=1}^{L} \beta_j\sigma \left(w_j^Tx + b_j \right) = [ \sigma_1,...,\sigma_L ] \, \beta = \sigma^T \beta $$








