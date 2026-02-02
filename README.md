# ⚡ UPS System Simulator

A comprehensive, interactive **Uninterruptible Power Supply (UPS)** simulator built with pure HTML5, CSS3, and JavaScript. This tool provides real-time energy flow visualization, accurate electrical calculations, advanced battery runtime analysis, and thermal management insights.

![UPS Simulator](https://img.shields.io/badge/Version-1.0.0-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Dependencies](https://img.shields.io/badge/Dependencies-None-brightgreen)

## 🌟 Features

### 📊 **Real-Time Energy Flow Visualization**
- **Animated Block Diagram**: Watch energy flow through the UPS system with 60fps particle animations
- **Color-Coded Modes**: Visual feedback for different operating states
  - 🟢 **Normal Mode**: Grid power → PFC → Inverter → Load
  - 🔵 **Charging Mode**: Normal operation + battery charging
  - 🟡 **Battery Mode**: Battery → Boost → Inverter → Load
  - ⚪ **Bypass Mode**: Direct grid power to load

### ⚡ **Comprehensive Electrical Calculations**
- **Multi-Stage Power Analysis**: Track voltage, current, and power at every component
- **Transformer Modeling**: Configurable turns ratio and efficiency
- **PFC (Power Factor Correction)**: Accurate rectifier power calculations with charger load
- **DC Bus**: Fixed 400V rail with dynamic current calculations
- **Dual Output Modes**:
  - **Resistive Load**: Pure real power (PF = 1.0)
  - **Reactive Load**: Maximum VA rating utilization
- **Circuit Breaker Protection**: Automatic trip warnings for overcurrent

### 🔋 **Advanced Battery Analysis**
- **Series/Parallel Configuration**: Flexible battery bank design (NsP format)
- **Peukert Effect**: Industry-standard capacity correction for discharge rates
- **End-of-Discharge Monitoring**: Voltage and current limit enforcement
- **Charging Simulation**: Power-limited constant current charging
- **Runtime Prediction**: Peukert-corrected runtime curves

### 📈 **Interactive Runtime Graph**
- **Dynamic Load Curves**: Automatic plotting from target load down to minimum
- **100W Resolution**: Hover points at practical load increments
- **Runtime Calculator**: 
  - Enter specific load (Watts or %)
  - Instant runtime calculation
  - Automatic tooltip synchronization
- **Smart Scaling**: Adaptive axis ranges for optimal visibility

### 🌡️ **Thermal Management**
- **Heat Dissipation Tracking**: Calculates losses from all inefficiencies
- **Required Cooling**: CFM calculation based on temperature rise
- **Component Efficiency**: Separate efficiency settings for each stage

### 🎛️ **Flexible Configuration**
- **Input Voltage Control**: Separate grid input and UPS output voltages
- **Low-Line Mode**: Simulate voltage sag conditions
- **Overload Mode**: Test system response to load spikes
- **Component Efficiencies**: Customize PFC, inverter, charger, boost performance
- **Charger Power Limit**: Configurable maximum charging power

## 🚀 Quick Start

### Installation
```bash
# Clone the repository
git clone https://github.com/josephkbingham/UPS-Calculator-.git

# Navigate to the directory
cd UPS-Calculator-

# Open in your browser
start ups-simulator.html  # Windows
open ups-simulator.html   # macOS
xdg-open ups-simulator.html  # Linux
```

### No Dependencies Required!
This simulator is built with **zero external dependencies**. Just open the HTML file in any modern browser:
- Chrome 90+
- Firefox 88+
- Edge 90+
- Safari 14+

## 📖 User Guide

### Basic Operation

1. **Select Operating Mode**
   - Click one of the four mode buttons (Normal, Charging, Battery, Bypass)
   - Watch the animated block diagram update to show energy flow

2. **Configure Power Settings**
   - **Grid Input Voltage**: AC voltage from utility (default 115V)
   - **Output Voltage**: UPS output voltage (default 115V)
   - **Target Output Power**: Desired load in Watts (default 1000W)
   - **VA Rating**: Maximum apparent power capacity (default 1200VA)

3. **Design Battery System**
   - **Cell Configuration**: Series count (voltage) × Parallel count (capacity)
   - **Cell Specifications**: Voltage (12V) and capacity (10Ah)
   - **End-of-Discharge**: Minimum safe voltage (10.5V per cell)

4. **Analyze Runtime**
   - View the runtime curve showing minutes vs load
   - Use the **Runtime Calculator** to check specific load points
   - Enter load in Watts or % of target power
   - Tooltip automatically snaps to calculated point

### Advanced Features

#### Low-Line Mode
Simulate voltage sag conditions:
- Enable "Low-Line Voltage Mode"
- Set tolerance percentage (e.g., 15% = 97.75V from 115V)
- Observe impact on input current and transformer loading

#### Overload Testing
Test system response to load spikes:
- Enable "Overload Mode"
- Set overload percentage (e.g., 20% = 1200W from 1000W)
- Check for circuit breaker trips or VA limit warnings

#### Reactive Load Analysis
Switch between resistive and reactive loads:
- **OFF**: Pure resistive load (PF = 1.0, VA = W)
- **ON**: Maximum reactive scenario (VA = rating, higher current)

#### Peukert Effect
Adjust battery discharge characteristics:
- **Coefficient (n)**: 1.0 (ideal) to 1.3 (lead-acid typical)
- Default: 1.2 for realistic lead-acid behavior
- Higher loads reduce effective capacity

## 🔬 Technical Details

### Electrical Model

**Normal Mode Energy Flow:**
```
Grid (115V) → Transformer → PFC (400VDC) → Inverter → Load
```

**Battery Mode Energy Flow:**
```
Battery → Boost (400VDC) → Inverter → Load
```

**Charging Mode Energy Flow:**
```
Grid → Transformer → PFC → [Inverter → Load + Charger → Battery]
```

### Key Calculations

**PFC Input Power (Normal):**
```
P_pfc = P_load / (η_pfc × η_inverter)
```

**PFC Input Power (Charging):**
```
P_pfc = [P_load / η_inverter + P_charger] / η_pfc
```

**Battery Current (Discharge):**
```
I_battery = P_load / (η_boost × η_inverter × V_battery)
```

**Peukert-Corrected Capacity:**
```
C_effective = C_rated × (I_rated / I_actual)^(n-1)
```

**Runtime:**
```
Runtime = C_effective × V_battery × η_total / P_load
```

**Required Cooling (CFM):**
```
CFM = (3.16 × P_heat) / ΔT
```

### Default Component Efficiencies
- **Transformer**: 95%
- **PFC (Rectifier)**: 92%
- **Inverter**: 90%
- **Charger**: 85%
- **Boost Converter**: 88%

## 📊 Example Configurations

### Small Home UPS (1000W)
```
Grid Voltage: 115V
Output Voltage: 115V
Target Power: 1000W
VA Rating: 1200VA
Battery: 10S×1P (120V, 10Ah)
Runtime @ 1000W: ~8 minutes
```

### Medium Office UPS (1500W)
```
Grid Voltage: 115V
Output Voltage: 115V
Target Power: 1500W
VA Rating: 2000VA
Battery: 10S×2P (120V, 20Ah)
Runtime @ 1500W: ~11 minutes
```

### Large Server UPS (3000W)
```
Grid Voltage: 230V
Output Voltage: 230V
Target Power: 3000W
VA Rating: 4000VA
Battery: 20S×3P (240V, 30Ah)
Runtime @ 3000W: ~20 minutes
```

## 🎨 Visual Design

- **Modern UI**: Clean, professional interface with gradient headers
- **Responsive Layout**: Adapts to different screen sizes
- **Color-Coded Warnings**: Red banner for critical issues
- **Smooth Animations**: 60fps particle effects with glowing trails
- **Interactive Tooltips**: Hover over graph for precise data
- **Formula Display**: Transparent calculations shown to user

## 🛠️ Development

### Project Structure
```
UPS-Calculator-/
├── ups-simulator.html    # Single-file application (1607 lines)
├── README.md            # This documentation
├── LICENSE              # MIT License
└── .gitignore          # Git ignore rules
```

### Technology Stack
- **HTML5 Canvas**: Hardware-accelerated graphics rendering
- **Vanilla JavaScript**: No frameworks, optimal performance
- **CSS3**: Modern styling with flexbox and grid
- **requestAnimationFrame**: Smooth 60fps animations

### Code Architecture
```javascript
// Core components:
- calculateSystem()        // Main electrical engine
- drawDiagram()           // Canvas block diagram
- drawRuntimeGraph()      // Battery runtime plotting
- Particle class          // Animation system
- updateDashboard()       // UI data binding
```

## 🐛 Known Limitations

- **Fixed DC Bus**: 400V rail cannot be changed
- **Linear Battery Model**: Voltage drop during discharge not modeled
- **Simplified Thermal**: Assumes uniform ambient temperature
- **No Transient Analysis**: Steady-state calculations only

## 🚧 Future Enhancements

- [ ] Export runtime data to CSV
- [ ] Save/load configurations
- [ ] Battery temperature modeling
- [ ] Multi-battery string comparison
- [ ] Efficiency vs load curves
- [ ] Print-friendly reports
- [ ] Dark mode theme

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details

## 👤 Author

**Joseph Bingham**
- GitHub: [@josephkbingham](https://github.com/josephkbingham)

## 🙏 Acknowledgments

- Inspired by real-world UPS systems from APC, Eaton, and Vertiv
- Battery modeling based on Peukert's Law (1897)
- Thermal calculations from ASHRAE standards

## 📞 Support

Found a bug or have a feature request? Please [open an issue](https://github.com/josephkbingham/UPS-Calculator-/issues)

---

**Made with ⚡ for electrical engineers, system designers, and UPS enthusiasts**
