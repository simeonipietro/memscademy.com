---
title: Static Euler-Bernoulli Theory Derivation
categories:
- Mechanical
feature_image: "/assets/images/Euler-Bernoulli/Cantilever.png"
---

## Introduction

Often, MEMS structures can be decomposed into a set of beams connected with each other. Since it is a fundamental component of several anchor schemes, it useful to study how an individual beam deforms when an external load is applied to it.

Euler-Bernoulli beam theory offers a way to simply obtain a deformation shape for a given load + boundary conditions. The deformation shape is a function **w(x)** that tells you how much lateral displacement the beam experiences at any point **x** along its length.

In EB theory we neglect shear deformation. This is an important approximation because it allows us to imagine infinitesimal portions **dx** of the beam as perfectly rigid to shear deformation, and the overall beam displacemnt is solely the result of these portions sliding vertically agains each other. In other words, the cross-section of the beam remains perpendicular to the beam axis at all times.

This approximation is suitable for slender beams, i.e. beams that are much longer than their thickness, that undergo small deformations. If this conditions are not met, then Timoshenko beam theory is needed to obtain accurate results.

For now, we can focus on static bending (aka low frequency), so that we can neglect any inertial effect coming from the beam mass.

To develop the static EB theory of beam bending, we need to combine 3 equations:

- Equilibrium Equation #1, that relates the shear force **V** to the distributed force **q**: 

$$\frac{dV}{dx}=-q$$

- Equilibrium Equation #2, that relates the shear force to the bending moment **M**: 

$$V = \frac{dM}{dx}$$

- The Constitutive Equation that relates the bending moment to the radius of curvature **ρ** through material properties (the Young modulus **E**) and geometrical properties from the second moment of area **I**: 

$$M=-\frac{-EI}{\rho}$$

We will now derive the 3 equations, and then proceed to combine them to obtain the differential equation for the static EB theory.

## Equilibrium Equations #1 and #2

Let's look at an infinitesimal portion along the beam with length **dx**

{% include figure.html image="/assets/images/Euler-Bernoulli/Beamdx.png" caption="" width="500" height="500" %}

The total force acting on this portion of the beam is:

$$F_{tot} = q dx + V + dV - V$$

Since we are at equilibrium, the beam piece we are observing is not moving in space and the net force must be zero. Therefore, we get:

$$ \frac{dV}{dx} = -q, $$

which is our Equilibrium Equation #1.

In a similar way, the infinitesimal beam portion is not rotating either, and its total bending moment must also be equal to zero. The total bending moment is given by:

$$ M_{tot} = M + V dx + dV dx - (M + dM). $$

By neglecting $dV dx$ and setting $M_{tot}$ to zero, we obtain:

$$ \frac{dM}{dx} = V, $$

that is the Equilibrium Equation #2.


## Constitutive Equation

To derive the Constitutive Equation for beams bending, we reference the following figure:

{% include figure.html image="/assets/images/Euler-Bernoulli/Bend.png" caption="" width="520" height="800" %}

In the figure, **dx** is the portion of the beam under scrutiny before bending.

After bending, the neutral axis is the plane along the beam thickness that does not change length as a result of the deformation, while portions of the beam above or below the neutral plane must change their length to adjust for the curvature.

**dL** is the length of the beam infinitesimal element, and it is a function of the vertical coordinate **z**. In the wat we are setting up the problem, we have that $z=0$ corresponds to the neutral axis position, and that $dL(z=0) = dx$.

We define as **ρ** the radius of curvature calculated from the neutral axis, and **dΘ** is the infinitesimal angle defining the beam portion **dL** from the center of the curvature.

Using trigonometry, we know that 

$$dx = \rho sin(d\theta) \approx \rho d\theta.$$

Moving along the thickness of the beam, the radius of curvature also changes according to $\rho - z$, so using the trigonometric relation above we have that

$$ dL = (\rho - z) d\theta. $$

Combining the two relations we can get rid of **dΘ** and link **dx** to **dL**:

$$ dL = (1 - \frac{z}{\rho}) dx $$

By definition, the strain along the beam's thickness is

$$ \frac{dL - dx}{dx}, $$

and it can be written as a function of **z** by substituting the expression of **dL** we just obtained. In this way, we get 

$$ \epsilon_x = -\frac{z}{\rho}, $$

which gives us the stress as well thanks to Hook's Law:

$$ \sigma_x = -E \frac{z}{\rho}.$$

Now that we have the stress as a function of the vertical position and curvature, our next step is linking the bending moment **M** to the stress in the beam.

The internal moment about the neutral axis is given by summing all the forces perpendicular to the beam's cross-section times the distance from the neutral axis. This is equivalent to integrating the product of the stress and **z** over the cross-sectional area:

$$ M = \int_A\sigma_x z dA $$

Plugging the stress expression as a function of **z** and doing the integral, we obtain the Constitutive Equation

$$ M = - \frac{EI}{\rho}. $$ 

## Putting Everything Together

We can now take the Equilibrium Equations #1 and #2, and the Constitutive Equation, and combine them into a single differential equation.

By remembering that the radius of curvature of a curved line at a given point can be expressed as $\rho=\frac{d^2w}{dx},$ we obtain a differential equation that relates the deformation **w(x)** to the distributed load **q**: 

$$\frac{d}{dx^2}(EI\frac{d^2w}{dx^2})=q$$

If the the material and cross-section of the beam is constant over the length, i.e. constant flexural rigidity *EI*, the equation can be further simplified to 

$$EI \frac{d^4w}{dx^4}=q.$$

<br/><br/>
