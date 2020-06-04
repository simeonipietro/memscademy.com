---
title: Euler-Bernoulli Made Easy - Part 1
categories:
- Mechanical
- Beam Theory
- Euler - Bernoulli
feature_image: "https://picsum.photos/2560/600?image=872"
---

## Introduction

Often, MEMS structures can be decomposed in a set of beams connected with each other. Since it is a fundamental component of several anchor schemes, it useful to study how an individual beam deforms when an external load is applied to it.

Euler-Bernoulli beam theory offers a way to simply obtain a deformation shape for a given load + boundary conditions. The deformation shape is a function **w(x)** that tells you how much lateral displacement the beam experiences at any point **x** along its length.

In EB theory we neglect shear deformation. This is an important approximation because it allows us to imagine infinitesimal portions **dx** of the beam as perfectly rigid to shear deformation, and the overall beam displacemnt is solely the result of these portions sliding vertically agains each other. In other words, the cross-section of the beam remains perpendicular to the beam axis at all times.

This approximation is suitable for slender beams, i.e. beams that are much longer than their thickness, that undergo small deformations. If this conditions are not met, then Timoshenko beam theory is needed to obtain accurate results.

For now, we can focus on static bending (aka low frequency), so that we can neglect any inertial effect coming from the beam mass.

To develop the static EB theory of beams bending, we need to combine 3 equations:

- Equilibrium equation #1, that relates the shear force to the distributed force **q**: 

$$\frac{dV}{dx}=-q$$

- Equilibrium equation #2, that relates the shear force **V** to the bending moment **M**: 

$$V = \frac{dM}{dx}$$

- The constitutive equation that relates the bending moment to the radius of curvature **ρ** through material properties (the Young modulus **E**) and geometrical properties from the second moment of area **I**: 

$$M=-\frac{-EI}{\rho}$$

## Equilibrium Equations #1 and #2

Let's look at an infinitesimal portion along the beam with length **dx**

{% include figure.html image="https://picsum.photos/600/800?image=894" caption="" width="300" height="800" %}

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



## Putting Everything Together

We can now take the equilibrium equations #1 and #2, and the constitutive equation, and combine them into a single differential equation.

By remembering that the radius of curvature of a curved line at a given point can be expressed as $\rho=\frac{d^2w}{dx},$ we obtain a differential equation that relates the deformation **w(x)** to the distributed load **q**: 

$$\frac{d}{dx^2}(EI\frac{d^2w}{dx^2})=q$$

If the the material and cross-section of the beam is constant over the length, i.e. constant flexural rigidity *EI*, the equation can be further simplified to 

$$EI \frac{d^4w}{dx^4}=q.$$
