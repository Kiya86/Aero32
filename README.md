# Aero32

<img width="3456" height="1884" alt="MainRender1" src="https://github.com/user-attachments/assets/c4da0b33-52e1-4049-8f33-8104e93957bc" />
<img width="3006" height="2002" alt="BoardRender1" src="https://github.com/user-attachments/assets/e170187c-141b-4145-a977-77b0322f71fb" />


<h4 align="center">
A custom STM32N6-based AI vision module!
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
  <a href="#power-architecture">Power System</a> •
  <a href="#bom">BOM</a> 
</p>

## Key Features

- **STM32N657X0H3Q** — Neural-ART accelerator that is used alongside the STM32N6 MCU
- **15-Pin CSI FPC Connector** — Camera sensor interface
- **MT35XU256ABA1G12** — 256 Mbit Octal SPI NOR Flash for either firmware or data 
- **IS66WVO32M8DALL** — 256 Mbit PSRAM for working memory
- **2× UART Ports** — Serial breakout headers
- **2× I2C Ports** — Two-wire serial communication breakout headers
- **1× SPI Port** — High-speed peripheral interface breakout
- **48 MHz & 32.768 kHz Crystals** — System clock and low power RTC
- **XT30 Battery Input** — 3S–4S LiPo input
- **USB-C** — Programming, debugging, and power input with ESD protection
- **5× Status LEDs** — 3 green + 2 red for power and debug feedback
- **Input OR** — TPS2121 power multiplexer for safe dual-source power switching

## Purpose

Aero32 is a small and compact AI vision board designed to serve as a node for drones or other flight hardware. The board offloads computer vision and processing from the external processing, communicating the results over UART, I2C, or SPI.

The STM32N6's Neural Processing Unit (NPU) allows anomaly detection, human recognition, and other advanced recognition directly on the board without AI hardware or wifi.

## PCB

Designed in **KiCad** and manufactured through **JLCPCB** (soon). The board uses a **6-layer PCB stackup** to allow for a reduction of EMI and signal interference. 

### Schematic

<img width="2200" height="1700" alt="Aero32-1" src="https://github.com/user-attachments/assets/e6d21b9e-2f73-4a85-9a8d-d651be0493ee" />

## Main Components

| Category | Component | Description |
|---|---|---|
| Microcontroller | STM32N657X0H3Q | STM32N6 with NPU |
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

## Communication Interfaces

### UART (×2)
Two independent UART breakout ports via 2-pin JST ZH 1.5mm connectors.

### I2C (×2)
Two I2C ports broken out via JST ZH 1.5mm connectors.

### SPI (×1)
One SPI port available for high-speed peripheral communication.

### Camera (CSI)
A 15-pin 1mm pitch FPC connector (Omron XF3M) provides the camera sensor interface.

## Power Architecture

Aero32 supports dual power inputs (USB-C and XT30 battery) with automatic source switching via the TPS2121 power mux.

## BOM

The full Bill of Materials is available in [`Aero32_BOM.csv`](./PCB/Aero32_BOM.csv), formatted for direct JLCPCB assembly upload.

JLCPCB Quote
<img width="3174" height="1922" alt="image" src="https://github.com/user-attachments/assets/1fe0bbe3-fb12-4405-9bad-bdb3e5c00252" />

