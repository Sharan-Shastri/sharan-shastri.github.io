---
layout: page
title: Ultra-High-Speed (>150k RPM) PM Motor Design & Automation
description: 2D/3D ANSYS FEA, rotor loss & demagnetization analysis, and automated Python-ANSYS flux-map pipelines at Dyson RDD.
img: assets/img/3.jpg
importance: 2
category: industrial
---

### Overview

In Research, Design & Development (RDD) at **Dyson (Singapore)**, I designed and optimized permanent-magnet motor systems for ultra-high-speed consumer applications operating above **$150\text{,000 RPM}$**.

### Key Technical Contributions

1. **Ultra-High-Speed Electromagnetic & Multiphysics Design**:
   - Optimized permanent-magnet rotor/stator geometries considering air-gap flux density, irreversible demagnetization margins under fault and overload currents, sleeve/rotor structural retention limits, and high-frequency manufacturability constraints.
   - Conducted detailed **2D/3D ANSYS Maxwell FEA** accounting for nonlinear $B\text{–}H$ saturation, high-frequency stator core losses (Bertotti separation), and 3D magnet eddy-current losses:
     $$P_{\text{core}} = k_h f B_m^\alpha + k_c f^2 B_m^2 + k_e f^{1.5} B_m^{1.5}$$
2. **Python–ANSYS Automation for Controls Integration**:
   - Created an automated **Python–ANSYS** workflow to sweep operating envelopes, extract nonlinear flux and inductance maps, and post-process efficiency contours directly into **MATLAB/Simulink** motor-drive models—eliminating manual post-processing bottlenecks.
3. **Magnetic Material & Supplier Qualification**:
   - Evaluated sintered and bonded permanent-magnet grades with suppliers to balance thermal stability ($H_{cJ}(T)$), remanence ($B_r$), and high-volume manufacturing tolerances.
