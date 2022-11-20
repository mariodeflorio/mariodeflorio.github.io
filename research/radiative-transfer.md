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
<div style="text-align: justify;"> In this <a href="https://doi.org/10.1016/j.jqsrt.2020.107384">work</a>, we aim to solve the Chandrasekhar's basic problem for Radiative Transfer for an incoming beam at $x = 0$, as shown in the follwing figure.
<p><br></p>
{% capture fig_img %}
![Foo]({{ "/assets/images/slab.JPG" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Geometry of the 1D slab for the considered Radiative Transfer Problem.</figcaption>
</figure>
<p><br></p>
<hr>

{% include feature_row id="feature_row1" type="left" %}


By following the notation used by <a href="https://doi.org/10.1016/S0022-4073(98)00144-7">Siewert</a>, the radiative transfer equation is written as
$$
\mu \frac{\partial}{\partial \tau} I(\tau,\mu,\phi) + I(\tau,\mu,\phi) = \frac{\omega}{4\pi} \int_{-1}^1 \int_0^{2\pi} p(\cos\Theta) I(\tau,\mu',\phi')\,d\phi'\,d\mu'
$$
where \(\Theta\) is the scattering angle, $\mu \in [-1,1]$ is the cosine of the polar angle , $\tau \in [0,\tau_0]$ is the optical variable, $\tau_0$ is the optical thickness, $\phi \in [0,2\pi]$ is the azimuthal angle, and $\omega \in [0,1]$ is the single scattering albedo.











