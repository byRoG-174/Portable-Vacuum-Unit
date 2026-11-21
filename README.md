# Portable Vacuum Unit (Nidec + 3S + PQ30RV21)

**Status:** Prototype (Work in Progress / Alpha)  
**Goal:** Autonomous power supply for a vacuum pump from a Li-Ion battery with speed control.

## About the project

A prototype assembly combining a Nidec 12V 0.6A pump with a 3S Li-Ion power bank using an LDO **PQ30RV21** as a clean, reliable voltage stabilizer. 

## Hardware & Schematic

* **Pump:** Nidec 12V 0.6A (BLDC, 4-wire) with Tacho monitoring and voltage speed control (`Vadj`).
* **Power:** 3S Li-Ion (3x18650) + 20A BMS.
* **Regulation & Cooling:** Sharp PQ30RV21 paired with a custom aluminum heatsink (>80 sq.cm) and thermal paste.

<p align="center">
  <img src="schematic/demo.gif" width="600" alt="Portable Vacuum Unit Prototype">
</p>

1. **Battery (+/-)** → Connect to `VIN` and common `GND` of PQ30RV21.
2. **Output Stage:** `VOUT` → Power diode (`1N5819`) → `470uF` Capacitor → Nidec Pump (+).
3. **Control & Tacho:** Voltage divider on `VADJ` (`5.6V – 11.5V` range) and Nidec yellow wire via `10k` pull-up to `VOUT` (`5V`) for the MCU.

## Known Issues & Quick Start

* **Thermal/Efficiency:** The LDO heats up under load and drains the 3S battery quickly; heatsink monitoring is mandatory.
* **Operation:** Connect the battery, adjust the potentiometer (starts reliably above ~6.5V), and keep an eye on temperature.

## TODO (Version 2.0)

- [ ] Replace PQ30RV21 with a DC-DC Buck converter for higher efficiency.
- [ ] Design a proper enclosure.
- [ ] Add a battery charge indicator.

---

**Disclaimer:** Use at your own risk. No hardware overheat protection included.
