---
layout: page 
date: 2024-4-1 15:59:00-0400
title: Safe Motion Planning and Control Under Uncertainty
importance: 2 
category: research
img: /assets/img/offroad.gif
---

<div style="width: 100%;">
    Robots usually need to leverage a robot-environment interaction model to properly plan their motions to avoid hazardous states and achieve desired behaviors.
    However, models (learned and hand-crafted) generally cannot exactly capture the real-world interactions and often involves high levels of uncertainties.
    This research aims at directly integrating the uncertainty estimation into the planning stage for generating robust and safe closed-loop motion plans (or policies).
</div>
    
<br/>

#### Value Function Approximation in Continuous MDPs
<div style="display: flex; align-items: center; gap: 20px;">
    <div style="flex: 0 0 60%;">
        At the core of this problem involves solving a continuous state and action Markov Decision Process (MDP).
        We propose a series of work that approximates and solves the continuous value function <a href="https://arxiv.org/pdf/2006.02008">[RSS 2021]</a> and integrates the proposed solver into a system that connects from perception to planning. This system has been heavily tested in real-world unstructured environments <a href="https://arxiv.org/pdf/2403.14956">[IJRR 2024]</a>.
    </div>
    <div style="flex: 0 0 40%;">
        <img src="/assets/img/offroad.gif" alt="Offroad Demo" style="width: 400px; height: 260px; object-fit: contain;">
    </div>
</div>

<br/>

#### Causal Inference for Motion Model Learning
<div style="display: flex; align-items: center; gap: 20px;">
    <div style="flex: 0 0 60%;">
        The above work computes the value function and policy using probabilistic motion models realized by a Gaussian distribution, with parameters learned from historical offline driving data. While effective, learning from offline data poses unique challenges due to confounding variables that can bias the robot's understanding of action-state relationship. In a follow-up work published in <a href="https://arxiv.org/pdf/2210.08679">ICRA 2023</a>, we address this limitation using causal inference to learn more sophisticated motion models. 
    </div>
    <div style="flex: 0 0 40%;">
        <iframe src="https://www.youtube.com/embed/GWHKrVvzl4M?si=Y4cOqUf_00Vz4irG" width="400" height="260" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>

<br/>

#### Safe Value Function
<div style="display: flex; align-items: center; gap: 20px;">
    <div style="flex: 0 0 60%;">
        This work directly bakes the safety and task constraints into the boundary conditions of the second-order Hamilton-Jacobi Belllman (HJB) Equation. As a result, the solution to this HJB equation is a safe value function that sharpens the distinction between safe and unsafe states and can guide the policy to achieve goals safely. By treating safety and task as boundary conditions, we move from complex, dense rewards to more straightforward, sparse constraints. Additionally, we also propose a hybrid model that combines a mesh-based function approximator for accurately computing boundary conditions with a meshless method, such as neural networks or kernel functions, to enhance computational efficiency. This work is accepted by the International Journal of Robotics Research (IJRR)
        <a href="https://arxiv.org/pdf/2403.14956">[Paper]</a>.
    </div>
    <div style="flex: 0 0 40%;">
        <iframe width="400" height="260" src="https://www.youtube.com/embed/URD5Z87jdO0?si=KNUV1E10STQMrc1x" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>
