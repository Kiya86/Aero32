# Aero32

<h4 align="center">
A custom STM32N6-based AI vision and sensor board designed for high-power rocketry flight computer integration.
</h4>

<div align="center">

![KiCad](https://img.shields.io/badge/KiCad-314CB0?style=for-the-badge&logo=kicad&logoColor=white)
![STM32N6](https://img.shields.io/badge/STM32N6-03234B?style=for-the-badge&logo=stmicroelectronics&logoColor=white)
![JLCPCB](https://img.shields.io/badge/JLCPCB-C00000?style=for-the-badge&logoColor=white)

</div>

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#purpose">Purpose</a> •
  <a href="#pcb">PCB</a> •
  <a href="#main-components">Main Components</a> •
  <a href="#communication-interfaces">Communication Interfaces</a> •
  <a href="#power-architecture">Power Architecture</a> •
  <a href="#bom">BOM</a> •
  <a href="#license">License</a>
</p>

---

## Key Features

- **STM32N657X0H3Q** — Neural-ART accelerator-equipped STM32N6 MCU in BGA-264, purpose-built for on-device AI inference
- **15-Pin CSI FPC Connector** — Camera sensor interface for image capture and AI vision pipelines
- **MT35XU256ABA1G12** — 256 Mbit Octal SPI NOR Flash for firmware and data storage
- **IS66WVO32M8DALL** — 256 Mbit PSRAM for frame buffer and inference working memory
- **2× UART Ports** — Serial breakout headers for flight computer data exchange
- **2× I2C Ports** — Sensor and peripheral expansion via JST ZH connectors
- **1× SPI Port** — High-speed peripheral interface breakout
- **48 MHz + 32.768 kHz Crystals** — System clock and low-power RTC references
- **Multi-rail Power System** — Dedicated 3.3V, 1.8V, 1V8B, 3V3, +3V3, 0VB33, and auxiliary supply rails
- **XT30 Battery Input** — 2S–3S LiPo input with automotive-grade buck regulation
- **USB-C** — Programming, debugging, and power input with ESD protection
- **Boot & Reset Buttons** — BOOT0 and NRST tactile switches for easy firmware flashing
- **5× Status LEDs** — 3 green + 2 red for power and debug feedback
- **Input OR-ing** — TPS2121 power multiplexer for safe dual-source power switching

---

## Purpose

Aero32 is a compact AI vision and telemetry board designed to serve as an intelligent sensor node for high-power rocketry systems. The board offloads computer vision and sensor inference from the main flight computer, communicating processed results over UART, I2C, or SPI.

The STM32N6's on-chip Neural Processing Unit (NPU) enables real-time image classification, anomaly detection, or apogee event recognition directly on the board — without requiring cloud or off-chip AI hardware.

Aero32 is intended to integrate with an existing flight computer as a co-processor, providing:

- AI-assisted flight event detection via camera
- Sensor fusion output streamed over UART/I2C/SPI
- High-capacity local storage for post-flight image and data review
- A flexible interface layer compatible with most flight computer architectures

> **Note:** This project is independent and not affiliated with any rocketry organization or team.

---

## PCB

Designed in **KiCad** and manufactured through **JLCPCB**. The board uses a **4-layer PCB stackup** to support clean power distribution, solid ground return paths, and low-noise routing for RF-adjacent signal lines.

The layout is divided into functional zones:

- **Power** — Input regulation, rail generation, and decoupling
- **MCU Core** — STM32N6 with supporting clocks, boot/reset, and decoupling
- **Memory** — Octal SPI NOR Flash and PSRAM in proximity to the MCU
- **Camera Interface** — CSI FPC connector with matched-length routing
- **I/O Breakouts** — UART, I2C, SPI, and power header sections
- **Indicators** — LED and debug circuitry

### Schematic

> *(See schematic image in the `/docs` folder or project repository)*

---

## Main Components

| Category | Component | Description |
|---|---|---|
| Microcontroller | STM32N657X0H3Q | STM32N6 with NPU, BGA-264 |
| NOR Flash | MT35XU256ABA1G12-0AUT | 256 Mbit Octal SPI Flash (Micron) |
| PSRAM | IS66WVO32M8DALL-200BLI | 256 Mbit Pseudo-SRAM (ISSI) |
| Camera Connector | XF3M(1)-1515-1B | 15-Pin 1mm Pitch FPC (Omron) |
| Main Buck Regulator | LM61495Q5RPHRQ1 | 3–36V 10A Automotive Buck (TI) |
| Aux Buck (3A) | AP3441LSHE-7B | 2.7–5.5V 3A Adjustable Buck |
| Aux Buck (3A) | TPS62088YFPR | 2.4–5.5V 3A Adjustable Buck (TI) |
| Fixed 3.3V Buck | TPS560430X3FDBVR | 4–36V 600mA 3.3V Fixed Buck (TI) |
| 1.8V LDO (×2) | ETA5055V180DD1E | 1.8V 500mA LDO |
| 3.3V LDO | ETA5055V330DD1E | 3.3V 500mA LDO |
| Power Mux | TPS2121RUXR | ORing Power Multiplexer (TI) |
| USB ESD | TPD2E001DRYR | 2-Channel USB ESD Protection (TI) |
| USB Connector | HC-TYPE-C-16P-01A-G | USB Type-C 16P 3A Female |
| Power Input | XT30PW-M | XT30 Male 15A Connector |
| System Crystal | SX0B48.000F0810F30 | 48 MHz ±10ppm Crystal |
| RTC Crystal | NX2012SA 32.768K | 32.768 kHz ±20ppm Crystal |
| Boot / Reset | K2-1808SN-A4SW | SPST Tactile Switch (×2) |
| Status LEDs | KT-0603G / KT-0603R | Green (×3) / Red (×2) 0603 LEDs |
| TVS Diode | LESD5D5.0CT1G | 150W Bidirectional TVS 5V |

---

## Communication Interfaces

### UART (×2)
Two independent UART breakout ports via 2-pin JST ZH 1.5mm connectors, available for bidirectional serial communication with a flight computer or ground support equipment.

### I2C (×2)
Two I2C ports broken out via JST ZH 1.5mm connectors for connecting external sensors, IMUs, or peripherals. Pull-up resistors included on-board.

### SPI (×1)
One SPI port available for high-speed peripheral communication, suitable for external sensors, displays, or additional flash/memory modules.

### Camera (CSI)
A 15-pin 1mm pitch FPC connector (Omron XF3M) provides the camera sensor interface, routed to the STM32N6's DCMI/CSI peripheral.

---

## Power Architecture

Aero32 supports dual power inputs (USB-C and XT30 battery) with automatic source switching via the TPS2121 power mux.

| Rail | Regulator | Purpose |
|---|---|---|
| VBAT / VIN | XT30 Input | 2S–3S LiPo battery input |
| VDCCORE | LM61495 (Buck) | Main core supply from battery |
| +3V3 | TPS560430 (Buck) | 3.3V fixed rail |
| 0VB33 | AP3441 (Buck) | Adjustable 3.3V auxiliary |
| VCC / +3V3 | TPS62088 (Buck) | Auxiliary 3.3V regulated rail |
| 1V8 | ETA5055 (LDO) | 1.8V rail (MCU I/O) |
| 1V8B | ETA5055 (LDO) | 1.8V secondary rail |
| 3.3V | ETA5055 (LDO) | Filtered 3.3V LDO output |
| VBUS | USB-C Input | 5V USB bus power |

Extensive decoupling is applied across all rails using a combination of 100nF, 1µF, 10µF, 22µF, and 47µF MLCCs placed at each supply pin.

---

## BOM

The full Bill of Materials is available in [`Aero32_BOM.csv`](./PCB/Aero32_BOM.csv), formatted for direct JLCPCB assembly upload.

Summary:

| Category | Count |
|---|---|
| MLCCs (Capacitors) | ~95 |
| Resistors | ~35 |
| Power Inductors | 4 |
| ICs & Regulators | 12 |
| Connectors | 10 |
| LEDs | 5 |
| Crystals | 2 |
| Switches | 2 |
| Diodes | 2 |

---

## License

GNU Affero General Public License v3.0
