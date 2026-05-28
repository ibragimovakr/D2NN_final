# D2NN — Diffractive Deep Neural Network

> **Optical implementation of a deep neural network via phase-modulating diffractive layers**  
> *Rodion Akinzhala, Ibragimova Ksenia*

---

## Overview

**D2NN** (Diffractive Deep Neural Network) is an all-optical computing architecture in which learned parameters are encoded as **phase profiles** on physical diffractive masks. Free-space wave propagation between masks performs the nonlinear field transformation, enabling inference at the speed of light with no electronic computation at test time.

The forward pass through $N$ layers is:

$$A_{\text{out}} = \mathcal{P}_{d_N} \circ e^{i\varphi_N} \circ \mathcal{P}_{d_{N-1}} \circ \cdots \circ e^{i\varphi_1} \circ \mathcal{P}_{d_0} \[{A_{\text{in}}\} ]$$

where $P_d$ denotes free-space Angular Spectrum Propagation over distance $d$, and $e^{i\varphi_m}$ is the phase modulation at layer $m$. The classifier reads the output intensity $I(x,y) = |A_{\text{out}}(x,y)|^2$ at a segmented detector plane.

**Trainable parameters:** phase profiles $\{\varphi_1, \ldots, \varphi_N\}$  
**Fixed parameters:** inter-layer distances $\{d_1, \ldots, d_{N-1}\}$

---

## Contributions

- **Novel Gerchberg–Saxton initialization.** A modified Gerchberg–Saxton algorithm is developed to produce physically structured initial phase masks, replacing the standard $\mathcal{U}[-\pi,\pi]$ random initialization. The procedure minimizes $\|{|B^{(k)}|} - |A_{\text{out}}|\|_2^2$ via alternating projections onto constraint sets and is proven to converge monotonically. This yields faster training convergence and higher final accuracy compared to random initialization.

- **Robustness characterization.** Systematic evaluation of model sensitivity to (i) source wavelength variation and (ii) proportional Gaussian phase noise $\delta \sim \mathcal{N}(0,\, \alpha^2\varphi^2)$, establishing practical tolerances.


## Repository Structure

```
D2NN/
├── code/       # Simulation, training, and analysis scripts
└── docs/    # Presentation materials and figures
```
