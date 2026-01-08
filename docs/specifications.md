# BMS Specifications

## System Requirements

### Battery Configuration
- **Cell Count**: 7 cells in series (7S)
- **Cell Type**: 18650 Lithium-Ion
- **Reference Cell**: Samsung ICR18650-30B
- **Cell Capacity**: 3000mAh nominal
- **Cell Voltage Range**: 2.8V - 4.2V per cell
- **Pack Voltage Range**: 19.6V - 29.4V
- **Nominal Pack Voltage**: ~25.9V (3.7V/cell)

### Electrical Specifications

#### Power
- **Operating Voltage**: 19.6V - 29.4V (from battery pack)
- **Auxiliary Power Output**: 3.3V, 5V regulated
- **Quiescent Current**: < 50mA (typical)
- **Standby Current**: < 5mA (sleep mode, if implemented)

#### Current Monitoring
- **Charge Current**: 0 - 7A (target application)
- **Discharge Current**: 0 - 20A (target application)
- **Current Sense Resolution**: 10-bit ADC minimum

#### Voltage Monitoring
- **Cell Voltage Accuracy**: ±5mV (LT6803 specification)
- **Measurement Resolution**: 12-bit (LT6803)
- **Sampling Rate**: Configurable, up to 10Hz for logging

#### Temperature Monitoring
- **On-board Temperature Sensor**: STM32 internal sensor
- **External Temperature Inputs**: Provision for thermistor inputs
- **Temperature Range**: 0°C - 45°C (operating)
- **Storage Temperature**: -20°C - 70°C

### Communication Interfaces

#### CAN Bus
- **Standard**: CAN 2.0B
- **Bit Rate**: Configurable, typically 250kbps or 500kbps
- **Transceiver**: ADM3054 (isolated)
- **Connector**: Screw terminal or pin header
- **Termination**: Software-selectable termination resistor

#### USB
- **Standard**: USB 2.0 Full Speed
- **Connector**: Micro-B USB
- **Purpose**: Debugging, configuration, data download
- **Protocol**: USB CDC (virtual COM port)

#### Debug Interface
- **Standard**: JTAG/SWD
- **Connector**: 2x5 pin 0.05" header (ARM Cortex standard)
- **Supported Tools**: ST-Link, J-Link, OpenOCD-compatible

### Data Logging
- **Storage**: microSD card (SPI interface)
- **Card Support**: SD and SDHC cards
- **File System**: FAT32
- **Logging Rate**: Configurable, 1Hz - 10Hz typical
- **Data Recorded**:
  - Cell voltages (7 channels)
  - Pack current (charge/discharge)
  - Temperature
  - Timestamp
  - Fault conditions

### Safety & Protection

#### Overvoltage Protection
- **Cell Level**: 4.25V per cell (typical threshold)
- **Action**: Disable charging, set fault flag

#### Undervoltage Protection
- **Cell Level**: 2.7V per cell (typical threshold)
- **Action**: Disable discharging, set fault flag

#### Overcurrent Protection
- **Charge Overcurrent**: Configurable threshold
- **Discharge Overcurrent**: Configurable threshold
- **Action**: Disable respective path, set fault flag

#### Over-temperature Protection
- **High Temperature**: 50°C (configurable)
- **Action**: Disable charging/discharging, set fault flag

#### Cell Imbalance Detection
- **Threshold**: Configurable (e.g., 100mV between highest and lowest)
- **Action**: Warning flag, optional balancing (not implemented in v01)

### Mechanical Specifications

#### PCB
- **Size**: Approximately 100mm x 75mm
- **Layers**: 4-layer stackup
- **Thickness**: 1.6mm (standard)
- **Finish**: HASL or ENIG
- **Solder Mask**: Green (standard)
- **Silkscreen**: White

#### Connectors
- **Battery Input**: Screw terminals or wire-to-board connector
- **Charge/Load Outputs**: Screw terminals
- **CAN Bus**: Screw terminal or pin header
- **USB**: Micro-B receptacle
- **JTAG**: 2x5 pin 0.05" header

#### Mounting
- **Mounting Holes**: 4x M3 holes
- **Enclosure**: Designed for Pelican iM2100 case integration

### Environmental Specifications
- **Operating Temperature**: 0°C - 45°C
- **Storage Temperature**: -20°C - 70°C
- **Humidity**: 20% - 80% RH, non-condensing
- **Altitude**: 0 - 2000m (designed for Boulder, CO at ~1655m)

### Firmware Requirements
- **Platform**: STM32F303CBT6
- **Development**: STM32CubeMX, GCC ARM toolchain
- **Real-time OS**: Optional (bare-metal or FreeRTOS)
- **Update Method**: JTAG/SWD or USB bootloader

### Compliance & Standards
**Note**: This is a student project and was not formally certified for compliance.

#### Design References
- **Battery Safety**: Based on UL 2271 principles (not certified)
- **CAN Bus**: CAN 2.0B specification
- **USB**: USB 2.0 specification
- **PCB Design**: IPC-2221 general principles

## Performance Requirements

### Accuracy
- **Voltage Measurement**: ±0.25% (LT6803)
- **Current Measurement**: ±2% (sensor dependent)
- **Temperature Measurement**: ±2°C

### Response Time
- **Fault Detection**: < 100ms
- **Fault Response**: < 10ms (disable output)
- **Data Logging**: 1Hz - 10Hz configurable

### Reliability
- **Target MTBF**: Not formally calculated (student project)
- **Design Life**: 5+ years (component selection basis)
- **Cycle Life**: Follows battery cell specifications

## System Interfaces

### Input Interfaces
1. **Battery Pack** - 7S lithium-ion pack
2. **Charge Input** - Battery charger connection
3. **CAN Bus** - Vehicle network communication
4. **USB** - Configuration and data interface
5. **JTAG/SWD** - Programming and debugging

### Output Interfaces
1. **Load Output** - To motor controller or load
2. **CAN Bus** - Vehicle network communication
3. **Status LED** - RGB LED for user feedback
4. **Fault Signals** - Digital outputs for charge/load enable

## Future Enhancements
*(Not implemented in v01, considerations for v02+)*

- Active cell balancing
- Wireless communication (Bluetooth/WiFi)
- Enhanced diagnostics and state-of-health estimation
- Improved thermal management with active cooling
- CAN-based bootloader for remote firmware updates

---

For detailed requirements traceability, see [../analysis/requirements/requirements.csv](../analysis/requirements/requirements.csv).
