---
layout: project
title: ENGRD2020-Project
description: Mechanism Design
technologies: [N/a]
image: /assets/images/engrd2020-sketch.jpg
math: true
---

### 1. Problem Definition
**Objective:**
Given a 2D design space of $150 \text{ cm} \times 50 \text{ cm}$, the goal is to design a lifting mechanism capable of raising the maximum possible weight to the highest possible vertical position.

**Constraints & Parameters:**
* **Design Space:** $L_{space} = 1.5\text{ m}$, $H_{space} = 0.5\text{ m}$.
* **Components:** One rigid bar (fixed length), three pin supports (two grounded), and one linear actuator.
* **Actuator Selection:** I selected the Tolomatic IMASS integrated motor actuator for its stroke-to-force ratio:
    * Stroke Range: $152.4 \text{ mm} - 457.2 \text{ mm}$
    * Base Weight: $24.8 \text{ kg}$
    * Peak Thrust: $35.8 \text{ kg} \approx 351 \text{ N}$

**Design Degrees of Freedom (DOF):**
The mechanism consists of a grounded single-DOF linkage system. 
* Three links (Ground, Bar, Actuator Piston).
* Three joints (Pin at A, Pin at B, Pin at C).
* Linear actuator This introduces 1 DOF, defined by the extension length of the actuator.

### 2. Rigid Body Analysis
To determine the maximum load capacity, I first treated the main lifting bar $AC$ as a rigid body.

**System Configuration:**
* Bar $AC$: Length $L = 0.5\text{ m}$. Pinned to the ground at $A$.
* Actuator $BC$: Pinned to the ground at $B$ and connected to the bar tip at $C$.
* Load: Weight $W$ hangs from tip $C$.

![Photo of Sketch]({{ "/assets/images/engrd2020-sketch.jpg" | relative_url }}){: .inline-image-l}


To maximize the vertical lift, the bar $AC$ should be vertical at full extension. ($h_{max} = 0.5\text{ m}$). 

When the actuator is at max stroke:
* $L_{act, max} = 142 + 457.2 = 599.2\text{ mm}$.
* The ground distance $d$ between pins $A$ and $B$ is calculated as $d = \sqrt{L_{act, max}^2 - L_{bar}^2} \approx 330.2\text{ mm}$.

When the actuator is at min stroke:
* $L_{act, min} = 142 + 152.4 = 294.4\text{ mm}$.
* Using the Law of Cosines, we find the angle of the bar and the resulting minimum height $h_{min} \approx 0.283\text{ m}$.

Therefore, the Total Lift: $\Delta h = h_{max} - h_{min} \approx 0.217\text{ m}$.

The limiting factor for the weight is the moment equilibrium about the main support pin $A$. The actuator acts as a two-force member, applying force $F_{act}$ along the line $BC$.

$$\sum M_A = 0$$

$$\vec{r}_C \times \vec{F}_{act} + \vec{r}_C \times \vec{W} = 0$$

The torque required to lift the weight is greatest when the "moment arm" of the weight is largest (i.e., when the bar is lowest). At the lowest position ($\theta_{bar} \approx 34.4^\circ$ from horizontal), the transverse component of the weight is maximized relative to the actuator's mechanical advantage. Based on my calculation, the actuator force required is approximately $1.3 \times$ the weight $W$.

Given the Peak Thrust $F_{max} = 351\text{ N}$:
$$W_{max} = \frac{F_{max}}{1.3} \approx 270.6 \text{ N}$$


### 3. Deformable Body Analysis

In this stage, the bar $AC$ is no longer treated as rigid. It is modeled as a beam subject to bending due to the transverse components of the applied forces.

##### A. Maximum Deflection Analysis
**Assumptions:**
1.  We model the bar as a fixed-free beam. One end is pinned at $A$,  the other free end applies the load.
2.  We consider the "worst-case" loading scenario: when the bar is horizontal (maximum moment arm for gravity).


The total transverse load $P$ at the tip $C$ consists of the Weight $W$. $P = W \approx 270.6 \text{ N}$

For a  beam with a point load at the free end, the maximum vertical deflection $\delta_{max}$ occurs at the tip: $\delta_{max} = \frac{P L^3}{3 E I}$


![Photo of Sketch]({{ "/assets/images/engrd2020-deflection.png" | relative_url }}){: .inline-image-r style="width: 800px"}

Where:
* $P = 270.6\text{ N}$
* $L = 0.5\text{ m}$
* $E$ = Young's Modulus of the material.
* $I$ = Area Moment of Inertia of the cross-section.



##### B. Material Selection and Cross-Section Design
**Constraint:** :The vertical deflection must be below 2% of the length. 
$$\delta_{limit} = 0.02 \times 0.5\text{ m} = 0.01\text{ m} = 10\text{ mm}$$


Rearranging the deflection formula to solve for the required stiffness $EI$:

$$EI \geq \frac{P L^3}{3 \delta_{limit}}$$

$$EI \geq \frac{270.6 \cdot (0.5)^3}{3 \cdot 0.01} = \frac{33.825}{0.03} \approx 1127.5 \text{ N}\cdot\text{m}^2$$

**Material Choice: Aluminum 6061-T6**
* Aluminum is highly mass-efficient. It has a high strength-to-weight ratio compared to steel, which is ideal for a lifting arm where self-weight should be minimized.
* Young's Modulus ($E_{Al}$): $70 \text{ GPa} = 70 \times 10^9 \text{ Pa}$.
* Density ($\rho_{Al}$: $2710kg/m^3$)


**Cross-Section Selection: $40 \times 40 \times 2$ mm Tube**

The required moment of inertia: $I_{req} \geq \frac{1127.5}{70 \times 10^9} \approx 1.61 \times 10^{-8} \text{ m}^4 = 16,107 \text{ mm}^4$

To achieve high stiffness with low mass, I choose a hollow suqare tube rather than a solid rod.
We use a $40\text{ mm} \times 40\text{ mm}$ square aluminum tube with $2\text{ mm}$ wall thickness.

![Photo of Sketch]({{ "/assets/images/engrd2020-crosssection.jpg" | relative_url }}){: .inline-image-r style="width: 150px"}

$$I = \frac{b_o h_o^3 - b_i h_i^3}{12}$$
- $h_o$ = 40mm
- $h_i$ = 36mm

$$I = \frac{40(40)^3 - 36(36)^3}{12} = \frac{2,560,000 - 1,679,616}{12} \approx 73,365 \text{ mm}^4$$

Since $73,365 > 16,107$, the design constraint is satisfied. 
$$\delta = \frac{P L^3}{3 E I}=\frac{270.6 *0.5^3}{3* (70*10^9)*(7.33*10^{-8})}\approx 2.197$$ mm

The total mass:
$$A = b_o h_o - b_i h_i = (0.04 \text{ m})^2 - (0.036 \text{ m})^2 = 0.000304 \text{ m}^2$$
$$m = \rho \times A \times L= 2710 \text{ kg/m}^3 \times 0.000304 \text{ m}^2 \times 0.5 \text{ m} \approx 0.412 \text{ kg}$$

### Conclusion:
The proposed $40 \times 40 \times 2$ mm Aluminum tube provides an inertia of $29,418 \text{ mm}^4$, which is significantly higher than the required $16,300 \text{ mm}^4$. This ensures the deflection remains well below the 10mm limit ($\delta \approx 2.2 \text{ mm}$), providing a safety factor for dynamic loads while maintaining a lightweight design ($m \approx  0.412 \text{ kg}$).

