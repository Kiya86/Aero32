# 📋 Aero32 — Getting Started Guide

> **hey. HEY.** this is not the Arduino tutorial you googled at 11pm.  
> this is an STM32N6 AI camera board with a BGA-264 package and 6 power rails.  
> if you're looking for "how to blink an LED with Python" — [you want this.](https://www.raspberrypi.com/documentation/)  
> still here? okay. let's go.

---

```
    ██████╗  ██████╗  ███╗   ██╗ ██╗ ██╗
   ██╔═══██╗██╔═══██╗████╗  ██║ ██║ ██║
   ███████╔╝███████╔╝██╔██╗ ██║ ██║ ██║
   ██╔═══██╗██╔═══██╗██║╚██╗██║ ╚═╝ ╚═╝
   ██║   ██║██║   ██║██║ ╚████║ ██╗ ██╗
   ╚═╝   ╚═╝╚═╝   ╚═╝╚═╝  ╚═══╝ ╚═╝ ╚═╝
         AI Vision. No WiFi. No excuses.
```

---

## 🗺️ Table of Contents

- [Wait, What Even Is This?](#wait-what-even-is-this)
- [What You'll Need](#what-youll-need)
- [Powering It On (Without Smoke)](#powering-it-on-without-smoke)
- [Interfaces — Talking to Your Flight Computer](#interfaces)
- [Flashing Firmware](#flashing-firmware)
- [LED Decoder Ring](#led-decoder-ring)
- [FAQ (Frequently Avoided Questions)](#faq)
- [Known Issues (aka character)](#known-issues)

---

## Wait, What Even Is This?

Aero32 is a compact AI vision co-processor designed to plug into an existing flight computer via **UART, I2C, or SPI** and do the heavy thinking so your flight computer doesn't have to.

It runs an **STM32N6** — which has a built-in Neural Processing Unit (NPU) — meaning it can do real-time image classification and anomaly detection *on-chip*, with no cloud, no WiFi, no latency, and no subscription fee. Just vibes and inference.

Think of it like this:

```
┌─────────────────────────────────────────────┐
│                                             │
│   Flight Computer                           │
│   (busy doing important flight stuff)       │
│              │                              │
│              │  "hey what do you see?"      │
│              ▼                              │
│         [ AERO32 ]  ◄── camera              │
│      STM32N6 + NPU                          │
│      "I see a person / the ground /         │
│       something that shouldn't be there"    │
│                                             │
└─────────────────────────────────────────────┘
```

Got it? Good. Moving on.

---

## What You'll Need

Before you do anything, make sure you have:

| Thing | Why |
|---|---|
| Aero32 board | ...this should be obvious |
| USB-C cable (data capable, not your phone charger) | programming & debug |
| ST-LINK V3 or compatible debugger | actual firmware flashing |
| 2S–3S LiPo **OR** USB power | pick one, not both at the same time unless you enjoy debugging shorts |
| STM32CubeIDE or your IDE of choice | writing code |
| A camera module with 15-pin 1mm FPC | the whole point of this board |
| Patience | non-negotiable |

> ⚠️ **Do not power via XT30 AND USB-C simultaneously** without understanding what the TPS2121 power mux is doing. It *handles* it, but you should still know what's happening. Read the datasheet. Yes, the whole thing.

---

## Powering It On (Without Smoke)

The board has two power paths:

```
XT30 (battery) ──┐
                 ├──► TPS2121 Power Mux ──► VDCCORE ──► everything else
USB-C (VBUS) ───┘
```

The TPS2121 automatically picks the active source. When both are connected, battery wins. 

### Rail Map (a.k.a. "which rail does what")

| Rail | Voltage | Comes From | Powers |
|---|---|---|---|
| VDCCORE | battery input | LM61495 buck | main system |
| +3V3 | 3.3V | TPS560430 buck | logic & peripherals |
| 0VB33 | 3.3V (aux) | AP3441 buck | secondary 3.3V loads |
| VCC | 3.3V | TPS62088 buck | MCU core VCC |
| 1V8 | 1.8V | ETA5055 LDO | MCU I/O bank |
| 1V8B | 1.8V | ETA5055 LDO | secondary I/O |
| VBUS | 5V | USB-C | USB interface only |

> If a rail is missing, check your inductors first. Then check your inductors again.  
> Then check if you soldered the inductor backwards. (You did.)

---

## Interfaces

### UART × 2 — `CN2`, `CN3`

2-pin JST ZH 1.5mm connectors. Standard async serial. Hook these to your flight computer's UART RX/TX.

```
Pin 1 ── TX  (Aero32 transmits)
Pin 2 ── RX  (Aero32 receives)
```

Default suggested config: **115200 baud, 8N1**. Change it in firmware to whatever your flight computer expects. Don't forget to cross TX↔RX. Everyone forgets to cross TX↔RX.

---

### I2C × 2 — `CN4`, `CN5`

2-pin JST ZH 1.5mm. Pull-ups are already on board, so don't add more unless you enjoy signal integrity problems.

```
Pin 1 ── SDA
Pin 2 ── SCL
```

Default address range: whatever you set in firmware. Aero32 can be configured as controller or target.

---

### SPI × 1 — `CN6`/`CN7`

3–4 pin JST ZH 1.5mm. MOSI, MISO, SCK, CS. Fast. Great for streaming processed frame data when UART feels too slow.

---

### Camera (CSI) — `FPC1`

15-pin 1mm pitch FPC connector (Omron XF3M). Routes to the STM32N6's DCMI interface.

> ⚠️ **The FPC connector is fragile.** Flip the lock up *before* inserting the cable.  
> Do not force it. Ask me how I know.

Compatible with most OV series and similar parallel camera sensors. Check the STM32N6 reference manual for DCMI timing requirements before picking a sensor.

---

## Flashing Firmware

### Step 1 — Enter Boot Mode

Hold **BOOT0** (`SW1`), then press and release **NRST** (`SW2`), then release **BOOT0**.

```
[HOLD BOOT0] → [PRESS+RELEASE NRST] → [RELEASE BOOT0]
      ↓
   STM32N6 now in bootloader mode
   (nothing will look different. that's normal.)
```

### Step 2 — Connect via ST-LINK or USB DFU

- **ST-LINK:** Use STM32CubeProgrammer → connect via SWD
- **USB DFU:** Connect USB-C, device enumerates as DFU device, flash with `dfu-util` or CubeProgrammer

### Step 3 — Flash

Load your `.elf` or `.bin` and hit program. Watch the green LED.

### Step 4 — Reset

Press **NRST** (`SW2`) to exit boot mode and start execution.

If nothing happens: check your linker script. Check your clock config. Check that you didn't accidentally target the wrong MCU in CubeIDE. (We've all been there.)

---

## LED Decoder Ring

```
LED1 (Green) ──── Power OK (3.3V rail alive)
LED2 (Red)   ──── Fault / Error indicator
LED3 (Green) ──── User-defined (firmware)
LED4 (Red)   ──── User-defined (firmware)
LED5 (Green) ──── User-defined (firmware)
```

All user LEDs are active-low through 68Ω resistors. In firmware:

```c
// Turn on LED3 (example, adjust GPIO to your pinout)
HAL_GPIO_WritePin(LED3_GPIO_Port, LED3_Pin, GPIO_PIN_RESET); // LOW = ON
```

> If **all LEDs are off**: either power isn't on, or you have bigger problems.  
> If **all LEDs are on**: you definitely have bigger problems.

---

## FAQ

**Q: Why STM32N6? Isn't that overkill?**  
A: Yes. That's the point.

**Q: Can I use this without a camera?**  
A: Technically yes. You'd just be running a very expensive microcontroller to blink some LEDs over SPI.

**Q: Why 6 layers?**  
A: EMI. Signal integrity. Controlled impedance. And also because 4 layers wasn't enough once the BGA fanout got involved.

**Q: What camera should I use?**  
A: Whatever has a 15-pin 1mm FPC and a pixel clock under what the DCMI interface supports. Check the datasheet. Yes, again.

**Q: The board isn't booting.**  
A: Is the 1V8 rail up? Is the 3V3 rail up? Is NRST being held low by something? Is the oscillator oscillating? Work down the list.

**Q: I shorted something.**  
A: Touch the board. Find the hot spot. That's where you shorted something.

**Q: Do I really need to read the LM61495 datasheet?**  
A: You're asking this after you've already assembled the board, aren't you.

---

## Known Issues

| Issue | Status | Workaround |
|---|---|---|
| Guide.md was empty for a while | ✅ Fixed (you're reading it) | N/A |
| BOM link in original README pointed to wrong path | ✅ Fixed | Updated to `PCB/Aero32_BOM.csv` |
| FPC connector will betray you if you're not careful | 🟡 Permanent | Be careful |
| The STM32N6 has a lot of pins | 🟡 Permanent | Read. The. Datasheet. |

---

> **Aero32** — an independent project.  
> Not affiliated with any rocketry team, drone manufacturer, or the FAA.  
> Build responsibly. Don't fly over people.
