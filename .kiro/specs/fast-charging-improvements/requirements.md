# Requirements Document

## Introduction

This specification defines improvements to the existing 65W USB Power Delivery fast charging power supply Simulink model. The current model has a disconnected feedback loop, simplified component modeling, and static load behavior. This enhancement will fix critical control loop issues, add realistic component models, implement dynamic load simulation, and improve overall system accuracy while maintaining the existing USB-PD protocol and safety features.

## Glossary

- **USB-PD**: USB Power Delivery protocol for negotiating power levels between charger and device
- **PWM Controller**: Pulse Width Modulation controller that regulates output voltage through duty cycle adjustment
- **Feedback Loop**: Control system path that measures output voltage and adjusts PWM to maintain regulation
- **Optocoupler**: Galvanic isolation component that transfers feedback signal across transformer barrier
- **VCC Supply**: Auxiliary voltage supply that powers the control circuitry
- **Dynamic Load**: Variable current draw that changes based on battery state of charge
- **Synchronous Rectifier**: Active MOSFET-based rectification on secondary side for improved efficiency
- **Bulk Capacitor**: Large capacitor that smooths rectified AC voltage on primary side
- **EMI Filter**: Electromagnetic interference filter at AC input
- **Rate Limiter**: Component that controls voltage transition speed during USB-PD negotiation

## Requirements

### Requirement 1

**User Story:** As a power electronics engineer, I want the feedback loop properly connected to the PWM controller, so that the output voltage is actively regulated through closed-loop control.

#### Acceptance Criteria

1. WHEN the feedback signal is generated from the output voltage THEN the Feedback System SHALL route the signal through the voltage divider, operational amplifier, optocoupler, and filter to the PWM controller error input
2. WHEN the output voltage deviates from the reference voltage THEN the PWM Controller SHALL adjust the duty cycle to correct the error
3. WHEN the system reaches steady state THEN the Output Voltage SHALL remain within 2% of the reference voltage
4. WHEN a load transient occurs THEN the Feedback System SHALL respond within 50 milliseconds to restore regulation
5. WHEN the feedback path is traced from output to PWM controller THEN the Signal Path SHALL be continuous with no disconnected segments

### Requirement 2

**User Story:** As a simulation engineer, I want realistic component models instead of simplified gain blocks, so that the simulation accurately represents physical hardware behavior.

#### Acceptance Criteria

1. WHEN modeling the primary MOSFET THEN the MOSFET Model SHALL include on-resistance, switching losses, and body diode characteristics
2. WHEN modeling the secondary rectifier THEN the Synchronous Rectifier SHALL include forward voltage drop and reverse recovery effects
3. WHEN modeling the transformer THEN the Transformer Model SHALL include magnetizing inductance, leakage inductance, and winding resistance
4. WHEN modeling diodes THEN the Diode Models SHALL include forward voltage drop and dynamic resistance
5. WHEN comparing simplified versus realistic models THEN the Power Loss Calculation SHALL show measurable differences in efficiency

### Requirement 3

**User Story:** As a battery charging system designer, I want dynamic load behavior that simulates actual phone charging, so that the model represents real-world operating conditions.

#### Acceptance Criteria

1. WHEN the battery state of charge is below 80% THEN the Load Model SHALL draw constant current at the maximum rated value
2. WHEN the battery state of charge exceeds 80% THEN the Load Model SHALL transition to constant voltage mode with decreasing current
3. WHEN the charging cycle progresses THEN the Current Draw SHALL decrease from 3.25A to approximately 0.5A following a realistic charging profile
4. WHEN the load current changes THEN the Output Voltage SHALL remain regulated within specification
5. WHEN the simulation completes THEN the Load Model SHALL demonstrate the complete constant-current to constant-voltage transition

### Requirement 4

**User Story:** As a control systems engineer, I want the VCC supply connected to power the PWM controller, so that the auxiliary power architecture is functionally complete.

#### Acceptance Criteria

1. WHEN the bulk DC voltage is established THEN the VCC Supply SHALL generate a regulated auxiliary voltage between 12V and 15V
2. WHEN the VCC voltage is available THEN the PWM Controller SHALL receive power from the VCC supply
3. WHEN the VCC voltage drops below 10V THEN the System SHALL enter undervoltage lockout mode
4. WHEN the AC input is present THEN the VCC Supply SHALL reach operating voltage within 100 milliseconds
5. WHEN monitoring the VCC rail THEN the Voltage Ripple SHALL remain below 500mV peak-to-peak

### Requirement 5

**User Story:** As a validation engineer, I want enhanced monitoring and visualization of the corrected feedback loop, so that I can verify proper closed-loop operation.

#### Acceptance Criteria

1. WHEN the simulation runs THEN the Monitoring System SHALL display the feedback signal at each stage of the feedback path
2. WHEN viewing the error signal THEN the Scope SHALL show the difference between reference voltage and feedback voltage
3. WHEN the PWM duty cycle changes THEN the Display SHALL show the real-time duty cycle percentage
4. WHEN the loop is operating THEN the Phase Margin Indicator SHALL show stability metrics
5. WHEN comparing before and after improvements THEN the Visualization SHALL clearly demonstrate closed-loop regulation versus open-loop behavior

### Requirement 6

**User Story:** As a power supply designer, I want accurate efficiency calculations based on realistic component losses, so that I can evaluate thermal design requirements.

#### Acceptance Criteria

1. WHEN the simulation runs THEN the Efficiency Calculator SHALL compute input power and output power continuously
2. WHEN component losses are modeled THEN the Loss Breakdown SHALL show switching losses, conduction losses, and magnetic losses separately
3. WHEN operating at different load levels THEN the Efficiency Curve SHALL show efficiency versus load current
4. WHEN the output power is 65W THEN the System Efficiency SHALL be between 85% and 92%
5. WHEN thermal analysis is performed THEN the Power Loss Data SHALL be available for each major component

### Requirement 7

**User Story:** As a USB-PD protocol implementer, I want the voltage transition behavior validated during 5V to 20V negotiation, so that I can ensure safe and compliant operation.

#### Acceptance Criteria

1. WHEN USB-PD negotiation completes THEN the Voltage Transition SHALL follow the rate limiter constraints of 30V per second
2. WHEN transitioning from 5V to 20V THEN the Output Voltage SHALL reach 20V within 600 milliseconds
3. WHEN the voltage is ramping THEN the Feedback Loop SHALL maintain active regulation at each intermediate voltage level
4. WHEN the phone is first connected THEN the System SHALL output 5V before USB-PD negotiation
5. WHEN monitoring the transition THEN the Voltage Overshoot SHALL not exceed 10% of the target voltage

### Requirement 8

**User Story:** As a safety engineer, I want verification that all protection limits function correctly with the improved model, so that the system remains safe under all operating conditions.

#### Acceptance Criteria

1. WHEN the output voltage attempts to exceed 20V THEN the Voltage Limiter SHALL clamp the output to 20V maximum
2. WHEN the load attempts to draw more than 3.25A THEN the Current Limiter SHALL restrict current to 3.25A maximum
3. WHEN the calculated power exceeds 65W THEN the Power Limiter SHALL enforce the 65W maximum limit
4. WHEN a short circuit is applied THEN the Protection System SHALL limit current and prevent damage
5. WHEN all three protection mechanisms are tested THEN each Limiter SHALL activate independently and correctly

### Requirement 9

**User Story:** As a model maintainer, I want improved code organization and documentation, so that the model is easier to understand and modify.

#### Acceptance Criteria

1. WHEN reviewing the MATLAB code THEN the Code Structure SHALL use functions for repeated operations
2. WHEN examining component definitions THEN the Parameter Definitions SHALL be grouped in a configuration section at the top
3. WHEN reading the code THEN the Comments SHALL explain the purpose of each major section and critical parameters
4. WHEN modifying parameters THEN the Configuration Section SHALL allow easy adjustment without searching through code
5. WHEN generating the model THEN the Script SHALL include error handling for missing Simulink libraries

### Requirement 10

**User Story:** As a simulation user, I want validation tests that automatically verify the improvements, so that I can confirm the model works correctly after modifications.

#### Acceptance Criteria

1. WHEN the model is generated THEN the Validation Script SHALL automatically run basic functionality tests
2. WHEN testing feedback loop closure THEN the Test SHALL verify that output voltage tracks reference voltage
3. WHEN testing dynamic load THEN the Test SHALL verify that current decreases over time following the charging profile
4. WHEN testing efficiency THEN the Test SHALL verify that calculated efficiency is within expected range
5. WHEN all tests complete THEN the Test Report SHALL display pass/fail status for each validation check
