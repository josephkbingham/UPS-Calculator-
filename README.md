# ⚡ UPS System Calculator — Intellipower

Interactive UPS and DC power-stage simulator with live topology rendering, formula-driven data cards, runtime modeling, and print-ready multi-mode reports.

![Version](https://img.shields.io/badge/Version-2.x-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Single File](https://img.shields.io/badge/App-Single%20HTML-brightgreen)

## 🌟 What It Does

- Live electrical calculations for UPS operating modes: **Normal**, **Charging**, **Battery**, and (when supported) **Bypass**
- Topology switching:
   - **WRPFC front-end** (removes transformer path)
   - **DC/DC output stage** (replaces inverter, configurable low-voltage DC output)
- Dynamic SVG system diagram with animated flow, protection state, and mode-aware component visibility
- Runtime-vs-load chart with hover inspection and a runtime calculator (W or % input)
- Detailed formula tooltips on dashboard rows (step-by-step derivation)
- Thermal estimate and airflow requirement using:
   - $CFM = (3.16 \times P_{heat})/\Delta T$
- Print View that renders all available modes in a report layout

## 🧩 Key Features

### Topology & Power Path
- Transformer + PFC or **WRPFC** selectable
- Inverter AC output or **DC/DC converter output** selectable
- Fixed 400 V DC bus model
- Mode-dependent energy flow visualization

### Battery Modeling
- Cell + pack inputs: voltage, min voltage (EOD), Ah, max discharge current, S/P counts
- Peukert support:
   - direct entry
   - calculated from 20-hour and 5-hour Ah data
- Pack current checks and EOD current validation

### Protection
- Input and output circuit breaker checks
- Boost and charger fuse checks (F1/F2)
- Warning banner for trips/over-limit conditions

### Reporting & UX
- Formula-aware data cards with hover explanations
- Runtime graph + highlight point from calculator input
- Print tab with per-mode diagrams and warning summaries

## 🚀 Quick Start

```bash
git clone https://github.com/josephkbingham/UPS-Calculator-.git
cd UPS-Calculator-
start ups-simulator.html
```

### Runtime Notes
- No local build step required.
- App uses browser-loaded CDN scripts for React and Babel (internet connection required).
- Recommended browsers: modern Chrome, Edge, Firefox, or Safari.

## 📖 Usage Guide

1. Pick **Calculator** tab and choose mode.
2. Configure topology:
    - enable/disable **WRPFC**
    - enable/disable **DC/DC Output**
3. Enter power, battery, efficiency, protection, and condition parameters.
4. Review:
    - live topology diagram
    - dashboard values + formula tooltips
    - runtime chart and runtime calculator
5. Switch to **Print View** for all-mode report output and print/export to PDF.

## 🔬 Core Model Notes

- Output stage efficiency is selected by topology:
   - inverter efficiency or DC/DC efficiency
- WRPFC mode removes transformer loss from front-end chain
- Runtime model includes Peukert correction and efficiency chain
- Thermal model sums stage losses and computes required airflow

## 🛠️ Project Structure

```text
UPS-Calculator-/
├── ups-simulator.html    # Single-file React app (via CDN + Babel)
├── README.md
├── LICENSE
└── .gitignore
```

## 🧪 Implementation Highlights

- `calcSystem()` handles mode/topology electrical calculations and warnings
- `calcRuntime()` computes runtime using Peukert-adjusted discharge behavior
- `Diagram` renders the animated SVG topology view
- `RuntimeChart` renders the load/runtime curve in SVG
- `UPSCalculator` manages UI state, tabs, and report composition

## 📝 License

MIT License — see [LICENSE](LICENSE).

## 👤 Author

**Joseph Bingham**  
GitHub: [@josephkbingham](https://github.com/josephkbingham)

## 📞 Support

Issues and feature requests: [open an issue](https://github.com/josephkbingham/UPS-Calculator-/issues)
