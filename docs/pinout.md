# BMS Connector Pinouts

This document describes the external connector pinouts for the Chibi-ECEN-BMS. Refer to the [schematic](../hardware/bms-v01/bms_v01_schematic.pdf) for complete signal details.

## Main Battery Connector

**Connector Type**: Screw terminal or wire-to-board

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | BATT- | Battery negative (cell 1 negative) |
| 2 | CELL1+ | Cell 1 positive / Cell 2 negative |
| 3 | CELL2+ | Cell 2 positive / Cell 3 negative |
| 4 | CELL3+ | Cell 3 positive / Cell 4 negative |
| 5 | CELL4+ | Cell 4 positive / Cell 5 negative |
| 6 | CELL5+ | Cell 5 positive / Cell 6 negative |
| 7 | CELL6+ | Cell 6 positive / Cell 7 negative |
| 8 | BATT+ | Battery positive (cell 7 positive) |

**Voltage Levels**: 19.6V - 29.4V (total pack voltage)

**Notes**:
- Each cell voltage is measured differentially by the LT6803
- RC filtering on each cell input for noise immunity
- Do not reverse polarity - no reverse polarity protection

## Charge Connector

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | CHRG+ | Charger positive output |
| 2 | CHRG- | Charger negative (return to pack negative) |
| 3 | CHRG_SENSE | Charge current sense (optional) |
| 4 | CHRG_EN | Charge enable signal (output from BMS) |

**Voltage Levels**:
- CHRG+/CHRG-: 19.6V - 29.4V (matches pack voltage)
- CHRG_EN: 3.3V logic level (active high)
- CHRG_SENSE: 0-3.3V analog

**Notes**:
- CHRG_EN controls external charge FET or relay
- CHRG_SENSE is optional current measurement input
- Charge path must include external FET/relay controlled by CHRG_EN

## Load Connector

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | LOAD+ | Load positive output |
| 2 | LOAD- | Load negative (return to pack negative) |
| 3 | LOAD_SENSE | Load current sense (optional) |
| 4 | LOAD_EN | Load enable signal (output from BMS) |

**Voltage Levels**:
- LOAD+/LOAD-: 19.6V - 29.4V (matches pack voltage)
- LOAD_EN: 3.3V logic level (active high)
- LOAD_SENSE: 0-3.3V analog

**Notes**:
- LOAD_EN controls external discharge FET or relay
- LOAD_SENSE is optional current measurement input
- Load path must include external FET/relay controlled by LOAD_EN

## CAN Bus Connector

**Connector Type**: Screw terminal or pin header

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | CAN_H | CAN High |
| 2 | CAN_L | CAN Low |
| 3 | CAN_GND | CAN Ground (isolated) |
| 4 | CAN_PWR | CAN Power (5V, optional) |

**Voltage Levels**:
- CAN_H/CAN_L: CAN 2.0B differential signaling (recessive ~2.5V, dominant 3.5V/1.5V)
- CAN_PWR: 5V output, max 100mA

**Notes**:
- CAN transceiver is isolated (ADM3054)
- 120Ω termination resistor can be enabled via jumper or software
- Follow CAN bus wiring guidelines (twisted pair, proper termination)
- Maximum cable length depends on bit rate (40m @ 1Mbps, 1000m @ 50kbps)

## USB Connector

**Connector Type**: Micro-B USB receptacle

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | VBUS | USB 5V power input |
| 2 | D- | USB Data negative |
| 3 | D+ | USB Data positive |
| 4 | ID | USB ID (not connected) |
| 5 | GND | USB Ground |

**Notes**:
- USB 2.0 Full Speed (12 Mbps)
- Appears as virtual COM port (CDC class)
- Can be powered from USB or battery (diode-OR)
- USB shield connected to GND through ferrite bead

## JTAG/SWD Debug Connector

**Connector Type**: 2x5 pin 0.05" (1.27mm) pitch header (ARM Cortex standard)

| Pin | Signal | Direction | Description |
|-----|--------|-----------|-------------|
| 1 | VTREF | Input | Target reference voltage (3.3V) |
| 2 | SWDIO/TMS | I/O | Serial Wire Debug I/O / JTAG TMS |
| 3 | GND | - | Ground |
| 4 | SWCLK/TCK | Input | Serial Wire Clock / JTAG Clock |
| 5 | GND | - | Ground |
| 6 | SWO/TDO | Output | Serial Wire Output / JTAG Data Out |
| 7 | KEY | - | Key (no pin) |
| 8 | TDI | Input | JTAG Data In (SWD mode: not used) |
| 9 | GND | - | Ground |
| 10 | NRST | I/O | Reset (active low, open-drain) |

**Notes**:
- Compatible with ST-Link, J-Link, and other ARM debuggers
- SWD mode is preferred (only requires SWDIO, SWCLK, GND, VTREF, NRST)
- JTAG mode uses all signals for full debug capability
- Pull-up resistors on SWDIO, SWCLK, NRST

## User Interface

### Status LED

**Type**: Common-cathode RGB LED

| Pin | Signal | Description |
|-----|--------|-------------|
| 1 | LED_R | Red channel (active high, current-limited) |
| 2 | LED_G | Green channel (active high, current-limited) |
| 3 | LED_B | Blue channel (active high, current-limited) |
| 4 | GND | Common cathode |

**Color Codes** (typical firmware implementation):
- **Green**: Normal operation
- **Blue**: Charging
- **Red**: Fault condition
- **Yellow** (Red+Green): Warning
- **Cyan** (Blue+Green): Discharging
- **Magenta** (Red+Blue): Initialization/bootloader
- **White** (all on): Test mode
- **Off**: Sleep/standby

### Buttons

| Button | Pin | Function |
|--------|-----|----------|
| BUTTON1 | PB10 | User button 1 (pulled high, active low) |
| BUTTON2 | PB11 | User button 2 (pulled high, active low) |

**Notes**:
- Debounced in firmware
- Can be used for manual fault reset, mode selection, etc.
- Exact function depends on firmware implementation

## STM32 Pin Assignments

### SPI1 - LT6803 Battery Monitor
| STM32 Pin | Signal | Function |
|-----------|--------|----------|
| PA5 | SPI1_SCK | Serial clock |
| PA6 | SPI1_MISO | Master in, slave out |
| PA7 | SPI1_MOSI | Master out, slave in |
| PA4 | SPI1_CS | Chip select (GPIO) |

### SPI2 - microSD Card
| STM32 Pin | Signal | Function |
|-----------|--------|----------|
| PB13 | SPI2_SCK | Serial clock |
| PB14 | SPI2_MISO | Master in, slave out |
| PB15 | SPI2_MOSI | Master out, slave in |
| PB12 | SPI2_CS | Chip select (GPIO) |

### CAN Bus
| STM32 Pin | Signal | Function |
|-----------|--------|----------|
| PA11 | CAN_RX | CAN receive |
| PA12 | CAN_TX | CAN transmit |

### USB
| STM32 Pin | Signal | Function |
|-----------|--------|----------|
| PA11 | USB_DM | USB D- (shared with CAN_RX) |
| PA12 | USB_DP | USB D+ (shared with CAN_TX) |

**Note**: PA11/PA12 are shared between CAN and USB. System design should ensure only one is active at a time, or use external multiplexing.

### ADC Inputs
| STM32 Pin | Signal | Function |
|-----------|--------|----------|
| PA0 | BATT_CURRENT | Battery current sense |
| PA1 | CHRG_CURRENT | Charge current sense |
| PA2 | CHRG_SENSE | Charge voltage sense |
| PA3 | LOAD_SENSE | Load voltage sense |
| Internal | PCB_TEMP | On-chip temperature sensor |
| Internal | VREFINT | Internal voltage reference |

### Digital I/O
| STM32 Pin | Signal | Direction | Function |
|-----------|--------|-----------|----------|
| PB0 | CHRG_EN | Output | Charge enable (active high) |
| PB1 | LOAD_EN | Output | Load enable (active high) |
| PB2 | CHRG_FLT | Input | Charge fault input (optional) |
| PB3 | LOAD_FLT | Input | Load fault input (optional) |
| PB4 | CAN_SHDN | Output | CAN shutdown control |
| PB5 | 5V_SHDN | Output | 5V power shutdown |
| PB6 | AUX_EN | Output | Auxiliary power enable |
| PB8 | CD | Input | microSD card detect |
| PB10 | BUTTON1 | Input | User button 1 |
| PB11 | BUTTON2 | Input | User button 2 |

### Oscillators
| STM32 Pin | Signal | Function |
|-----------|--------|----------|
| PF0 | OSC_IN | 8MHz external crystal input |
| PF1 | OSC_OUT | 8MHz external crystal output |
| PC14 | OSC32_IN | 32.768kHz RTC crystal input |
| PC15 | OSC32_OUT | 32.768kHz RTC crystal output |

## Power Pins Summary

| Pin | Net | Description |
|-----|-----|-------------|
| VDD (multiple) | +3V3 | 3.3V main power |
| VSS (multiple) | GND | Ground |
| VDDA | VDDA | 3.3V analog power |
| VSSA | GND | Analog ground |
| VBAT | RTC_VBAT | RTC backup battery (optional) |
| VREF+ | VDDA | ADC positive reference |
| VREF- | GND | ADC negative reference |

---

For complete pin assignments and electrical characteristics, refer to the [STM32F303 datasheet](../datasheets/STM32F303-microcontroller.pdf) and the [schematic](../hardware/bms-v01/bms_v01_schematic.pdf).

For signals CSV data, see [../analysis/requirements/bms_signals.ods](../analysis/requirements/) (if available).
