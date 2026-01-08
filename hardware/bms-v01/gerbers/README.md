# Gerber Files - BMS v01

This directory contains the complete set of Gerber files for manufacturing the Chibi-ECEN-BMS Version 1 PCB.

## File List

### Copper Layers
- `bms_v01.L1` - Top copper layer (signal + power)
- `bms_v01.L2` - Inner layer 1 (ground plane)
- `bms_v01.L3` - Inner layer 2 (power plane)
- `bms_v01.L4` - Bottom copper layer (signal + power)

### Solder Mask
- `bms_v01.smb` - Bottom solder mask
- `bms_v01.smt` - Top solder mask

### Silkscreen
- `bms_v01.slk` - Silkscreen (component designators, outlines)

### Solder Paste (for stencil)
- `bms_v01.bps` - Bottom paste (if needed)
- `bms_v01.tps` - Top paste (for SMD assembly)

### Drill Files
- `bms_v01.drl` - NC Drill file (Excellon format)
- `bms_v01.drd` - Drill drawing (documentation)
- `bms_v01.dri` - Drill rack information

### Mechanical
- `bms_v01.oln` - Board outline
- `bms_v01.gpi` - Gerber info file

### Additional Files
- `4LPlus-Sunstone.cam` - CAM job definition for 4-layer boards
- `excellon.cam` - Excellon drill file CAM definition

## PCB Specifications

### Board Parameters
- **Layers**: 4 (2 signal, 2 plane)
- **Dimensions**: ~100mm x 75mm (refer to outline layer)
- **Thickness**: 1.6mm (standard)
- **Material**: FR-4
- **Copper Weight**: 1 oz (35µm) on all layers

### Manufacturing Tolerances
- **Min Trace Width**: 6 mil (0.15mm)
- **Min Trace Spacing**: 6 mil (0.15mm)
- **Min Drill Size**: 0.3mm (12 mil)
- **Min Annular Ring**: 4 mil (0.1mm)

### Finish Options
- **HASL** (Hot Air Solder Leveling) - Standard, low cost
- **ENIG** (Electroless Nickel Immersion Gold) - Preferred for fine-pitch components, flat surface

### Solder Mask
- **Color**: Green (standard) or your choice
- **Type**: LPI (Liquid Photo-Imageable)
- **Clearance**: Standard (typically 3 mil from copper)

### Silkscreen
- **Color**: White (standard)
- **Placement**: Top side only
- **Min Text Size**: 40 mil (1mm) recommended for readability

## Layer Stack-up

```
┌─────────────────────┐
│ Top Solder Mask     │
├─────────────────────┤
│ L1 - Top Copper     │ ← Signal traces, SMD pads
│   (1 oz / 35µm)     │
├─────────────────────┤
│ Prepreg             │
├─────────────────────┤
│ L2 - Ground Plane   │ ← Solid ground plane
│   (1 oz / 35µm)     │
├─────────────────────┤
│ Core                │
├─────────────────────┤
│ L3 - Power Plane    │ ← +3.3V, +5V, Battery+ planes
│   (1 oz / 35µm)     │
├─────────────────────┤
│ Prepreg             │
├─────────────────────┤
│ L4 - Bottom Copper  │ ← Signal traces, SMD pads
│   (1 oz / 35µm)     │
├─────────────────────┤
│ Bottom Solder Mask  │
└─────────────────────┘

Total thickness: 1.6mm
```
