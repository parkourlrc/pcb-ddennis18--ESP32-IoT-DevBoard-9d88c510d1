# ESP32-IoT PCB

An ESP32-C3 based IoT controller board designed in KiCad. The board combines
wireless control, sensor interfaces, local storage, audio/light sensing, USB
connectivity, and single-cell Li-ion battery support on a compact four-layer
PCB.

## Main features

- **ESP32-C3-WROOM-02-H4** wireless microcontroller module
- **BME280** environmental sensor
- **MicroSD card** interface
- **W25Q32JV** external SPI flash
- **MAX4466** microphone amplifier and **CMC-5042PF-AC** microphone
- **TEMT6000X01** ambient light sensor
- **USB-C** connector with:
  - CP2102N USB-to-UART bridge
  - USB ESD protection
  - Boot and reset controls
- **Single-cell Li-ion power path**:
  - MCP73871 charger/power-path controller
  - JST battery connector
  - 3.3 V LM1117 regulator
- Status and activity LEDs
- Exposed SPI test points for SCLK, MOSI, MISO, chip select, and SD chip select
- Two M2 mounting holes

## PCB specifications

| Property | Value |
| --- | --- |
| Board thickness | 1.6 mm |
| Layer count | 4 copper layers |
| Copper stack | F.Cu / In1.Cu / In2.Cu / B.Cu |
| Copper thickness | 35 µm per copper layer |
| Core material | FR-4 |
| Approximate outline | 96.5 mm × 54.4 mm |
| Minimum routed trace width | 0.20 mm |
| Minimum routed spacing | 0.15 mm |
| Solder mask | Top and bottom |
| Silkscreen | Top and bottom |
| Finish | Not specified in the KiCad board setup; confirm with the fabricator |

The board outline includes a stepped/notched section around the USB connector
edge. Use the `Edge.Cuts` layer in the KiCad board file, rather than the
approximate dimensions above, for fabrication.

## Repository layout

### Design files

- [`ESP32-IoT.kicad_pcb`](./ESP32-IoT.kicad_pcb) — PCB layout
- [`ESP32-IoT.kicad_sch`](./ESP32-IoT.kicad_sch) — main schematic
- [`esp32-c3-02.kicad_sch`](./esp32-c3-02.kicad_sch) — ESP32-C3 subsystem
- [`sensors.kicad_sch`](./sensors.kicad_sch) — sensor subsystem
- [`user-interface.kicad_sch`](./user-interface.kicad_sch) — user-interface subsystem
- [`ESP32-IoT.kicad_pro`](./ESP32-IoT.kicad_pro) — KiCad project

### Libraries and reference material

- [`Libraries/Footprints/`](./Libraries/Footprints/) — project-specific footprints
- [`Libraries/Symbols/`](./Libraries/Symbols/) — project-specific symbols
- [`Libraries/3D models/`](./Libraries/3D%20models/) — STEP models used by the board
- [`Datasheets/`](./Datasheets/) — component datasheets
- [`fp-lib-table`](./fp-lib-table) and [`sym-lib-table`](./sym-lib-table) — project library configuration

## Opening the design

1. Install KiCad with PCB Editor and Schematic Editor.
2. Clone or download this repository while preserving the directory layout.
3. Open [`ESP32-IoT.kicad_pro`](./ESP32-IoT.kicad_pro).
4. Open the schematic and PCB from the KiCad project manager.
5. Keep the project-local `Libraries` directory beside the project files so the
   paths in `fp-lib-table` and `sym-lib-table` resolve correctly.

The PCB was saved by KiCad 10.0. Older KiCad releases may not be able to open
the board without conversion. Save a copy before converting the project.

## Assembly and bring-up notes

Populate and inspect the power section before fitting the ESP32-C3 module.
Check for shorts between `+3.3V`, USB VBUS, battery input, and `GND`, then
verify the regulator output with a current-limited supply.

For first power-up:

1. Leave the battery disconnected and power the board from USB.
2. Verify the 3.3 V rail and the power/status LED.
3. Confirm that the CP2102N enumerates over USB.
4. Use the **BOOT** and **RESET** switches to enter the ESP32-C3 download
   mode.
5. Program and test the ESP32-C3 firmware before connecting a battery.

Observe the polarity markings for the battery connector and polarized
capacitors. Do not connect a Li-ion cell until the charger and power-path
voltages have been verified.

## Design status

This repository contains the KiCad source and exported fabrication files.
Firmware, a complete assembly BOM, and a documented connector pinout are not
included in the current project snapshot. Validate the latest schematic,
component values, ERC/DRC results, and manufacturer capabilities before
production.

## License

This project is licensed under the [MIT License](./LICENSE).

The MIT license allows reuse, modification, distribution, and commercial use,
provided that the copyright notice and permission notice are retained in all
copies or substantial portions of the project.
