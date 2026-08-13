| Title | Author | Description | Created_at |
|--------|--------|-------------|------------|
| Aero32 | Kiya | AI Camera Module! | 2026-07-24 |

# Dev Log "Aero32"

**Total Time (Hours): 352 Hours**

## Week 1 (05/18/2026) - 42 Hours

Days worked on:

Monday – 8 hours<br>
Tuesday – 8 hours<br>
Wednesday – 9 hours<br>
Thursday – 8 hours<br>
Friday – 9 hours<br>

- Started to research all types of mcu's and comapred each to se which is best (STM32N6, ESP32 P4 and others)
- Read through data sheets and decided to choose the STM32N6 (STM32N6) looked way better than others
- Found out the same day that it has an NPU, which is just AWESOME
- Started to get other components and did more research (REALLY hard to find memory chips (WAY to hard))
- Started to work on the power section (Input OR and MUX)
- Planned out what ouputs I wanted to add (UART, SPI, etc.)
- Created a KiCad project and started to add all the components ONE BY ONE (I am genuinely so mad this took so long)
- Broke up the schematic into different chunks to make life easier (Also found out STM32N6 has multiple symbols)
- Estimated overall board dimensions so the module could easily fit inside a bunch of stuff (universal)

  <img width="585" height="822" alt="image" src="https://github.com/user-attachments/assets/e5f6cff9-0788-4146-8653-c50b9ab8298b" />
  <img width="781" height="713" alt="image" src="https://github.com/user-attachments/assets/b240c2c4-2bae-461c-b4b3-19221b958153" />
  <img width="601" height="780" alt="image" src="https://github.com/user-attachments/assets/10907d8d-f5dd-4cf5-a712-96612e2c8618" />

## Week 2 (06/01/2026) - 48 Hours

Days worked on:

Monday – 10 hours<br>
Tuesday – 9 hours<br>
Wednesday – 9 hours<br>
Thursday – 10 hours<br>
Friday – 10 hours<br>

- Started to complete different parts of the schematic
- Added all power rails and started on decouping caps (So many of them)
- Added all of the crystals
- Decided to swap out two of my voltage rails for more efficient ones (Also smaller)
- Started to research power on sequence that the STM32N6 needs
- Added USB-C programming circuitry and ESD protection
- Selected the TPS2121 power multiplexer for automatic USB-C and battery switching
- Added the camera FPC connector 
- Spent several hours checking datasheets to verify recommended layouts (Also double checked all connections for shorts!)
- Organized schematic sections

  <img width="2032" height="1104" alt="image" src="https://github.com/user-attachments/assets/6fd01fc5-975f-4b04-897e-513691e4af5d" />
  <img width="1454" height="902" alt="image" src="https://github.com/user-attachments/assets/e0e20947-0885-4a53-9ceb-408be9da8b0b" />


## Week 3 (06/08/2026) - 45 Hours

Days worked on:

Monday – 9 hours<br>
Tuesday – 9 hours<br>
Wednesday – 9 hours<br>
Thursday – 9 hours<br>
Friday – 9 hours<br>

- Finished with 90% of the schematic
- Added PSRAM and Octo SPI connections (For memory and RAM)
- Added UART, SPI, and I2C breakouts
- Finished up with the correct STM32N6 power up sequence
- Added LEDS for multiple rails and multi use
- Fixed all of footprint mismatches
- Ran ERC multiple times
- Fixed warnings and errors

  <img width="1750" height="832" alt="image" src="https://github.com/user-attachments/assets/72ed722f-f25b-4ee0-b640-8c2f2fb5cdda" />
  <img width="1246" height="1778" alt="image" src="https://github.com/user-attachments/assets/629d8903-bbae-4ae5-aa54-4953bb038573" />



## Week 4 (06/15/2026) - 44 Hours

Days worked on:

Monday – 9 hours<br>
Tuesday – 8 hours<br>
Wednesday – 9 hours<br>
Thursday – 9 hours<br>
Friday – 9 hours<br>

- Started the layout
- Decided on a the 6 layer board
- Started to decide the location of each of the ic's
- Positioned memory devices close to the MCU (THIS TOOK SO LONG. I HAD TO PLAY AROUND WITH IT AND THEN TUNE ALL OF THE TRACES...TUNE)
- Optimized placement of buck converters and LDOs
- Began routing high-speed signals (Pain, like never again. Memory and RAM chips should not exist)
- Started to stitch all of the layers (Ground planes)

  <img width="2264" height="1300" alt="image" src="https://github.com/user-attachments/assets/94b3c50c-323f-4dc6-9d77-c6a77e55b718" />
  <img width="2230" height="1706" alt="image" src="https://github.com/user-attachments/assets/ddce6070-4ebc-4ee4-9d00-b088c49c8314" />



## Week 5 (06/22/2026) - 43 Hours

Days worked on:

Monday – 9 hours<br>
Tuesday – 8 hours<br>
Wednesday – 8 hours<br>
Thursday – 9 hours<br>
Friday – 9 hours<br>

- Routed the USB differential pair
- Routed camera interface traces (Tuned trace lengths once again)
- Added more stitching vias
- Improved grounding around regulators
- Added silkscreen stuff and my own touch
- Checked clearances

<img width="1766" height="1488" alt="image" src="https://github.com/user-attachments/assets/9a17d0ed-2681-42f5-a4b5-a439c66f30e6" />
<img width="2244" height="1716" alt="image" src="https://github.com/user-attachments/assets/bd41abc6-bda0-4dbd-8f2c-10874367a36c" />


## Week 6 (06/29/2026) - 44 Hours

Days worked on:

Monday – 9 hours<br>
Tuesday – 9 hours<br>
Wednesday – 8 hours<br>
Thursday – 9 hours<br>
Friday – 9 hours<br>

- Finished remaining routing (UART, I2C, SPI breakouts | Boot and Reset Buttons)
- Finalized all of the layers and planes 
- Made sure trace width could handle LiPo input (3s-4s MAX)
- Fixed all of the DRC violations (Traces were too small)
- Added the mounting holes
- Generated several 3D renders 
- Cleaned up silkscreen (Removed extra wording)

  <img width="2260" height="1730" alt="image" src="https://github.com/user-attachments/assets/6de18154-8430-410d-81e0-889f12d17f23" />
  <img width="1320" height="984" alt="image" src="https://github.com/user-attachments/assets/76e502d8-e9a1-4665-9694-72d34665352f" />


## Week 7 (07/06/2026) - 43 Hours

Days worked on:

Monday – 9 hours<br>
Tuesday – 8 hours<br>
Wednesday – 9 hours<br>
Thursday – 8 hours<br>
Friday – 9 hours<br>

- Double-checked the schematic and cross-checked layout recommendations on datasheets
- Generated Gerber files
- Exported Pick & Place files
- Started to make the BOM file (Took so long; JLC PCB needs its own formatting) 
- Uploaded files to JLCPCB
- Corrected orientation issues
- Started to work on PCB CAD files!

  <img width="1601" height="766" alt="image" src="https://github.com/user-attachments/assets/106a23a2-7dac-48eb-a41a-7a58cd233da1" />
  <img width="1627" height="839" alt="image" src="https://github.com/user-attachments/assets/e84abde6-ee1a-4cf0-a323-e57edda4a298" />
  <img width="1611" height="834" alt="image" src="https://github.com/user-attachments/assets/302b2d0e-ed4c-41f9-8302-bf138707feac" />


## Week 8 (07/13/2026) - 43 Hours

Days worked on:

Monday – 9 hours<br>
Tuesday – 8 hours<br>
Wednesday – 9 hours<br>
Thursday – 8 hours<br>
Friday – 9 hours<br>

- Imported the full PCB and started to make a general board mount
- Made mistakes on tolerances and fixed (Did not account for anodization) 
- Made the full button half with no cutout
- Made the top half and then started to make a cutout for usb followed by rounding to match curve
- Added standoffs to the lower half
- Added text to indicate what each breakout is for
- Finalized the screws needed and threaded each hole
- Cross-checked everything and made renders!

  <img width="1633" height="830" alt="image" src="https://github.com/user-attachments/assets/617ee5be-021c-45ea-bb45-9127ab4ed824" />
  <img width="1626" height="800" alt="image" src="https://github.com/user-attachments/assets/f2781039-dfaf-4a9b-9d7e-68c170ff8ace" />


# Physical Build

##COMING SOON (Hopefully?)
