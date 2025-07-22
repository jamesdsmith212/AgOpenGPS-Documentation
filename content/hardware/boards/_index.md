+++
title = "Boards"
simple_list = true
weight = 4
+++

## Overview

AgOpenGPS hardware is built around a set of modular, open-source circuit boards.
These boards connect your sensors, actuators, and control devices, and are
designed to make installation, troubleshooting, and upgrades as easy as
possible.

Below you'll find a brief overview of the boards.

---

## Types of Boards

### 1. [All-In-One (AIO) Boards](all-in-one-boards/)

- **Purpose:** The most popular and recommended option for new builds. Combines
  all essential functions (steering, sensors, power management, networking) onto
  a single PCB.
- **Versions:** Multiple generations exist (e.g., v2.4, v4.5). Each version
  brings improvements in features, reliability, and ease of assembly. The latest
  version (July 2025) is the v4.5.

### 2. [Implement Boards](/hardware/boards/implement-boards)

For controlling additional devices, such as section control or implement lift.

### 3. Legacy Boards

- **Purpose:** Early designs, now largely replaced by AIO boards. Still useful
  for reference or for supporting older builds.
- **Note:** New users are strongly encouraged to use the latest AIO boards.

---

## Choosing the Right Board

- **New to AgOpenGPS?**  
  Start with the latest All-In-One (AIO) board. It’s the most supported, easiest
  to assemble, and has the best documentation. you can add rate control/section
  control later

---

## Board Assembly & Configuration

- Most boards are available as pre-assembled PCBs from manufacturers like
  JLCPCB, or you can order the bare PCB and solder components yourself.
- After assembly, you’ll need to:
  1. Install the microcontroller (usually a
     [Teensy 4.1](../Other-components/teensy-4.1.md))
  2. Flash the firmware (see
     [Configuring the Teensy](../boards/configuring-boards/Configuring-The-Teensy.md))
  3. Connect sensors, actuators, and power
  4. Wire up the correct cables to run to and from your board
  5. Install the board in-cab and power up

---

## Board Documentation

- [All-In-One Boards](all-in-one-boards/)
- [Micro AIO Board](micro-aio-board/)
- [Configuring Boards](configuring-boards/)
- [Steering Options](/hardware/steering-options/)
- [Other Components](/hardware/Other-components/)

---

## Community & Support

- **Forum:** [AgOpenGPS Discourse](https://discourse.agopengps.com)
- **Telegram:** [@AgOpenGPSInternational](https://t.me/AgOpenGPSInternational)
- **GitHub:**
  [AgOpenGPS-Official/Boards](https://github.com/AgOpenGPS-Official/Boards)

If you’re unsure which board to choose, or need help with assembly, the
community is always happy to help!
