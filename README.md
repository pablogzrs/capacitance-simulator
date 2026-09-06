# 🔌 Capacitive Liquid Level Sensor

MATLAB App Designer simulator of a capacitive liquid-level probe: given a measured capacitance and a known dielectric, it infers the liquid level and renders the filled container in 3D.

## 📋 Overview

A parallel-plate capacitor is submerged vertically in a container. As liquid rises between the plates, part of the gap is filled by the liquid's dielectric and part remains air, so the probe behaves as two capacitors in parallel and its total capacitance rises with the level.

The app inverts that relationship. You pick a liquid, set a capacitance on the slider, and it solves for the height, reports the corresponding volume, and draws the container with the liquid at that level.

## 📐 Physical Model

For plates of width `α` and height `L`, separated by `d`, submerged to a depth `L₂` in a liquid of relative permittivity `k`:

```
C = (ε₀·α / d) · [ L + (k − 1)·L₂ ]
```

Solved for the level, which is what the app actually computes:

```
L₂ = (1 / (k − 1)) · [ C·d / (ε₀·α) − L ]
```

**Geometry (hardcoded):**

| Parameter | Symbol | Value |
|---|---|---|
| Vacuum permittivity | ε₀ | 8.85 × 10⁻¹² F/m |
| Plate separation | d | 0.005 m (0.5 cm) |
| Plate width | α | 0.066 m (6.6 cm) |
| Plate height | L | 0.04 m (4 cm) |
| Container | — | 10 × 10 × 4 cm |

With the probe empty (`L₂ = 0`), the baseline capacitance is `ε₀·α·L / d ≈ 4.67 pF`. Below that the model has no physical solution, which is why the slider starts at 5 pF.

## 🧪 Dielectrics

Each option carries its relative permittivity and a full-scale capacitance — the value the probe reads when the liquid reaches the top of the plates.

| Liquid | k | Full scale | Render color |
|---|---|---|---|
| Agua (Teórica) | 80 | 373 pF | blue |
| Vino | 25 | 116 pF | magenta |
| Vinagre | 24 | 112 pF | red |
| Aceite de Oliva | 3.1 | 14 pF | yellow |
| Aceite de Silicón | 2.5 | 11 pF | white |
| Agua (Experimental) | — | 37–98 pF | blue |

**Agua (Experimental)** is the one option that does not use the formula above. It applies a linear fit to measured data instead:

```
L₂ = 6.4687×10⁸ · C − 0.023622
```

valid over 37–98 pF, which maps to empty and full respectively.

The gap between the two water entries is the most interesting result in the project: theory predicts 373 pF at full immersion, measurement gives about 98 pF — off by a factor of roughly 3.8. Real water is not an ideal dielectric at the measurement frequency, and conductivity and electrode effects pull the effective permittivity well below the textbook value of 80.

## 🖥️ Interface

- **Dieléctrico** — dropdown, six liquids
- **Capacitancia (pF)** — slider, range 5 to 373
- **Inicio** — computes and redraws
- **Rangos posibles (pF)** — reference panel listing each liquid's valid ceiling
- **Elevación de líquido (cm)** — computed output
- **Volumen (mL)** — computed output, `100 × height`, since the container cross-section is 100 cm²
- **3D axes** — transparent container, opaque liquid at the solved level, the two black plates, and a filled liquid surface

## 🚀 How to Run

Requires MATLAB with App Designer (R2019a or later).

```matlab
>> Tanque_Capacitancia_PROYECTO
```

Or open `Tanque_Capacitancia_PROYECTO.mlapp` in App Designer and press Run. Keep `start.png` and `itesm.png` in the same folder — the button icon and image component load them by relative path.

**First run:** the dropdown defaults to *Agua (Experimental)* and the slider to 5 pF, which is outside that option's valid range. Pressing **Inicio** in that state does nothing. Move the slider into 37–98 pF, or switch to another liquid, before pressing it.


## 🎓 Academic Context

**Institution:** ITESM
**Topics:** electrostatics, dielectrics, capacitive sensing, inverse measurement, MATLAB App Designer

## 📝 Notes

The `drawCuboid` 3D prism helper was generated with AI assistance (ChatGPT), as documented in a comment in the source.
