# Portable Vacuum Unit

Battery-powered vacuum pump on a Nidec 12V BLDC motor: manual speed control,
3S Li-Ion pack, compact DIY build.

**Status:** Status: v0.1 — assembled, verified, video attached. Next: v2 (INA3221 + ESP32).

## Demo

https://github.com/user-attachments/assets/faaa4c4b-80e8-4265-8f0d-c4ae3ed239fa

## What it is

A self-contained unit that runs a Nidec 12V 0.6A BLDC vacuum pump from a
3S Li-Ion battery (3×18650, 20A BMS). Pump speed is set with a potentiometer;
the tacho output lets you verify the pump is spinning. v1 uses a Sharp
PQ30RV21 LDO as the regulator — simple, but inefficient (see Known Issues).
v2 will switch to a buck converter.

## Quick start

1. Connect the 3S battery to `VIN` / `GND`.
2. Turn the potentiometer up: the pump starts reliably above ~6.5V on `VADJ`.
3. Keep an eye on the heatsink — there is no thermal protection on board.

## Wiring

1. Battery (+/−) → `VIN` and common `GND` of the PQ30RV21.
2. `VOUT` → 1N5822 diode → 470 µF capacitor → pump (+).
3. Voltage divider on `VADJ` sets the 5.6–11.5V range
   (R1 = <!-- значение -->, R2 = <!-- значение -->).
4. Pump tacho (yellow wire) → 10k pull-up → controller / measurement input.

## Measured performance

<!-- заполни замерами, пока пусто — так честнее, чем выдуманные цифры: -->
- Max vacuum: <!-- kPa -->
- Runtime on a full charge: <!-- min -->
- Heatsink temperature under load: <!-- °C -->

Полная версия BOM и проект KiCad — в репозитории:
- [KiCad project](schematic/) — schematic and PCB files
- [BOM (CSV)](schematic/Portable_Vacuum_Unit.csv)
- [Datasheets](datascheet/) — pump and regulator PDFs

## Known issues (v1)

- The LDO burns the surplus voltage as heat: the pack drains fast and the
  heatsink gets hot. Monitoring is mandatory.
- No thermal protection, no low-battery cutoff.

## Roadmap (v2)

- [ ] Replace the LDO with a buck converter (efficiency).
- [ ] Enclosure (3D-printed).
- [ ] Battery gauge.

## License

Distributed under the MIT. See `LICENSE` for details.
