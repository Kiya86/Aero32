| Title | Author | Description | Created_at |
|--------|--------|-------------|------------|
| Aero32 | Kiya | AI Camera Module! | 2026-07-24 |

# Dev Log "Aero32"

**Total Time (Hours): 352 Hours**

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

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

---

# Physical Build

##COMING SOON (Hopefully?)
