---
layout: page 
date: 2023-9-9 15:59:00-0400
title: Combining Bounded Rationality with Game Theory
importance: 3 
category: research
img: /assets/img/6cf_position_swap1.png
---
<div>
This research introduces a practical approach to (numerically) compute Nash Equilibrium (NE) by abandoning the assumption of perfect rationality. Instead of trying to predict optimal behavior, which is computationally intensive and often inaccurate, the framework incorporates "bounded rationality" – accounting for limited decision-making capabilities.

<br/>

<div style="display: flex; align-items: flex-start; gap: 20px;">
    <div style="flex: 0.6;">
        In a paper published in <a href="https://arxiv.org/pdf/2210.08672">DARS 2022</a>, we use the information-theoretic perspective of bounded rationality, which states that agents' do not want to deviate from their nominal behavior. Combining with the game theory, the approach enables robots to predict and respond to sub-optimal behaviors while working within their own computational limits. The method was successfully demonstrated in both simulated and real-world multi-robot navigation tasks.
    </div>
    <div style="flex: 0.4;">
        <iframe width="100%" height="200" src="https://www.youtube.com/embed/hzCitSSuWiI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>

<br/>
In a follow-up <a href="https://ieeexplore.ieee.org/abstract/document/10342006">work</a> published in IROS 2023, we
design a prior policy that provides informative goal-directed navigation heuristics in familiar environments and is
adaptive in unfamiliar ones via Reinforcement Learning augmented with an environment-dependent exploration noise.
Integrating this prior policy in the game-theoretic bounded rationality framework allows agents to quickly make
decisions in a group considering other agents' computational constraints.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/informed.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Shows the adaptation process from default to satisficing path in the proposed method and the baseline. (a) to (e) shows the proposed method’s
performance on the adaptability. (f) to (j) shows the baseline method’s performance. The snapshot has been taken after the same number of iteration to shoe
the comparison. Both the method uses 5 sampled trajectories.
</div>

