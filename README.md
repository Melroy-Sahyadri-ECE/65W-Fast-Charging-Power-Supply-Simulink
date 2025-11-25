# 65W Fast Charging Power Supply - Simulink Model

A complete Simulink model of a 65W USB Power Delivery (USB-PD) fast charging power supply with closed-loop feedback control.

## 🚀 Features

- **USB-PD Protocol Support**: Automatic voltage negotiation (5V → 20V)
- **65W Maximum Power**: Limited to 20V @ 3.25A
- **Closed-Loop Control**: PI controller with feedback regulation
- **Safety Limits**: Voltage, current, and power limiting
- **Complete Monitoring**: 14 scopes + 3 displays for all signals
- **Professional Design**: Clean architecture with proper isolation

## 📊 Specifications

| Parameter | Value |
|-----------|-------|
| Input Voltage | 230V AC (50Hz) |
| Output Voltage | 5V / 20V (USB-PD) |
| Maximum Power | 65W |
| Maximum Current | 3.25A |
| Switching Frequency | 20kHz |
| Voltage Ramp Rate | 30V/s |

## 🔧 System Architecture

```
AC Input (230V) → EMI Filter → Bridge Rectifier → Bulk Capacitor (310V DC)
                                                          ↓
                                                    Power Stage
                                                          ↓
                                            Transformer (10:1 ratio)
                                                          ↓
                                        Secondary Rectification + Filtering
                                                          ↓
                                                Output (5V/20V, 65W max)
                                                          ↓
                                                    Feedback Path
                                                          ↓
                                            PWM Controller (PI Control)
```

## 📁 Files

- `create_perfect_fast_charging.m` - Main MATLAB script to build the Simulink model
- `power_supply_block_diagram.png` - System block diagram
- `README.md` - This file

## 🎯 Quick Start

### Prerequisites
- MATLAB R2020a or newer
- Simulink
- Simulink Control Design Toolbox

### Running the Model

1. Clone this repository:
```bash
git clone https://github.com/YOUR_USERNAME/65w-fast-charging-simulink.git
cd 65w-fast-charging-simulink
```

2. Open MATLAB and navigate to the project directory

3. Run the script:
```matlab
create_perfect_fast_charging
```

4. The Simulink model `FastCharging_65W_Perfect.slx` will be created and opened automatically

5. Click **Run** to simulate (2 seconds simulation time)

## 📈 Simulation Timeline

| Time | Event | Output Voltage | Power |
|------|-------|----------------|-------|
| 0 - 0.1s | Standby | 5V | ~5W |
| 0.1s | Phone connected | 5V | ~5W |
| 0.3s | Fast charge request | 5V → 20V | Ramping |
| 0.8s+ | Fast charging | 20V | 65W |

## 🔍 Key Components

### USB-PD Protocol
- Phone detection at t=0.1s
- Fast charge negotiation at t=0.3s
- Smooth voltage transition with rate limiting

### Power Stage
- Flyback topology with transformer isolation
- Primary MOSFET switching at 20kHz
- Synchronous rectification on secondary

### Control System
- PI controller (P=0.15, I=20)
- Closed-loop feedback with optocoupler isolation
- Error-driven PWM generation

### Safety Features
- Voltage limiter: 20V maximum
- Current limiter: 3.25A maximum
- Power limiter: 65W maximum

## 📊 Monitoring Points

The model includes comprehensive monitoring:

- **Scope_USBPD**: USB-PD protocol signals
- **Scope_Before_Phone**: Voltage before phone connection
- **Scope_After_Phone**: Voltage after phone connection
- **Scope_Voltage_Ramp**: Voltage ramp (5V→20V)
- **Scope_Power_65W**: Power output (≤65W)
- **Scope_AC**: AC input waveform
- **Scope_Rectified**: Rectified DC voltage
- **Scope_PWM**: PWM control signal
- **Scope_Primary**: Primary side voltage
- **Scope_Secondary**: Secondary side voltage
- **Scope_Feedback**: Feedback signal
- **Scope_Output**: Final output voltage
- **Display_Voltage**: Real-time voltage display
- **Display_Power**: Real-time power display
- **Display_State**: USB-PD state display

## 🛠️ Customization

### Changing Output Voltage
Edit the `FastCharge_20V` constant block value (default: 20V)

### Adjusting Power Limit
Edit the `Power_Limiter_65W` upper limit (default: 65W)

### Tuning PI Controller
Modify PI_Controller parameters:
- Proportional gain (P): default 0.15
- Integral gain (I): default 20

## 📝 Technical Details

### Component Values
- Bulk Capacitor: 470µF
- EMI Filter: 1ms time constant
- Output Inductor: 100µH
- Output Capacitors: 220µF
- Transformer Ratio: 10:1 (0.1 gain)

### Control Loop
- Sampling: Continuous
- Solver: ode45 (variable-step)
- Simulation time: 2.0 seconds

## 🐛 Troubleshooting

**Model won't open:**
- Ensure you have Simulink installed
- Check MATLAB version compatibility

**Simulation errors:**
- Verify all toolboxes are installed
- Check solver settings (should be ode45)

**Unexpected output:**
- Review scope signals for debugging
- Check USB-PD timing (0.1s, 0.3s)

## 📄 License

MIT License - Feel free to use and modify

## 👤 Author

Created for power electronics education and simulation

## 🤝 Contributing

Contributions welcome! Please feel free to submit a Pull Request.

## ⭐ Acknowledgments

- Based on USB Power Delivery specification
- Flyback converter topology
- PI control theory

---

**Note**: This is a simulation model for educational purposes. Real-world implementation requires additional safety features, EMI compliance, and proper component selection.
