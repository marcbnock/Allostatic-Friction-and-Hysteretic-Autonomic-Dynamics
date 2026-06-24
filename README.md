## 1. Project Abstract & Theoretical Overview

The **Allostatic-Friction-and-Hysteretic-Autonomic-Dynamics** framework provides a computational, mathematical, and simulation-driven toolkit designed to model the non-linear path dependency (**hysteresis loops**) and active metabolic energy dissipation (**allostatic friction**) within the human nervous system. 

Conventional health metrics focus primarily on static biomonitoring, evaluating isolated component integrity (e.g., resting heart rate, blood panels, or hormone assays). This repository shifts the paradigm upstream, treating the brainstem's autonomic core—specifically the **Parabrachial Nucleus (PBN)**, the **Nucleus Tractus Solitarius (NTS)**, and the **Reticular Activating System (RAS)**—as a non-linear, path-dependent dynamic control network.

### The Problem Space
When an individual exhibits a compromised craniofacial or upper-airway architecture (such as a retrognathic mandible, narrow inter-molar width, or collapsed maxilla), the respiratory pathway becomes a mechanical bottleneck. To prevent airway collapse during standard behavior and sleep states, the brainstem executes automatic, life-saving fallback protocols. It commands continuous, high-frequency isometric contractions of the accessory muscles of the neck, jaw, and cervical spine to prop the airway open. 

This mechanical workaround siphons a massive daily budget of metabolic energy (ATP) and floods the central nervous system with chronic spatial noise via Cranial Nerve V (The Trigeminal Afferent Deluge). This continuous background processing tax is defined here as **Allostatic Friction**. 

Furthermore, this repository models the **Hysteresis Layer** of autonomic biology. In highly hysteretic dynamic systems, the path required to return to a baseline state of rest is entirely distinct from the path taken to enter a state of crisis. When an external psychological or lifestyle stressor drops to zero (e.g., a "stress sabbatical"), the internal system remains locked in a high-vigilance sympathetic attractor because the uncorrected hardware error continues to act as an anchor, preventing the baseline from resetting.

---

## 2. Mathematical Foundations

The framework tracks the evolution of an autonomic state vector, $x(t)$, restricted to the domain $x \\in [0, 1]$, where:
* $x \\to 0$ represents complete parasympathetic access, high signal fidelity, and optimal systemic restoration.
* $x \\to 1$ represents maximum sympathetic drive, elevated allostatic load, and systemic bandwidth exhaustion.

### 2.1 The Governing Non-Linear State Equation
The state vector's progression over time is determined by a coupled non-linear differential system factoring in the potential energy landscape of the structure, trigeminal sensory flux, and a convolution historical memory kernel:

$$\\frac{dx}{dt} = -\\nabla V(x, \\theta) + \\mu_{af}(\theta)\\Phi_{trigeminal}(t) + \\int_{t_0}^{t} \\Gamma(x, \\tau) e^{-\\lambda(t-\\tau)} d\\tau$$

Where:
* $V(x, \\theta)$ is the structural potential energy well, parameterized by the multi-dimensional craniofacial misalignment vector $\theta$.
* $\mu_{af}(\theta)$ represents the dimensionless **Allostatic Friction Coefficient**.
* $\Phi_{trigeminal}(t)$ represents the instantaneous informational flux of the Trigeminal Afferent Deluge, measured in bits/second or high-frequency neural spike arrays.
* $\\int_{t_0}^{t} \\Gamma(x, \\tau) e^{-\\lambda(t-\\tau)} d\\tau$ is the memory integral representing the historical path dependency, scaled by the memory decay constant $\lambda$.

### 2.2 The Allostatic Friction Coefficient ($Ref: C_{af}$)
The metabolic overhead required to preserve physiological homeostatic equilibrium scales exponentially as a function of upper airway volume constriction ($\Omega_{airway}$) and skeletal jaw retrusion vectors:

$$\\mu_{af}(\theta) = \\alpha \\cdot \\exp\\left( \\frac{\\theta_{recession}}{\\Omega_{airway}} \\right) + \\beta \\cdot \\sum_{i=1}^{n} \\|\\vec{F}_{isometric, i}\\|$$

Where:
* $\\alpha$ and $\\beta$ are biological scaling constants derived from systemic control loops.
* $\\Omega_{airway}$ represents the minimum three-dimensional cross-sectional area of the pharyngeal airway.
* $\\vec{F}_{isometric, i}$ represents the isometric force vector of the $i$-th accessory muscle unit engaged in stabilizing the craniomandibular frame against gravity.

### 2.3 The Hysteresis Loop Transform
The state engine implements a modified Duhem model for path-dependent hysteresis, tracking the system's autonomic behavior under varying external workloads:

$$\\frac{dx}{dE} = f(x, E) \\cdot \\text{sgn}(\\dot{E}) + g(x, E)$$

Where $E$ represents the net external environmental input, demonstrating that the forward path ($E$ increasing) and the relaxation path ($E$ decreasing) do not overlap when internal structural noise creates a permanent operational floor.

---

## 3. Codebase Architecture & Directory Structure
