---
title: Piezoelectricity in MEMS - An Introduction for Grad Students
categories:
- Mechanical
- Electrical
feature_image: "https://picsum.photos/2560/600?image=872"
---

## Introduction

Some materials are characterized by a crystal structure such that a net polarization forms if they get deformed. In other words, you can squeeze, bend, or twist a piezoelectric material to generate electrical charges.

This mechanical-to-electrical conversion is referred to as *direct piezoelectric effect*. The phenomenon is reciprocal, and you can mechanically deform the material by generating electric fields in it, for example by applying a voltage between electrodes placed on its top and bottom sides. In this case we are observing the *inverse piezoelectric effect*.

{% include figure.html image="/assets/images/Piezo-Grad/SchemaPiezo.gif" caption=" " width="500" height="500" %}

Unsuprisingly, this transduction mechanism is central to the MEMS industry, and is used by several device categories such as inertial sensors, MEMS microphones, and ultrasound transducers. 

Early piezoelectric MEMS devices were based on bulk materials, but thanks to improvements in microfabrication techniques we are now able to deposit piezoelectric materials such AlN and PZT in the form of thin films, which enable the miniaturized size and electronics integration of modern day sensors.

## The Constitutive Equations of Piezoelectricity

In (non-piezoelectric) solids mechanics, we normally use a matrix representation to linearly relate a stress vector to a strain vector. These vectors have 6 components, 3 for axial and 3 for shear stress/strain. Therefore a 6x6 *stiffness matrix* is used to calculate the contribution of each strain component to the stress vector:

$$T = cS$$

Where **T** is the stress vector, **c** is the stiffness matrix, and **S** is the strain vector.

If the material is piezoelectric, we can extend this equation to

$$T = c^ES - e^tE$$

Here **e** is a 3x6 matrix that couples the 3 electric field components in **E** to the 6x1 stress vector. The elements of **e** are the piezoelectric coefficients of the material.

So far, we have 9 unknowns and only 6 equations. To fully define our system we take the polarization equations and expand them to account for the direct piezoelectric effect:

$$D = \epsilon E  \xrightarrow{}  D = eS + \epsilon^S E$$

Where **D** is the polarization vector and $\pmb{\epsilon}$ is the 3x3 dielectric constants matrix.

Putting together the two equations above we obtain the *constitutive equations of piezoelectricity* in the stress-charge form. "Stress - Charge" simply denotes that **T** and **D** are chosen as dependent variables. 

The same equations can be expressed as having any combination of electrical and mechanical dependent variables, with the appropriate matrix transformations to obtain the correct coupling coefficients. 

In practice either the Stress-Charge form or the Strain-Charge form are used, depending on which one is convenient for the particular problem at hand:

$$
\begin{equation}
   Stress-Charge\:Form : \left\{
   \begin{array}
     . T = c^ES - e^tE \\
     D = e\;S + \epsilon^S E 
   \end{array}
   \right.
\end{equation}
$$

$$
\begin{equation}
   Strain-Charge\:Form : \left\{
   \begin{array}
     . \:S = s^ET + d^tE \\
     D = d\;T + \epsilon^T E 
   \end{array}
   \right.
\end{equation}
$$

Where **s** is the compliance matrix ($s=c^{-1}$) and **d** is the piezoelectric coefficients 3x6 matrix for the Strain - Charge form of the constitutive equations.

The correct units for the piezoelectric coefficients are $\frac{C}{m^2}$ for **e** and $\frac{C}{N}$ for **d**.

## How coefficients are extracted

You probably noticed that when we expand the purely mechanical and electrical equations to the piezoelectric constitutive equations, we add a superscript to the stiffness/compliance matrices and the dielectric constants matrix ($\pmb{c}^E$, $\pmb{s}^E$, $\pmb{\epsilon}^S$, or $\pmb{\epsilon}^T$ depending on the equations form). 

This means that the coefficients in the matrix were obtained while keeping that variable constant. For example, $\pmb{\epsilon}^T$ means that the dielectric constant coeffiecients were extracted in a measurement setup that ensured **T** stayed constant. 

This makes sense, as normally, in a non-piezoelectric material, you could obtain the dielectric constant by fitting a capacitance value to an I-V. However, if the measurement setup does not control for the changing stress, part of the I-V response will be given by the mechanical contribution, and the dielectric constant that fits the curve would not be correct.

Keeping the desired quantities unchanged is achieved by applying the approprate boundary conditions to your material. To maintain stress or strain constant during an electrical test, you would respectively allow the the material to freely deform (zero stress) or constrain it in such a way that no deformation takes place. 

{% include figure.html image="/assets/images/Piezo-Grad/piezo_boundary.png" caption=" " width="700" height="700" %}

Similarly, to keep **D** and **E** constant when extracting mechanical properties, you would either keep an open-circuit condition or keep a constant voltage drop across the material (for example with a short-circuit), respectively.

In general, the piezoelectric effect does not dominate the electrical or mechanical responses of sensors. This means that only a small portion of mechanical/electrical energy gets converted to the other domain (see $k_t^2$), so if you are looking for first order results you should be able to safely neglect this details.

However, if you are looking for a more precise derivation of a sensor or actuator response, you should make sure that the material properties you are using were extracted with boundary conditions that match those of your device.

Finally, if you have access to FEA, all of the above is automatically captured in the simulation. So what someone would commonly do is using first order results to define an appropriate design space for the device, and then use FEA if further refinement is needed.

## First Order Derivations Example

Before moving on to the example, we can review some relations that are used in this kind of probelm. While these relations are simple, it is useful to present them here if you are not used to these type of derivations.

While the constitutive equations are expressed in terms of stress, strain, electric field and polarization, in practice we are interested in their integrated versions, that is force, displacement, voltage and charge (or rather current).

To obtain voltage and displacement (**V** and **d<sub>0</sub>**), we integrate electric field and strain over a the distance of interest. This distance could be the thickness of the piezoelectric film (**h**) or the length of a beam:

$$ V = \int_0^hE dz $$

$$ d_0 = \int_0^hS dz$$

Charge and force (**Q** and **F**) are obtained by integrating over the area perpendicular to the **D** and **T** vectors, for example over the length **l** and width **w** of the transducer:

$$ Q = \int_0^l\int_0^wD dxdy $$

$$ F = \int_0^l\int_0^wT dxdy $$

As we will see in a moment, in our simplified cases derivations we will assume that the the fields above are constant along the geometries of interest, reducing the integrals to simple multiplications.

Current is obtained by taking the time derivative of charge. If we are studying the harmonic response of the transducer, this corresponds to multiplying the charge by **j$\pmb{\omega}$**:

$$ Q = Q_0 e^{j\omega t} $$

$$ i = \frac{dQ}{dt} = j\omega Q_0 e^{j\omega t} = j\omega Q $$

Since we are typically interested in the amplitude, we can drop the imaginary unit **j** that simply represents a 90 degrees phase shift: $ i = \omega Q $. 

#### Longitudinal Sensor Example

When using a transducer as a sensor, we convert a physical quantity into an electrical signal that can be read by a circuit.

A transducer operates in a longitudinal configuration when the input and output fields are parallel to each other. For example, we can see in the figure below that the components of the mechanical and electrical fields we are interested in are both along the vertical direction.

INSERT IMAGE

We begin the derivation by writing down a 1-dimensional piezoelectric constitutive equation. In this example we use a polarization equation in the Stress-Charge form:

$$ D_3 = \epsilon _3 E_3 + e_{33} S_3 $$

It is worth noting that this is an approximation to facilitate a quick derivation, and that full electrical response from the piezoelectric layer will always be captured by solving the complete system of constitutive equations. For example, strain in one direction can cause deformations along different axis through the poisson effect, which in turn contribute to the electrical signal we are interested in measuring. Sometimes these effects are lumped into an "effective piezoelectric coefficient", allowing us to study the approximated problem as we are doing now, while obtaining results that are closer to what is observed experimentally.

We obtain the following derivation by using some of the relations outlined above:

$$ \int_{-\frac{h}{2}}^{\frac{h}{2}} D_3 dz = \int_{-\frac{h}{2}}^{\frac{h}{2}} (\epsilon _3 E_3 + e_{33} S_3) dz $$

$$ D_3 h = \epsilon _3 E_3 h + e_{33} S_3 h $$

$$ D_3 = \epsilon _3 \frac{V}{h} + e_{33} d_{03} $$

$$ Q = \int_{A} D_3 dxdy = \epsilon _3 \frac{AV}{h} + e_{33} A d_{03} $$

$$ i = \frac{dQ}{dt} = \epsilon _3 \omega \frac{VA}{h} + e_{33} A \omega d_{03} $$

Assuming we are not applying any voltage on the sensor, the current response is entirely produced by mechanical excitation:

$$ i = \frac{dQ}{dt} = e_{33} A \omega d_{03} $$

If we wanted to obtain the voltage response, we can take the expression of charge and convert it into voltage through the capacitance $ C= \epsilon _3 \frac{A}{h}$ between the electrodes:

$$ Q=CV \xrightarrow{} V = \frac{e_{33}}{\epsilon _3} h d_{03} $$

Finally, we can express the displacement in terms of force through Hook's law ($T_3 = E_Y S_3$) by using the young modulus $\pmb{E_Y}$:

$$ V = \frac{e_{33}}{\epsilon _3} h d_{03} = \frac{e_{33}}{\epsilon _3} h^2 S_{3} = \frac{e_{33}}{\epsilon _3} h^2 \frac{T_{3}}{E_Y} = \frac{e_{33}}{\epsilon _3} \frac{h^2}{A} \frac{F_3}{E_Y}$$

With this derivations we can see how to jump from one expression to another depending on what is more convenient for the problem at hand.

It's important to keep in mind that the concept of Young modulus does not quite apply to anisotropic material such as piezoelectric crystals, and that $\pmb{E_Y}$ in our derivation stands as an "equivalent parameter". This numbers are often given for several materials. For example, it is common to use $\pmb{E_Y} = 400 GPa$ for thin film AlN.

