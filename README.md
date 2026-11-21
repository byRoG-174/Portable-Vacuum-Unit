# # Portable Vacuum Unit (Nidec + 3S + PQ30RV21)

**Status:** Prototype (Work in Progress / Alpha).
**Goal:** Autonomous power supply for a vacuum pump from a Li-Ion battery with speed control.

## About the project
A "whatever was on the desk" assembly to get off the wall socket. 
The task was simple: take a Nidec 12V 0.6A pump, a 3S Li-Ion bank, and make it run autonomously.

As the brain and stabilizer, an old but reliable LDO `PQ30RV21` is used. Yes, it gets hot. Yes, a linear regulator on a battery is not the most efficient way to drain power. But it provides clean power without ripple, is cheap, and forgives assembly mistakes. This is a prototype, and it is supposed to look ugly.

## Hardware
*   **Pump:** Nidec 12V 0.6A (BLDC, 4-wire). Yellow wire (Tacho) is routed to an oscilloscope/MCU for monitoring, speed control is by voltage (Vadj).
*   **Power:** 3S Li-Ion (3x18650) + 20A BMS.
*   **Regulation:** Sharp PQ30RV21. 
*   **Heatsink:** The first piece of aluminum found (area "by eye" >80 sq.cm). Pressed with thermal paste. Without it, the chip burns out in 2 minutes under load.

## Schematic (Concept)
(Your current hand-drawn or messy schematic picture should be here).

**Quick connection guide:**
1.  **Battery (+)** -> `VIN` of PQ30RV21.
2.  **Battery (-)** -> Common `GND`.
3.  **Output `VOUT`** -> Power diode (1N5819, stripe to output!) -> 470uF Cap -> Nidec Pump (+).
4.  **Adjustment:** Divider on `VADJ` (1k to ground, 3.5k + 4.7k pot to output). Range 5.6V – 11.5V.
5.  **Tachometer:** Yellow wire Nidec via 10k pull-up to `VOUT` (5V) -> MCU pin.

## Known Issues
*   **Heating up:** PQ30RV21 becomes a furnace at low battery charge and high RPM. This is normal for an LDO. If you can hold the heatsink — it works.
*   **Consumption:** Autonomy is limited by linear regulator efficiency. Drains the 3S battery faster than desired.
*   **Aesthetics:** Wires are hanging, soldering is messy, heatsink is held by electrical tape. This is a feature, not a bug.

## Quick Start
1.  Connect the 3S battery to the input.
2.  Turn the potentiometer smoothly.
3.  At minimum (5.63V) the pump might just hum and not start. Add to 6.5V — it should kick in.
4.  Watch the heatsink. If it smells like burning — you forgot thermal paste or the heatsink is too small.

## TODO (Version 2.0, if it survives)
*   [ ] Throw out PQ30RV21, put a DC-DC Buck (Efficiency from 50% to 90%).
*   [ ] Proper case, not a cardboard box.
*   [ ] Battery charge indicator.

---
**License:** Use at your own risk. The circuit works, but there is no overheat protection in the MCU yet. Do not leave unattended at max RPM.