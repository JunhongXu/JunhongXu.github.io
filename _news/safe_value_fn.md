---
layout: post
date: 2024-4-1 15:59:00-0400
summary: Safe Value Function 
inline: true
---

<div style="width: 100%;">
    <div style="width: 100%;"> 
    This work directly bakes the safety and task constraints into the second-order Hamilton-Jacobi Belllman (HJB) Equation.
    The resulting solution is a safe value function that can guide the policy to achieve goals safely.
    By integrating safety and task constraints directly into the boundary conditions, we move from complex, dense rewards to more straightforward, sparse constraints.
    As a result, the resulting value function sharpens the distinction between safe and unsafe states.
    Additionally, we also propose a hybrid model that combines a mesh-based function approximator for accurately computing boundary conditions with a meshless method, such as neural networks or kernel functions, to enhance computational efficiency.
    This work is accepted by the International Journal of Robotics Research (IJRR) <a href="https://arxiv.org/pdf/2403.14956">[Paper]</a>.
    </div>
</div>

<br/>

<div style="width: 100%; display: flex; justify-content: center; align-items: center;">
    <iframe width="560" height="314" src="https://www.youtube.com/embed/URD5Z87jdO0?si=KNUV1E10STQMrc1x" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
