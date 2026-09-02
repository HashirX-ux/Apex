# Apex

[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/status-in%20progress-orange?style=flat-square)]()
[![Layout](https://img.shields.io/badge/layout-112%20key%20full--size-111111?style=flat-square)]()
[![MCU](https://img.shields.io/badge/MCU-nRF52840-black?style=flat-square)]()
[![PCB](https://img.shields.io/badge/PCB-KiCad-314CB0?style=flat-square)]()
[![Firmware](https://img.shields.io/badge/firmware-ZMK-00599C?style=flat-square)]()
[![Wireless](https://img.shields.io/badge/wireless-BLE%205.0-blueviolet?style=flat-square)]()

> A fully wireless full-size mechanical keyboard built from scratch — custom PCB, per-key RGB, BLE 5.0, Kailh hot-swap, 0.91" OLED, rotary encoder, and a 3D-printed case. Designed for daily work. Routed by hand.

---

## What is it?

Apex is a custom **112-key full-size** wireless mechanical keyboard I designed from the ground up after building a macropad and deciding a store-bought board would never feel like mine.

The PCB is designed in **KiCad**, the case in **FreeCAD**, and the firmware runs on **ZMK**. It talks over Bluetooth 5.0 on a Nordic **nRF52840**, charges a 1500 mAh LiPo through an MCP73831, and uses **Kailh MX hot-swap sockets** so switches come out without a soldering iron.

On top of a standard full-size layout it adds:

- a **0.91" SSD1306 OLED** (128×32, I²C) for layer / battery / connection status
- an **EC11 rotary encoder** with push switch (volume and extras)
- an onboard **buzzer** driven by a 2N3904
- **per-key SK6812 Mini-E** reverse-mount RGB

Build log: [`Journal.md`](Journal.md)

---

## Why I built it

I already knew I could finish a macropad. A full keyboard is a different machine — matrix size, power, RF, a case you actually live with. I did not want to spend $200+ on something that still was not fully mine.

Apex is the daily-driver version of that idea: wireless, full-size, OLED, encoder, hot-swap, RGB. Every part on the board is a choice I can point to.

---

## Features

- 112 keys, full-size layout (ANSI 104 + 8 extra keys)
- 8×14 col2row matrix
- Wireless BLE 5.0 via Nordic nRF52840 (AQFN-73)
- USB-C wired + wireless dual mode
- Per-key SK6812 Mini-E RGB, reverse-mounted
- Kailh MX hot-swap sockets — no soldering to swap switches
- 0.91" OLED (SSD1306, 128×32, I²C)
- EC11 rotary encoder with push switch
- Onboard buzzer (2N3904 driver)
- 3.7 V LiPo 1500 mAh with MCP73831 charger
- 74AHCT125 level shifter for LED data (3.3 V → 5 V)
- USBLC6-2SC6 ESD protection on USB D+/D−
- 32 MHz crystal for the nRF52840
- ZMK firmware (USB + BLE, battery reporting, OLED, encoder, RGB)
- 2-layer PCB, KiCad, JLCPCB fabrication
- Custom 3D-printed case designed in FreeCAD

---

## Hardware Specs

| Component | Details |
|---|---|
| MCU | Nordic nRF52840-QIAA, AQFN-73 7×7 mm |
| Layout | Full-size, 112 keys (ANSI 104 + 8 extras) |
| Matrix | 8 rows × 14 columns, col2row |
| Switches | MX-compatible 5-pin, PCB mount × 112 |
| Hot-swap | Kailh CPG151101S11 MX sockets × 112 |
| LEDs | SK6812 Mini-E × 112, reverse mount on B.Cu |
| OLED | 0.91" 128×32 SSD1306, I²C (ER-OLED0.91) |
| Encoder | Alps EC11, 20 mm, with push switch |
| Buzzer | 12×9.5 mm, 2N3904 NPN driver |
| Wireless | Bluetooth 5.0 BLE |
| Wired | USB-C, dual-mode with BLE |
| Firmware | ZMK |
| Battery | 3.7 V LiPo 1500 mAh, JST PH 2.0 |
| Charger IC | MCP73831-2-MC, DFN-8 |
| Level shifter | 74AHCT125, TSSOP-14 |
| ESD protection | USBLC6-2SC6, SOT-23-6 |
| USB connector | GCT USB4105, 16-pin USB-C |
| Crystal | 32 MHz, 2016 4-pin, 12 pF load caps |
| Reset | SMD tactile, CK KMR2 |
| Fuse | 500 mA resettable, 1206 |
| PCB | 2-layer, FR-4, 1.6 mm, KiCad / JLCPCB |
| Case | 3D printed, FreeCAD |
| Status LED | 0603 SMD |

ZMK is currently targeted at `nice_nano_v2` as a bring-up stand-in. The PCB carries a **bare nRF52840** (not a Pro Micro module). Pin mapping on the real board is still being finished — see [Firmware](#flash-the-firmware).

---

## How to Build

### Order the PCB

1. Go to [JLCPCB](https://jlcpcb.com)
2. Upload the Gerbers from `pcb/gerber/gerber.rar`
3. 2-layer, FR-4, **1.6 mm**, HASL or **ENIG** (ENIG recommended for hot-swap pads and the AQFN-73)
4. Minimum order is 5 boards
5. Order a stencil for the nRF52840, SK6812 Mini-E, and other SMD parts — the AQFN-73 is not a hand-solder-first footprint

### Flash the Firmware

Firmware lives in [`frimware/`](frimware/) and is a **ZMK skeleton**, not the final keymap.

1. Fork this repo (or copy `frimware/` into a [ZMK config](https://zmk.dev/docs/user-setup) repo)
2. Current build target in `frimware/build.yaml`:

   ```yaml
   include:
     - board: nice_nano_v2
       shield: apex
   ```

3. Edit the keymap at `frimware/config/apex.keymap`
4. Push — GitHub Actions builds the `.uf2`
5. Download the artifact, double-tap reset to enter the bootloader, drag the `.uf2` onto the drive that appears

The overlay (`frimware/config/boards/shields/apex/apex.overlay`) is still a 5×14 bring-up matrix. The PCB is **8×14 / 112 keys**. Next step is mapping the real nRF52840 pins, OLED, encoder, buzzer, and the 112-LED chain.

### Assembly Notes

- Solder **SK6812 Mini-E** on **B.Cu**, reverse mount, emitting down through the switch holes
- Solder **Kailh hot-swap sockets** on **F.Cu**
- Each key gets a **1N4148W (SOD-123)** in the matrix
- Each LED gets a **100 nF 0805** decoupling cap next to it
- Place the **32 MHz crystal** and two **12 pF** caps as close to the nRF52840 as the layout allows
- **74AHCT125** shifts `LED_DATA_3V3` to 5 V `LED_DATA_OUT` — VCC of the shifter must be 5 V
- OLED on I²C: `SDA` / `SCL`, address `0x3C`
- Encoder: `ENC_A` / `ENC_B`, 20 mm EC11 with switch
- Buzzer: GPIO → **2N3904** (TO-92) → buzzer; **330 Ω** base resistor
- Battery: **JST PH 2.0** 2-pin on **J2**, 1500 mAh 3.7 V LiPo
- USB-C on **J1** (GCT USB4105) with **USBLC6-2SC6** on D+/D− and **5.1 kΩ** CC resistors
- Reset is **SW114** (KMR2 tactile)
- The nRF52840 AQFN-73 is 0.5 mm pitch — use stencil + hot plate / reflow, not a hobby iron as the first tool

---

## BOM

> Estimated total: **~$230 USD** — can drop to **$170–$200** buying locally and skipping extras (second switch pack, spare LEDs, extra PCBs).

Prices are typical AliExpress pack prices as of 2026. You buy the pack; you do not need every piece in it. Shipping not included.

| Component | Spec | Qty | Price | Notes | Link |
|---|---|---|---|---|---|
| Microcontroller | nRF52840-QIAA, AQFN-73 | ×1 | $5.00 | Bare Nordic SoC — BLE 5.0, 7×7 mm | [Buy](https://www.aliexpress.com/item/1005009698070392.html) |
| 74AHCT125 level shifter | TSSOP-14 | ×1 | $2.52 | Pack of 10 — LED data 3.3 V → 5 V | [Buy](https://www.aliexpress.com/item/1005008171122183.html) |
| MCP73831 LiPo charger | MCP73831-2-MC, DFN-8 3×2 mm | ×1 | $2.50 | Pack of 10 — **DFN-8 footprint**, not SOT-23-5 | [Buy](https://www.aliexpress.com/item/1005007439657191.html) |
| USBLC6-2SC6 ESD | SOT-23-6 | ×1 | $1.50 | Pack of 10 — USB D+/D− | [Buy](https://www.aliexpress.com/item/32807108222.html) |
| MX mechanical switches | 5-pin PCB mount | ×112 | $32.00 | Pack of 110–120 — Gateron / any MX 5-pin | [Buy](https://www.aliexpress.com/item/1005006091988869.html) |
| Kailh hot-swap socket | MX compatible, CPG151101S11 | ×112 | $14.00 | Pack of 100 × 2 | [Buy](https://www.aliexpress.com/item/1005006105603269.html) |
| SK6812 Mini-E RGB LED | Reverse mount, 3.2×2.8 mm | ×112 | $27.00 | Pack of 100 × 2 — buy 200, use 112 + spares | [Buy](https://www.aliexpress.com/item/1005004249903121.html) |
| 1N4148W matrix diode | SOD-123 | ×112 | $3.00 | Pack of 100 × 2 | [Buy](https://www.aliexpress.com/item/1005010728396328.html) |
| EC11 rotary encoder | 20 mm, with push switch | ×1 | $2.00 | Pack of 5 | [Buy](https://www.aliexpress.com/item/1005006460161288.html) |
| Rotary knob | Aluminum, 6 mm D-shaft, 20 mm | ×1 | $2.00 | 2 pieces | [Buy](https://www.aliexpress.com/item/4001091267351.html) |
| Reset button | SMD tactile, CK KMR2 | ×1 | $1.50 | Pack of 30 | [Buy](https://www.aliexpress.com/item/4001107416458.html) |
| OLED display | 0.91" 128×32 SSD1306 I²C | ×1 | $2.50 | ER-OLED0.91, address 0x3C | [Buy](https://www.aliexpress.com/item/1005004375650245.html) |
| Buzzer | 12×9.5 mm, 5 V | ×1 | $1.80 | Pack of 10 — matches 12×9.5 RM7.6 footprint | [Buy](https://www.aliexpress.com/item/4000829554492.html) |
| 2N3904 transistor | TO-92 | ×1 | $1.40 | Pack of 50 — buzzer driver | [Buy](https://www.aliexpress.com/w/wholesale-2n3904-transistor.html) |
| 32 MHz crystal | SMD 2016, 4-pin | ×1 | $1.80 | Pack of 10 — nRF52840 HFCLK | [Buy](https://www.aliexpress.com/w/wholesale-32mhz-crystal.html) |
| Status LED | 0603 SMD | ×1 | $1.00 | Pack of 100 — charger / power indicator | [Buy](https://www.aliexpress.com/w/wholesale-0603-smd-led.html) |
| Resistor 10 kΩ | 0603 | ×3 | $1.20 | Pack of 300 — I²C / reset pull-ups | [Buy](https://www.aliexpress.com/item/1005011779883974.html) |
| Resistor 5.1 kΩ | 0603 | ×2 | $1.30 | Pack of 300 — USB-C CC1/CC2 | [Buy](https://www.aliexpress.com/item/1005011779883974.html) |
| Resistor 330 Ω | 0603 | ×1 | $2.00 | Pack of 500 — buzzer base / LED | [Buy](https://www.aliexpress.com/item/1005005700395390.html) |
| Resistor 1 kΩ | 1206 + 0805 | ×2 | $1.20 | Pack of 300 — PROG / current limit | [Buy](https://www.aliexpress.com/item/1005011779883974.html) |
| Capacitor 100 nF | 0805 | ×119 | $2.00 | Pack of 200 — 112 LED + MCU decoupling | [Buy](https://www.aliexpress.com/item/1005007660078779.html) |
| Capacitor 12 pF | 0402 | ×2 | $1.50 | Pack of 100 — crystal load | [Buy](https://www.aliexpress.com/w/wholesale-0402-12pf-capacitor.html) |
| USB-C receptacle 16P | GCT USB4105 SMD | ×1 | $4.50 | Pack of 5 | [Buy](https://www.aliexpress.com/item/1005005581945089.html) |
| JST PH 2-pin | PH2.0, B2B-PH-K vertical | ×1 | $2.00 | Pack of 2 — battery connector | [Buy](https://www.aliexpress.com/item/1005010615395743.html) |
| Polyfuse 500 mA | Resettable, 1206 | ×1 | $1.70 | Pack of 10 | [Buy](https://www.aliexpress.com/item/1005005235906949.html) |
| LiPo 3.7 V 1500 mAh | JST PH 2.0 | ×1 | $5.80 | Size to fit the case tray | [Buy](https://www.aliexpress.com/item/1005010110802624.html) |
| Keycap set | PBT, full-size MX | ×104+ | $26.00 | 104-key set; extras needed for 112 | [Buy](https://www.aliexpress.com/w/wholesale-104-keycap-set.html) |
| PCB fabrication | 2-layer, FR-4, 1.6 mm, HASL/ENIG | ×5 boards | $32.00 | Full-size board — ENIG preferred | [JLCPCB](https://cart.jlcpcb.com/quote) |
| 3D print — case | FDM PETG / SLA resin | ×1 | $42.00 | FreeCAD sources in `cad/` — local print is cheaper | [JLC3DP](https://jlc3dp.com/3d-printing-quote) |
| M3 screws | M3 × 8 mm countersunk | ×10 | $1.00 | Pack of 50 | [Buy](https://www.aliexpress.com/item/1005008810897680.html) |
| M3 standoffs | M3 × 4–6 mm | ×10 | $1.00 | Pack of 50 | [Buy](https://www.aliexpress.com/item/1005008810897680.html) |

**BOM notes**

- The charger footprint on the PCB is **DFN-8 (MCP73831-2-MC)**. A SOT-23-5 MCP73831 will not fit without a bodge.
- SK6812 Mini-E must be the **reverse-mount** Mini-E, not SK6812 Mini or WS2812B 3535.
- Hot-swap sockets are **Kailh MX** (CPG151101S11), 1.00u. Stabilizers are still required on 2U+ keys (not listed — use your usual plate/PCB-mount Cherry-style stabs).
- nRF52840 can run from VDDH (2.5–5.5 V high-voltage mode), which is why there is no separate 3.3 V LDO on this rev. LEDs are 5 V (`LED_5V` / VBUS).
- PROG resistor on the MCP73831 sets charge current (`IREG ≈ 1000 / RPROG`). 1 kΩ ≈ 1 A; 2 kΩ ≈ 500 mA. 500 mA is gentler on a 1500 mAh cell.

---

## Repository

```text
Apex/
├── cad/                  FreeCAD case + STEP
│   ├── APex cad.FCStd
│   └── .step
├── frimware/             ZMK config (skeleton)
│   ├── build.yaml
│   └── config/
│       ├── apex.conf
│       ├── apex.keymap
│       └── boards/shields/apex/
├── pcb/
│   ├── apex-pcb_design.kicad_sch
│   ├── apex-pcb_design.kicad_pcb
│   ├── LED-Design.kicad_sch
│   └── gerber/gerber.rar
├── Journal.md            Build log
└── LICENSE               MIT
```

---

## Credits

- [KiCad](https://www.kicad.org/) — PCB design
- [ZMK Firmware](https://zmk.dev/) — open-source wireless keyboard firmware
- [FreeCAD](https://www.freecad.org/) — case design
- [Nordic Semiconductor](https://www.nordicsemi.com/) — nRF52840
- [nice!nano](https://nicekeyboards.com/nice-nano/) — ZMK bring-up target
- Guides that got this off the ground: [nice!nano docs](https://nicekeyboards.com/docs/nice-nano/), [JLCPCB keyboard PCB guide](https://jlcpcb.com/blog/pcb-keyboards-design-guide), [Masterzen keyboard design series](https://www.masterzen.fr/2020/05/03/designing-a-keyboard-part-1/)

Made by **Hashir** — 2026

---

## License

[MIT](LICENSE)
