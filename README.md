# 2.4 GHz Half-Wave Dipole Antenna — CST Simulation

A **simulation-based design and analysis** of a half-wave dipole antenna targeting the **2.4 GHz band**, using **CST Studio Suite Learning Edition**. The project covers the initial analytical design, dimensional optimization, impedance matching, and far-field radiation characteristics.

**[Türkçe README](README_TR.md)** · **[Full technical report (Turkish, PDF)](report/2.4GHz_Dipole_Antenna_Design_and_Simulation_Report_TR.pdf)**

![Dipole antenna model in CST](figures/01_antenna_geometry.png)

## Project overview

The initial dimensions were calculated from the free-space wavelength. An initial simulated resonance near **2.19 GHz** led to a shorter arm length, shifting the simulated response toward the **2.4 GHz** target. The model was evaluated using CST's **Time Domain Solver** and far-field results.

This is a **simulation study**, not a fabrication or experimental measurement report.

## Design parameters

| Parameter | Value |
|---|---:|
| Target frequency | 2.4 GHz |
| Free-space wavelength | 125 mm |
| Initial theoretical arm length (λ/4) | 31.25 mm |
| Optimized arm length (each side) | 28.5 mm |
| Total optimized conductor length (excluding gap) | ~57.0 mm |
| Conductor diameter | 1 mm |
| Feed gap | 1 mm |
| Reference/port impedance | 50 Ω |
| Solver | CST Time Domain Solver |

Key design relationships:

$$
\lambda_0 = \frac{c}{f_0}, \qquad
L_{\mathrm{theoretical}} = \frac{\lambda_0}{2}
$$

An approximate shortening ratio of **2.19 / 2.40 ≈ 0.9125** was used to guide the change from **31.25 mm** to **28.5 mm** per arm. This ratio is specific to this design iteration, not a universal dipole correction factor.

## Simulation results

| Metric | Reported result |
|---|---:|
| Resonance region | ~2.4 GHz |
| Minimum S₁₁ | ~−14.8 dB |
| −10 dB frequency range | ~2.31–2.49 GHz |
| −10 dB bandwidth | ~180 MHz |
| Fractional bandwidth | ~7.5% |
| VSWR near resonance | ~1.45 |
| Reflected power fraction near S₁₁ minimum | ~3.31% |
| Maximum directivity | ~2.092 dBi |
| Maximum gain (CST result) | ~2.095 dBi |
| Maximum realized gain | ~1.948 dBi |
| Total efficiency (CST result) | ~96.75% |
| Half-power beamwidth, φ = 90° cut | ~78.6° |

All values are approximate readings or calculations from the provided CST report. The gain is marginally above the directivity in the displayed simulation results; the report attributes this small nonphysical difference to numerical precision, not a physical efficiency greater than 100%.

### S₁₁ and impedance matching

![Simulated S11 versus frequency](figures/02_s11_response.png)

At the reported minimum, **S₁₁ ≈ −14.8 dB**, corresponding to approximately **3.31% reflected power** and **96.69% accepted power** at the simulated port. The reported −10 dB bandwidth is approximately **180 MHz**.

### Three-dimensional radiation patterns

**Directivity**

![3D directivity at 2.4 GHz](figures/03_directivity_3d.png)

**Gain**

![3D gain at 2.4 GHz](figures/04_gain_3d.png)

**Realized gain**

![3D realized gain at 2.4 GHz](figures/05_realized_gain_3d.png)

The patterns show stronger radiation perpendicular to the antenna axis and a null near the axis, consistent with a half-wave dipole.

### Two-dimensional radiation pattern

![2D far-field polar pattern, phi 90 degrees](figures/06_e_plane_radiation_pattern.png)

The reported **half-power beamwidth (HPBW)** is approximately **78.6°** for the **φ = 90°** cut.

## Proposed feed cable and limitations

The report proposes **RG-178 B/U**, a **50 Ω coaxial cable**, as a possible feed for the **1 mm gap**. This is a design recommendation only:

- The coaxial cable was **not modeled physically** in CST.
- Cable, connector, common-mode current, and actual feed-connection effects are therefore **not represented** in the reported results.
- The suitability of a physical implementation requires additional electromagnetic and mechanical verification.
- This repository contains **report figures and the PDF**, but **not the editable CST project file or raw solver data**.

## Repository structure

```text
2.4GHz-Dipole-Antenna-CST/
├── README.md
├── README_TR.md
├── figures/
│   ├── 01_antenna_geometry.png
│   ├── 02_s11_response.png
│   ├── 03_directivity_3d.png
│   ├── 04_gain_3d.png
│   ├── 05_realized_gain_3d.png
│   └── 06_e_plane_radiation_pattern.png
├── report/
│   └── 2.4GHz_Dipole_Antenna_Design_and_Simulation_Report_TR.pdf
└── .gitignore
```

## Suggested next steps

Model the coaxial/balun feed explicitly, perform mesh-convergence and dimensional sweeps, and compare simulation predictions with measurements after building a prototype.

*All figures originate from the attached CST simulation report. The original PDF content has been retained without technical edits.*
