---
layout: distill
title: Workforce routing optimization for an Energy Saving COmpany (ESCO)
description: How to meet 99.9% of maintenance due dates while optimizing costs
img: assets/img/publication_preview/coptw-snap.png
importance: 1
category: papers
featured: true
doi: "10.1016/j.cor.2023.106488"
bibliography: esco.bib
authors:
  - name: Michele Urbani
    affiliations:
      name: University of Trento
toc:
    - name: Introduction
    - name: Case study
    - name: Technology
    - name: Results
---


## Introduction

Efficient workforce management holds paramount importance across various industrial sectors. A systematic approach not only yields cost savings but also enhances due date compliance and boosts the overall efficiency of the worker fleet. In our recently published paper<cite key="BENDAZZOLI2024"></cite>, we delve into the application of operations research to optimize workforce routing for an Energy Saving Company.

## Case study

**Understanding ESCO**: An Energy Saving Company (ESCO) offers a comprehensive array of energy-related solutions, "including designs and implementation of energy savings projects, retrofitting, energy conservation, energy infrastructure outsourcing, power generation, energy supply, and risk management".
<aside>Source: <a href="https://en.wikipedia.org/wiki/Energy_service_company">en.wikipedia.org</a></aside>
Our focus in this project lies on the maintenance aspect, specifically addressing local regulations mandating periodic servicing of heating, ventilation, and air conditioning (HVAC) systems.
Timely maintenance is critical for an ESCO, as non-compliance could result in penalty payments and pose potential health risks to users.

Maintenance tasks for contracted buildings fall under the purview of ESCO employers, necessitating meticulous organization by managers. Therefore, optimizing workforce routing becomes pivotal for meeting due dates and adhering to various practical constraints. For instance, operators are trained in two distinct profiles—electrical and thermal-hydraulic—and are eligible for tasks aligned with their specific skill set. Another practical constraint involves the departure/arrival depot of workers, operating within regular work hours from 8 AM to 4 PM, unless urgent circumstances dictate otherwise.

A unique requirement in this case study is the synchronization of interventions, where maintenance events necessitate the presence of two or more operators at the same location simultaneously. Planning such activities poses a challenge for maintenance managers, who, despite their experience, may need to adjust schedules dynamically.

### Rolling horizon approach

The central challenge in managing the maintenance of a building portfolio is ensuring compliance with due dates. With up to 600 activities in the case study, each with distinct due dates, the task of combining urgent tasks with maintenance of nearby buildings becomes complex for human decision-makers.
Prioritizing tasks through a scoring system, based on their proximity to due dates, facilitates effective selection.
This approach allows for:
1. Inserting the most urgent activities in the maintenance schedule with a very high probability.
1. Filling operators' free time with lower-scoring activities.
1. Reassessing previously unselected activities with higher priority on subsequent days to prevent leaving buildings unattended.

## Technology

This research addresses the workforce routing problem using a mathematical model, specifically a mixed-integer linear program (MILP).
This model remains independent of specific data, allowing seamless integration of changing task priorities or the addition of new buildings without altering the underlying problem description.
A heuristic optimization algorithm, the Adaptive Large Neighbourhood Search (ALNS), is employed to solve the MILP model effectively within a limited timeframe.

### Integration of data and problem constraints

The MILP model encapsulates the problem's mathematical representation, providing a data-agnostic framework.
This allows for the pipeline of data into the solver for daily use and hypothetical what-if analyses without necessitating code modifications.

### Problem solving mechanism

The ALNS heuristic algorithm is an extension of the Large Neighbourhood Search (LNS) procedure, which foresees to explore the solution space through the neighbours of an existent solution.
By definition, a neighbourhood is a solution that can be obtained through the aplication of a heuristic (either deterministic or stochastic) rule to an already known solution.
However, in the LNS procedure, heuristic rules (a.k.a. operators) are usually selected randomly, thus loosing the opportunity to focus on the top performers.
In the ALNS algorithm instead, the past performance of operators is leveraged to steer the selection: the better the track of records of a heuristic rule, the higher the probability that it will be selected.
Since the effectiveness of an operator may change during the execution of an algorithm, its probability to be selected is adjusted accordingly.
This simple form of experience-based intelligence attributes the adaptability feature to the algorithm.

#### Interaction of ALNS with solutions

A solution to the maintenance planning problem can be indirectly described by a collection of lists, each encoding the ids of the buildings to be visited by a technician.
The ALNS algorithm interacts with a solution by means of a set of heuristic rules, namely a list of well-known rules that can be used to improve a solution.
For example, the *or-opt* rule swaps the position of a visit along a route with all the other positions to check if an improvement is possible.
The *2-opt* rule is slightly more explorative than or-opt: it randomly choose a visit along two different routes and split the route into head and tail. Finally, to produce two new routes, the tails are swapped.
The figure below shows the or-opt and 2-opt operators using an animation.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/2-opt.png" class="img-fluid rounded z-depth-1" style="text-align: center;" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/or-opt.png" class="img-fluid rounded z-depth-1" style="text-align: center;" zoomable=true %}
    </div>
</div>
<div class="caption">
    Figure 1: A graphical representation of 2-opt (left) and or-opt heuristics (right). After the 2-opt operator has been applied, route 1 visits locations 1, 2, 7, and 8, whereas route 2 visits buildings 5, 6, 3, and 4. The or-opt operator changes the order of visits from 1, 2, 3, 4, to a new order 1, 3, 2, 4.
</div>

## Results

The result of this research and development project was an effective and scalable workforce optimization solution.
Maintenance managers could:

1. Automatically set or manually define priorities for the activities to be assigned to maintenance staff;
1. See the results of the optization process in minutes, without any manual planning effort, hence wiht the opportunity to focus on reviewing and refining the maintenance schedule proposed by the optimization tool;
1. Address emergency maintenance requests by re-optimising the maintenance schedule starting from the actual position of the fleet of workers.

The result of the optimization process could be visualised in a map format as shown by the figure below.

<div class="l-page">
  <iframe src="{{ '/assets/plotly/map.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>
<div class="caption">
    An interactive map of operators' daily maintenance schedule. <span style="color:green">Green</span> markers identify low-priority activities, <span style="color:red">red</span> markers identify urgent activities, and <span style="color:orchid">purple</span> ones are activities requiring synchronisatio of operators, whereas <span style="color:DodgerBlue">blue</span> markers show the house of technicians. By selecting only the operators Paoli Pasquale and Mario Rossi, it is possible to check that they carry out a synchronised activity in Brentonico (South east of Riva del Garda).
</div>

In the picture's example, a fleet of six maintenance technicians is routed to maximise the sum of priorities collected by carrying out a set of maintenance activities.
The route of each technician can be visualised or hidden by flagging in the top-right menu in the figure.
By hovering a marker in the map, it is possible to visualise useful information about a specific task, included the expected start time of the activitiy, the technician assigned to it, the skill required to execute the task (if any), and the task's priority value.
Some activities required the synchronisation of two technicians: for example, technicians Paoli Pasquale and Mario Rossi carry out a synchronised maintenance task on a building located south-east of Riva del Garda (purple marker).
They are expected to meet around 1:45 PM, then each continue working according to different schedules.
Route directions to move between two builldings are calculated according the [Valhalla routing engine](https://github.com/valhalla/valhalla), a free tool based on [OpenStreetMap](https://www.openstreetmap.org/) cartography.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/Trajectory.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>
<div class="caption">
  An animation showing the trajectories followed by the six operators in the maintenance schedule found by the algorithm.
</div>

## Conclusions

The integration of company data, technician skills, and external data on travel times and distances effectively optimizes workforce routing. Beyond cost savings, the company can consistently meet due dates and strategically manage less urgent tasks. Maintenance managers are relieved of planning duties, enabling them to focus on reviewing and refining schedules proposed by the optimization tool. Field technicians gain awareness of being part of a systematic plan, enhancing overall efficiency.

For further details, refer to the open-access paper: [https://doi.org/10.1016/j.cor.2023.106488](DOI: 10.1016/j.cor.2023.106488).
