---
layout: project
title: ENGRD2020-Project
description: Mechanism Design
technologies: [N/a]
image: /assets/images/hw5-sketch.jpg
math: true
---

Given a 2D design space of 150 cm long and 50 cm tall, I designed a mechanism system with a rigid bar of a fixed length, three pin supports (two of which need to be mounted on the ground), and a linear actuator. The goal is for this mechanism to lift the maximum possible weight to the maximum possible height.

I chose IMASS for the linear actuator, as it has the maximum force and stroke length among the Tolomatic's integrated motor actuator series:
- Face Size: 142mm
- Stroke: 152.44-457.2mm
- Based Weight: 24.8kg
- Peak Thrust: 35.8kg

In my design, the rigid bar is pinned at support $A$ and hangs the weight at the end $C$ of bar $AC$. The bar's length is $L=|AC| = 0.5 m$, which maximizes the accessible height when bar $AC$ is fully lifted and stays vertical.
The linear actuator, mounted on the ground at $B$, is connected at the end $C$ of bar $AC$.

![Photo of Sketch]({{ "/assets/images/hw5-sketch.jpg" | relative_url }}){: .inline-image-l}

Given the size dimensions of the linear actuatorm, the distance between $A$ and $B$ can be deduced. When the bar $AC$ is fully lifted vertically, $h_{max}=0.5m$, actuator $BC$ should reach its maximum stroke length $BC_{max}=142+457.2mm=0.599m$. So, distance $d\approx 330.21mm$, with an angle $\theta_a=90^\circ$ and $\theta_b=56.55^\circ$. 
To minmize the possible height (maximize the height difference), actuator $BC$ should reach its minimum stroke length $BC_{min}=142+152.2mm$, we got the minimum height of $C$, $h_{min}=R_{AC}*\hat{j}=282.70=0.294$, $\theta_a=34.43^\circ$, and $\theta_b=106.17^\circ$.

Then,  height gain of the weight is $\Delta h = h_{\max}-h_{\min}\approx 0.500-0.2827=0.2173\ \text{m}$.

Let the hanging weight be $W$. The actuator is a two-force member along $BC$. The moment equilibrium about pin $A$ gives: $\sum M = F(\theta_a)\frac{d}{BC_{\theta_a}} + W\frac{x_c}{y_c}=0$.
Then,  $F(\theta_a)$ is largest at lowest height with $\theta_{a}=34.43^\circ$. $F(\theta_a)_max \approx 1.30 W$.

Since Peak Thrust of the actuator is 35.8kg, $F(\theta_a)_max=351.08N$. Then $W\approx 270.6 N$ is the maximum load. 


