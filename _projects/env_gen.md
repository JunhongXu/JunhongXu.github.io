---
layout: page 
date: 2023-9-9 15:59:00-0400
title: Grounded Environment Generation for Reducing Sim-to-Real Gap
importance: 1 
category: research
img: /assets/img/terrain.gif
---

<div style="width: 100%;">
    <div style="width: 100%;"> 
Model-free reinforcement learning has emerged as a powerful method for developing robust robot control policies capable of navigating through complex and unstructured terrains.
The effectiveness of these methods hinges on two essential elements:
(1) the use of massively parallel physics simulations to expedite policy training,
and
(2) an environment generator tasked with crafting sufficiently challenging yet attainable terrains to facilitate continuous policy improvement. 
Existing methods of environment generation often rely on heuristics constrained by a set of parameters, limiting the diversity and realism.
In this work, we introduce the Adaptive Diffusion Terrain Generator (ADTG), a novel method that leverages Denoising Diffusion Probabilistic Models to dynamically expand existing training environments by adding more diverse and complex terrains adaptive to the current policy.
ADTG guides the diffusion model's generation process through initial noise optimization, blending noise-corrupted terrains from existing training environments weighted by the policy's performance in each corresponding environment.
By manipulating the noise corruption level, ADTG seamlessly transitions between generating similar terrains for policy fine-tuning and novel ones to expand training diversity.
Our experiments show that the policy trained by ADTG outperforms both procedural generated and natural environments, along with popular navigation methods.
</div>
<br/>
<div style="width: 100%; display: flex; justify-content: center; align-items: center;">
    <iframe width="100%" height="320" src="https://www.youtube.com/embed/Ua8HeGvr4Ms" title="Adaptive Diffusion Terrain Generator for Autonomous Uneven Terrain Navigation" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
