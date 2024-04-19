---
layout: distill
title: People, planet, and profits in parcel delivery
description: A novel model and algoritm for social and environmental aware parcel delivery
img: assets/img/publication_preview/coptw-snap.png
importance: 1
category: papers
featured: true
bibliography: multi-policy.bib
authors:
  - name: Michele Urbani
    affiliations:
      name: University of Trento
toc:
    - name: Introduction
    - name: Case study
    - name: A sustainable delivery model
    - name: Results
---


## Introduction


## A sustainable delivery model

### A novel multi-objective algorithm

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/heuristics-search-space.png" class="img-fluid rounded z-depth-1" style="text-align: center;" zoomable=true %}
    </div>
</div>
<div class="caption">
Figure 1: A mapping from the heuristic search space to the solution space of the problem. Each heuristic on the left produces a new solution on the right, some of which could be infeasible, e.g., solution ``b`` in solution space. A transition between heuristics ``A`` and ``C``, may produce a "jump" in the solution space, that is a solution ``c`` completely different from solution ``a``. Some transitions between heuristics may return a so-called "neighborhood" move in the solution space, like from solution ``a`` to ``c``. Both jumps and neighborhood moves are welcome, depending on the algorithm's elapsed execution time.
</div>

## Case study results and insignhts

### City delivery

Show example map with markers for pickup and delivery locations.
Add layer to show connections between pickup-delivery pairs.

Show an example frontier of possible delivery plans.

### Sparse pickup and delivery in valleys

### Uniform demand all over the region

## Conclusions

