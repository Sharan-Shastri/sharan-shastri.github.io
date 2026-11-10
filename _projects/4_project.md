---
layout: page
title: PMBLDC Motor & Drive for EV Three-Wheeler Traction
description: Electromagnetic sizing, ANSYS Maxwell FEA, and MATLAB/Octave vehicle-load traction simulation for electric three-wheelers.
img: assets/img/7.jpg
importance: 2
category: academic
---

### Overview

Conducted during my Integrated M.Tech thesis at the **Central University of Karnataka** (Supervised by Dr. V. Sandeep; **University Gold Medal, 2018**), this project focused on the complete electromagnetic design and drive simulation of a Permanent Magnet Brushless DC (PMBLDC) traction motor for Indian three-wheeler electric vehicles (e-rickshaws / auto-rickshaws).

### Technical Highlights

- **Vehicle Dynamics & Tractive Effort Modeling**:
  Derived peak and continuous torque-speed envelopes from gradeability, rolling resistance, aerodynamic drag, and drive-cycle acceleration requirements:
  $$F_{\text{tractive}} = m g C_{rr} \cos\alpha + m g \sin\alpha + \frac{1}{2}\rho_{\text{air}} C_d A_f v^2 + \delta m \frac{dv}{dt}$$
- **Analytical Sizing & 2D Electromagnetic FEA**:
  Sized the stator slot/pole combination and permanent-magnet rotor geometry, followed by **ANSYS Maxwell** finite-element verification of air-gap flux density, back-EMF waveform, cogging torque, and overload torque capability.
- **Closed-Loop Traction Drive Simulation**:
  Simulated six-step and hysteresis current-controlled inverter operation under dynamic vehicle load profiles in **MATLAB/Octave**.
