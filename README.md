# ⚡ Tank Capacitance Simulator

MATLAB App Designer application for simulating coupled tank systems with capacitance dynamics.

## 📋 Overview

Interactive simulator for modeling liquid level behavior in coupled tanks. Built as an educational tool for understanding control systems and fluid dynamics concepts.

## ✨ Features

- Interactive parameter controls for tank geometry and flow rates
- Real-time visualization of tank levels
- Graphical plots of system response
- Adjustable simulation parameters

## 🛠️ Technologies

- **Platform:** MATLAB R2020a or later
- **Tool:** App Designer
- **Format:** `.mlapp`

## 📁 Files

```
.
├── Tanque_Capacitancia_PROYECTO.mlapp    # Main application
├── start.png                              # UI assets
├── itesm.png                             # Branding
└── README.md
```

## 🚀 How to Run

**In MATLAB:**
```matlab
>> Tanque_Capacitancia_PROYECTO
```

**Or:**
1. Open MATLAB
2. Double-click `Tanque_Capacitancia_PROYECTO.mlapp`
3. Click Run

## 📐 System Model

Simulates coupled tank equations:

```
Tank 1: A₁(dh₁/dt) = Qᵢₙ - (h₁ - h₂)/R₁
Tank 2: A₂(dh₂/dt) = (h₁ - h₂)/R₁ - h₂/R₂
```

Where:
- h₁, h₂ = Tank levels
- A₁, A₂ = Tank areas
- R₁, R₂ = Valve resistances
- Qᵢₙ = Input flow rate

## 🎓 Academic Context

Developed at Tecnológico de Monterrey for control systems coursework.

## 📦 Deployment

**For MATLAB users:** Share the `.mlapp` file

**Standalone version:**
```matlab
>> mcc -m Tanque_Capacitancia_PROYECTO.mlapp
```

Requires MATLAB Runtime for users without MATLAB.

---

**Institution:** ITESM  
**Platform:** MATLAB App Designer
