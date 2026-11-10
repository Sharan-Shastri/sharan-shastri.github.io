---
layout: post
title: "PMSM d-q Frame Modeling, Reluctance Torque & Live Interactive Simulation"
date: 2025-05-10 10:00:00+0530
description: Mathematical derivation of Interior PMSM d-q equations and an interactive browser simulation of electromagnetic, alignment, and reluctance torque vs. current advance angle.
tags: electric-machines control-systems fea math plotly
categories: knowledge-base motor-design
featured: true
related_publications: true
chart:
  plotly: true
toc:
  beginning: true
---

This note serves both as a technical reference on **Interior Permanent Magnet Synchronous Machine (IPMSM)** $d\text{–}q$ modeling and as a live template for writing notes with **MathJax equations**, **BibTeX citations**, **Plotly charts**, and **interactive parameter sliders** in `al-folio`.

---

## 1. Synchronous $d\text{–}q$ Frame Voltage & Flux-Linkage Equations

In the rotor-aligned synchronous reference frame ($d$-axis aligned with the permanent magnet north pole, $q$-axis leading by $90^\circ$ electrical), the stator voltage equations are given by:

$$
\begin{aligned}
v_d &= R_s i_d + \frac{d\psi_d}{dt} - \omega_e \psi_q \\
v_q &= R_s i_q + \frac{d\psi_q}{dt} + \omega_e \psi_d
\end{aligned}
$$

Assuming magnetic linearity (prior to cross-saturation $\psi_d(i_d, i_q), \psi_q(i_d, i_q)$ extracted via automated 2D/3D FEA {% cite shastri2023rapid_jmmct %}), the flux linkages are:

$$
\psi_d = L_d i_d + \psi_f, \qquad \psi_q = L_q i_q
$$

where:
- $R_s$ is the per-phase stator winding resistance ($\Omega$),
- $L_d, L_q$ are the direct- and quadrature-axis synchronous inductances ($\text{H}$),
- $\psi_f$ is the permanent-magnet flux linkage ($\text{Wb}$), and
- $\omega_e = p\,\omega_m$ is the electrical angular velocity ($\text{rad/s}$) for $p$ pole pairs.

---

## 2. Electromagnetic Torque & MTPA Trajectory

The total electromagnetic torque $T_e$ produced by an IPMSM consists of **PM alignment torque** and **reluctance torque**:

$$
T_e = \frac{3}{2} p \Big( \underbrace{\psi_f i_q}_{\text{Alignment Torque}} + \underbrace{(L_d - L_q) i_d i_q}_{\text{Reluctance Torque}} \Big)
$$

Expressing the stator current phasor amplitude as $I_s = \sqrt{i_d^2 + i_q^2}$ with current advance angle $\beta$ measured from the $q$-axis ($i_d = -I_s \sin\beta$, $i_q = I_s \cos\beta$):

$$
T_e(\beta) = \frac{3}{2} p \left[ \psi_f I_s \cos\beta + \frac{1}{2}(L_q - L_d) I_s^2 \sin(2\beta) \right]
$$

Setting $\frac{\partial T_e}{\partial i_d} = 0$ subject to $i_d^2 + i_q^2 = I_s^2$ yields the **Maximum Torque Per Ampere (MTPA)** locus:

$$
i_{d,\text{MTPA}} = \frac{\psi_f}{2(L_q - L_d)} - \sqrt{\frac{\psi_f^2}{4(L_q - L_d)^2} + i_q^2}
$$

---

## 3. Declarative Plotly Chart (Static JSON Block)

Using `al-folio`'s built-in `plotly` fenced block (`chart: plotly: true` in frontmatter), we can embed zoomable, hoverable plots directly from JSON data:

```plotly
{
  "data": [
    {
      "x": [0, 15, 30, 45, 60, 75, 90],
      "y": [12.0, 11.59, 10.39, 8.49, 6.0, 3.11, 0.0],
      "name": "Alignment Torque (N·m)",
      "type": "scatter",
      "mode": "lines+markers"
    },
    {
      "x": [0, 15, 30, 45, 60, 75, 90],
      "y": [0.0, 3.38, 5.85, 6.75, 5.85, 3.38, 0.0],
      "name": "Reluctance Torque (N·m)",
      "type": "scatter",
      "mode": "lines+markers"
    },
    {
      "x": [0, 15, 30, 45, 60, 75, 90],
      "y": [12.0, 14.97, 16.24, 15.24, 11.85, 6.49, 0.0],
      "name": "Total Torque Te (N·m)",
      "type": "scatter",
      "mode": "lines+markers",
      "line": { "width": 3 }
    }
  ],
  "layout": {
    "title": { "text": "Baseline IPMSM Torque Breakdown vs. Current Advance Angle β" },
    "xaxis": { "title": { "text": "Current Advance Angle β (deg)" } },
    "yaxis": { "title": { "text": "Torque (N·m)" } }
  }
}
```

---

## 4. Live Interactive Simulator (Real-Time Parameter Sliders)

Adjust the current amplitude $I_s$, permanent-magnet flux linkage $\psi_f$, and saliency $(L_q - L_d)$ below to see the **Alignment Torque**, **Reluctance Torque**, **Total Torque $T_e(\beta)$**, and the optimal **MTPA angle $\beta^*$** update live in your browser:

<div style="padding: 1.25rem; border: 1px solid var(--global-divider-color, #ccc); border-radius: 8px; margin: 1.5rem 0;">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 1rem; margin-bottom: 1rem;">
    <label style="display: flex; flex-direction: column; font-size: 0.9rem;">
      <span><strong>Stator Current $I_s$ (A):</strong> <span id="val-is">50</span> A</span>
      <input type="range" id="slider-is" min="10" max="150" step="5" value="50" />
    </label>
    <label style="display: flex; flex-direction: column; font-size: 0.9rem;">
      <span><strong>PM Flux $\psi_f$ (Wb):</strong> <span id="val-psif">0.08</span> Wb</span>
      <input type="range" id="slider-psif" min="0.02" max="0.20" step="0.01" value="0.08" />
    </label>
    <label style="display: flex; flex-direction: column; font-size: 0.9rem;">
      <span><strong>$L_d$ (mH):</strong> <span id="val-ld">1.2</span> mH</span>
      <input type="range" id="slider-ld" min="0.5" max="5.0" step="0.1" value="1.2" />
    </label>
    <label style="display: flex; flex-direction: column; font-size: 0.9rem;">
      <span><strong>$L_q$ (mH):</strong> <span id="val-lq">3.0</span> mH</span>
      <input type="range" id="slider-lq" min="0.5" max="8.0" step="0.1" value="3.0" />
    </label>
  </div>
  <div id="mtpa-readout" style="font-size: 0.95rem; margin-bottom: 0.75rem; font-weight: 500;"></div>
  <div id="live-pmsm-plot" style="width: 100%; height: 420px;"></div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    function renderPMSM() {
      if (typeof Plotly === "undefined") {
        setTimeout(renderPMSM, 150);
        return;
      }
      const p = 4; // pole pairs
      const Is = parseFloat(document.getElementById("slider-is").value);
      const psif = parseFloat(document.getElementById("slider-psif").value);
      const Ld = parseFloat(document.getElementById("slider-ld").value) * 1e-3;
      const Lq = parseFloat(document.getElementById("slider-lq").value) * 1e-3;

      document.getElementById("val-is").textContent = Is.toFixed(0);
      document.getElementById("val-psif").textContent = psif.toFixed(2);
      document.getElementById("val-ld").textContent = (Ld * 1e3).toFixed(1);
      document.getElementById("val-lq").textContent = (Lq * 1e3).toFixed(1);

      const betas = [];
      const tAlign = [];
      const tReluct = [];
      const tTotal = [];

      let maxT = -Infinity;
      let optBeta = 0;

      for (let b = 0; b <= 90; b += 1) {
        const rad = (b * Math.PI) / 180.0;
        const ta = 1.5 * p * psif * Is * Math.cos(rad);
        const tr = 1.5 * p * 0.5 * (Lq - Ld) * Is * Is * Math.sin(2 * rad);
        const tt = ta + tr;
        betas.push(b);
        tAlign.push(ta);
        tReluct.push(tr);
        tTotal.push(tt);
        if (tt > maxT) {
          maxT = tt;
          optBeta = b;
        }
      }

      document.getElementById("mtpa-readout").innerHTML =
        `Pole pairs p = ${p} &nbsp;|&nbsp; Peak MTPA Torque: <strong>${maxT.toFixed(2)} N·m</strong> at advance angle <strong>β* = ${optBeta}°</strong>`;

      const traces = [
        { x: betas, y: tAlign, name: "Alignment Torque", mode: "lines", line: { dash: "dot" } },
        { x: betas, y: tReluct, name: "Reluctance Torque", mode: "lines", line: { dash: "dash" } },
        { x: betas, y: tTotal, name: "Total Torque Te(β)", mode: "lines", line: { width: 3 } },
        {
          x: [optBeta],
          y: [maxT],
          name: "MTPA Operating Point",
          mode: "markers",
          marker: { size: 11, symbol: "diamond" }
        }
      ];

      const layout = {
        margin: { t: 30, r: 20, b: 50, l: 55 },
        xaxis: { title: { text: "Current Advance Angle β (degrees)" } },
        yaxis: { title: { text: "Electromagnetic Torque (N·m)" } },
        legend: { orientation: "h", y: 1.12 }
      };

      Plotly.react("live-pmsm-plot", traces, layout, { responsive: true });
    }

    ["slider-is", "slider-psif", "slider-ld", "slider-lq"].forEach(function (id) {
      const el = document.getElementById(id);
      if (el) el.addEventListener("input", renderPMSM);
    });

    renderPMSM();
  });
</script>
