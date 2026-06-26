# Aero32 (duh)

**hey. HEY.** this is not the Arduino tutorial you googled at 11pm.  

## Contents

- [Wait, What Even Is This?](#wait-what-even-is-this)

## Wait, What Even Is This?

Aero32 is a compact AI vision co-processor designed to plug into an existing flight computer via **UART, I2C, or SPI**. This is so that the flight computer doesn't have to do as much work. 

It runs an **STM32N6** which has a built-in Neural Processing Unit (NPU). This allows it to run object detection off-grid! 

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
