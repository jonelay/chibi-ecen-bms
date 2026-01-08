# Hardware Files

This directory contains manufacturing-ready files for the Chibi-ECEN-BMS hardware versions.

## Contents

### [bms-v01/](bms-v01/) - Version 1 (Manufactured & Tested)
Complete manufacturing files for Version 1, which was designed in February 2015, manufactured in March 2015, and successfully tested.

**Status**: ✓ Manufactured, ✓ Assembled, ✓ Tested

**Files**:
- `bms_v01_schematic.pdf` - 3-page schematic (battery monitoring, microcontroller, interfaces)
- `bms_v01_layout.pdf` - PCB layout (4-layer board, ~100mm x 75mm)
- `bms_v01_assembly_bom.csv` - Bill of materials with part numbers
- `gerbers/` - Complete gerber files for PCB manufacturing

**Manufacturing Specifications**:
- 4-layer PCB
- Dimensions: ~100mm x 75mm
- Thickness: 1.6mm
- Min trace/space: 6/6 mil
- Min drill: 0.3mm
- Finish: HASL or ENIG
- Solder mask: Green
- Silkscreen: White

## Manufacturing Information

### Hand Assembly

The v0.1 prototype boards were hand-assembled to save on cost and schedule.

**Assembly Considerations**:
- LT6803 is QFN package - requires good soldering skills or reflow oven
- STM32F303 is LQFP48 - manageable with fine-tip iron
- Most passives are 0603 size - tweezers and magnification helpful
- Stencil recommended for solder paste application

**Tools Needed**:
- Soldering iron with fine tip (Hakko FX-888D or similar)
- Hot air station (for QFN packages) or reflow oven
- Tweezers, flux, solder paste
- Multimeter for testing
- Oscilloscope for verification (recommended)

## Testing

After assembly, follow the test procedure in [../testing/test-procedure.pdf](../testing/test-procedure.pdf).

**Basic Tests**:
1. Visual inspection - Check for shorts, proper component placement
2. Power-on test - Verify 3.3V and 5V rails before connecting battery
3. Microcontroller test - Program and verify LED blink
4. LT6803 test - Verify cell voltage readings
5. CAN bus test - Verify communication with test device
6. microSD test - Verify file read/write

**Safety Warning**:
- Do not connect battery until power rails are verified correct
- Use current-limited power supply for initial testing
- Start with low voltage (e.g., 3S pack) before full 7S pack
- Monitor for smoke, heating, or unusual behavior

## Design Files

Native Eagle CAD design files are located in [../design-source/eagle/](../design-source/eagle/).

**Files**:
- `bms_v01.sch`, `bms_v01.brd` - Version 1 Eagle files
- `bms_v02.sch`, `bms_v02.brd` - Version 2 Eagle files

**Eagle Version**: Designed with Eagle 6.x or 7.x

## License

Hardware design files are released under the MIT License. See [../LICENSE](../LICENSE) for details.

---

**Disclaimer**: This is a student project from 2015. While care was taken in design and the hardware was successfully tested, use at your own risk. Battery management systems require careful design for safety.
