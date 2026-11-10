---
layout: page
title: Topology-Optimized e-Machines & Digital Twin Validation
description: Rotor topology optimization, electromagnetic/NVH evaluation, and MATLAB/Simulink + dSPACE virtual validation for automotive traction drives.
img: assets/img/12.jpg
importance: 1
category: industrial
---

### Overview

At **Jaguar Land Rover**, I lead cross-functional digital twin and validation activities for automotive electric propulsion (`e-Machines`), bridging multi-physics CAE (electromagnetic, thermal, structural, and NVH) with physical prototype testing and hardware-in-the-loop (HIL) validation.

### Key Technical Contributions

1. **Rotor Topology Optimization**:
   - Developed a topology-optimization methodology for permanent-magnet rotors that reduces rotor core volume and mass while preserving peak/continuous torque and minimizing torque ripple:
     $$\max_{\rho(\mathbf{x})} \; \overline{T}_e(\rho) \quad \text{subject to} \quad V(\rho) \le V_{\max}, \quad \sigma_{\text{von Mises}}(\rho) \le \sigma_{\text{allow}}, \quad T_{\text{ripple}}(\rho) \le \epsilon_T$$
2. **Digital Twin & Virtual Validation**:
   - Built high-fidelity plant models and integrated flux-linkage maps $\psi_d(i_d, i_q, \theta_e), \psi_q(i_d, i_q, \theta_e)$ into **MATLAB/Simulink** and **dSPACE** virtual validation environments for e-drive/controller calibration and verification.
3. **Requirements, V&V & Test–CAE Correlation**:
   - Defined component and system-level requirements with end-to-end verification traceability.
   - Coordinated NVH assessment, magnetic material characterization, radial/tangential electromagnetic force evaluation, and test–simulation correlation.
