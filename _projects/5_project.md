---
layout: page
title: EV Charger Placement Optimization for Public Transit Buses
description: Mixed-integer linear programming (Python-PuLP & MATLAB/Octave) for optimal off-board fast-charger siting along intra-city bus routes.
img: assets/img/9.jpg
importance: 3
category: academic
---

### Overview

This project developed an optimization framework for siting off-board electric vehicle (EV) fast chargers across an intra-city public transport bus network, minimizing total infrastructure and energy expenditure while guaranteeing route state-of-charge (SoC) feasibility.

### Technical Highlights

- **Route Energy & Battery SoC Modeling**:
  Modeled route-specific energy consumption across stops and layover windows, accounting for bus battery capacity bounds ($\text{SoC}_{\min} \le \text{SoC}_k \le \text{SoC}_{\max}$) and dwell-time charging power limits.
- **Optimization Formulation (Python-PuLP & MATLAB/Octave)**:
  Formulated and solved a constrained cost-minimization problem using **Python (`PuLP`)** and **MATLAB/Octave** to determine optimal charger locations and power ratings across candidate transit terminals.
