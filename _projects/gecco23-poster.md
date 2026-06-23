---
layout: distill
title: A multi-policy hyper heuristic for multiobjective optimization
description: A poster for the GECCO23 Conference, July 15-19th, 2023, Lisbon
img: assets/img/publication_preview/gecco23-poster-thumbnail-1.png
importance: 1
category: posters
featured: true

bibliography: gecco23.bib

authors:
  - name: Michele Urbani
    affiliations:
      name: Department of Industrial Engineering, University of Trento
  - name: Francesco Pilati
    affiliations:
      name: Department of Industrial Engineering, University of Trento
toc:
    - name: Motivations
    - name: Research goals
    - name: Methodology
    - name: Algorithm architecture
    - name: Experimental setting
    - name: Selected results
    - name: Conclusions and future research
---

Selection hyper-heuristics (SSHH) are search strategies that can be successfully applied to multi-objective optimization (MOO) problems.
They showed resilient results to different types of optimization problems, which may come at the cost of a longer resolution time than other metaheuristics.
Learning a single selection rule in MOO might be limiting because the information from the multiple objectives might be unexploited.
A novel approach named the multi-policy approach is proposed and discussed to further enhance the searching ability of sequence-based selection hyper-heuristics, together with an ad-hoc learning rule.
The availability of a set of problem-specific low-level heuristics is assumed and the resolution of a specific class of combinatorial problems, i.e., vehicle routing problems (VRPs), is considered for a numerical example.
The multi-policy approach showed the ability to learn different selection rules for each objective and to change them during the execution of the algorithm, i.e., when solutions are getting closer to the Pareto front.
The availability of parallel computation can speed up the calculation since the methodology is suitable for parallelization.
The proposed methodology was found to produce production-ready solutions and the approach is expected to be successfully extended to problems different from the VRP.

## Motivations

* Selection hyper-heuristics (SSHH) are search strategies that can be successfully applied to multiobjective optimization problems<d-cite key="DRAKE2020405"></d-cite>.
* Learning a single selection rule in a SSHH might be limiting because the information from the multiple objectives might be unexploited<d-cite key="TRICOIRE20123089"></d-cite>.
* Algorithms based on sequences of problem-specific low-level heuristics can efficiently solve complex combinatorial problem<d-cite key="kheiri2020inventory"></d-cite>.

## Research goals

* A novel approach named the **multi-policy** approach is proposed to further enhance the searching ability of sequence-based selection hyper-heuristics.
* The multi-policy approach performs **online** learning of the select policies. One selection policy per objective is learned using objective-wise information.
* The proposed algorithm is tested on a **real-world** instance of the vehicle routing problem with pickup and delivery (VRPPD).

## Methodology

A **low-level heuristic** (LLH) is a rule that modifies the decision variables $$\mathbf{z}$$ of the problem under analysis.
A set $$H$$ of $$m$$ LLHs is assumed to be available to modify the solutions $$\mathbf{z} \in Pop$$.

A **selection policy** is an ensemble of Markov decision models that alternates the selection of LLHs $$h$$ and sequence-termination signals $$AS$$ (see box 1 in Figure 1).
There are **as many selection policies as the number $N$ of objectives**.

At each iteration, a selection policy produces a sequence of low-level heuristics $$SEQ$$ (see box 2 in Figure 1) to be applied to a solution $$\mathbf{z}$$.

For each new solution $$\mathbf{z'} \in Pop'$$ that was improved by a sequence of heuristics $$SEQ$$, the **reward rule** (see box 3 in Figure 1) attributes a score to all the couples of subsequent heuristics in $$SEQ$$.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/selection-policy-1.png" class="img-fluid rounded z-depth-1" style="text-align: center;" zoomable=true %}
    </div>
</div>
<div class="caption">
    Figure 1: The architecture of the learning system.
</div>

## Algorithm architecture

The multi-policy hyper heuristic foresees an initiation phase followed by the main loop.
The main loop is executed separately for each policy, which makes the procedure suitable to be parallelized.
The termination criterion chosen for the poster was the number of iterations; time and convergence of a performance metric can be used as well.

As shown in Figure 2, the main loop is followed by the update of selection policies and a check for the termination condition.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/mphh-architecture-1.png" class="img-fluid rounded z-depth-1" zoomable=true width=400 %}
    </div>
</div>
<div class="caption">
    Figure 2: The architecture of the multi-policy hyper heuristic.
</div>

## Experimental setting

Numerical experiments were carried out to solve a three-objective version of the vehicle routing problem with pickup and delivery (VRPPD).

The multi-policy algorithm was tested on a single instance of the VRPPD with **60 deliveries** and **4 pickup points**.
Figure 3 shows an example of the Pareto front obtained by the multi-policy algorithm.

<div class="l-page">
  <iframe src="{{ '/assets/plotly/pareto.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    Figure 3: A Pareto front obtained by the multi-policy algorithm.
</div>

Data are inspired to a **real-world case study**: a geography with non-Euclidean distances was used, and goods to be delivered presented different weights and volumes.

## Selected results

1. Selection policies evolve over time: for example, comparing $$\mathbf{p}^{(eco)}$$ at iteration 25 and 50 in Figure 4, the selection probability distribution $$p_{h_4}$$ changes significantly.
2. Selection policies evolve differently from each other: for instance, $$\mathbf{p}^{(eco)}$$ and $$\mathbf{p}^{(env)}$$ at iteration 50 in Figure 4 and 5 present significantly different values for $$p_{h_0}$$ and $$p_{h_1}$$.
3. The learned policies are sensitive to: (1) the **reward value** $$r$$ that is used, (2) the number of iterations between **policy updates** $$N_{update}$$, and (3) the weight that is used when updating the probabilities in the Markov decision model.

<div class="l-page">
  <iframe src="{{ '/assets/plotly/economic.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    Figure 4: A representation of the low-level heuristic selection policy for the economic objecetive.
</div>

<div class="l-page">
  <iframe src="{{ '/assets/plotly/environmental.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    Figure 5: A representation of the low-level heuristic selection policy for the environmental objecetive.
</div>

<div class="l-page">
  <iframe src="{{ '/assets/plotly/social.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    Figure 6: A representation of the low-level heuristic selection policy for the social objecetive.
</div>

## Conclusions and future research

* **Learning selection policies** is not straightforward. Extensive testing of the learning rule is required over a large and diverse set of instances of the problem studied.
* **Online learning** in multiobjective combinatorial problems is **time expensive**. Either a high-performance implementation of the algorithm exists, or offline learning should be considered.
* **Comparative analysis** of the proposed multi-policy hyper heuristic is required. Algorithms such as multiobjective local search (MOLS) and choice function hyper heuristic (CFHH) will be considered for testing over **large** (e.g., up to 500 nodes) and **diverse** (e.g. geography, load, time windows) **problem instances**.
* **Sampling of LLH sequences** yield widely variable execution times when the termination criterion is the number of iterations, which might be undesirable in the production phase.
