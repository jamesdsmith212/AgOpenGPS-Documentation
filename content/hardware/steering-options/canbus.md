+++
title = "Steering via CANBUS"
linkTitle = "CANBUS"
weight = 10
description = "Comprehensive guide to steering via CANBUS. Explains how to interface with tractor CAN systems, required hardware, configuration steps, and specific notes for various tractor brands."
+++

## Overview

## Introduction to canbus

CommonRail has written a superb guide on how to investigate the CANbus on your
system - give it a good read!

https://discourse.agopengps.com/t/canbus-for-beginners-super-simple/3814/884

https://discourse.agopengps.com/c/hardware/canbus/33

[Here's a success story](https://discourse.agopengps.com/t/steering-a-22-mf-6718s-over-canbus/11955)
using the AIO and CANBUS to control an MF 6718S

The Teensy has 3 CANBUS receivers on it, but you still need transceivers. The
AIO 2.4 board has space for 2 transceivers and the 4.x boards have space for 1.
The part you're looking for is
https://www.mouser.co.uk/ProductDetail/579-MCP2562T-E-SN

These are absolutely tiny and you'll be soldering them on here most likely:

![image](../../img/canbus-receivers-pcb.png)

## The PCB of Tony

CommonRail has an excellent resource including the code you need
[here](https://github.com/MechanicTony/AOG_CAN_Teensy4.1) on how to learn about
CANBUS, and control your machine with it.

CAN controllers on Tonys board as per:

- CAN1: Tractor BUS / armrest when the Engage message (button) is one a
  different bus from the valve.
- CAN2: ISOBUS (not really in use) we can put NMEA2000 position on the bus
- CAN3: V-Bus or Valve Bus this is where we communicate with the valve. (Read
  the angle, send the desired angle)

### Post assembly steps

Once you have the board assembled and flashed use Arduino IDE or similar tool to
do the necessary configuration via the Service menu over Serial.  
Usually we set P for Panda mode at 460k (just like the AIO board)  
Select the brand we should emulate.

## Tractor Brand Specifics

### Generic CAN connector

Pinout is as follows:

![image](../../img/can-connector-pinout.png)

### Case / New Holland

Activate the necessary in the [HH menu](../../files/NH_H3_Config.pdf) There's
also a CH3 which MUST be NO else you'll have errors.

Maybe you need to [calibrate the WAS as well](../../files/NH_Steering_Cal.pdf)

Locate the pins for the bus this varies from tractor to tractor. Use a CAN
Sniffer and the sourcecode (CAN_ALL_Brands) to see if you see those messages. We
don't care about their content just the message header. For example:

> 0x0CACAA08, EXT); //CaseIH Curve Data & Valve State Message

### Massey Ferguson

Massey steer bus location:

![image](../../img/can-massey-ferguson.png) (There's also a black DT 3P
connector with a CAN terminator on some models.)

### Fendt

V-Bus is for steering:

![image](../../img/can-fendt.png)

![image](../../img/can-fendt2.png)

### Tracked Challengers

Here the WAS can't be sniffed. There's a 4pin DT connector behind the right
cover where you want to attach yourself. There's no engage button by default so
wire one for the CAN board. Put it gear, let it drive slow, move the steering a
bit then engage from the tablet.

### Claas

This can only be steered if we break the factory quicksteer.  
You'll have to modify the wiring harness. The necessary connectors can't be
easily sourced however there's a similar connector where you can break or grind
out the positioning tabs to make it fit.  
Connector for the CAN (buy these in pairs)

- 16pin: 2-963217-1 + 2-964449-1
- 6pin: 5-967241-1 + 2-962349-1

We'll steal the 2 CAN circuits (Tractor -> CAN1 , Steer -> CAN3) + 12V from the
6 pin connector.  
Using the Serial Service tool of Teensy we need to modify the PVED valve
settings.

### Valtra

It has a button to engage but it never worked. Easier to add your own button.
Otherwise it's the same deal: Find the pins with the right can message. Add your
controller and off you go.

## How to engage steering

Make sure that:

- The tractor is in gear and drives
- You're not riding the clutch
- There was movement on the steering wheel in the last 30? or so seconds.
- Operator is in the seat (yes a faulty seat switch can also give you trouble)
- sometimes you need to be going forward at speeds greater than 1.5km/h but
  under 25km/h sometimes you can engage even in reverse
- Case / New Holland / CNH require the main switch to be turned OFF then ON
  after every time you start the tractor
- Road lockout / hydraulic lockout switch is NOT active
- If Quicsteer / SpeedSteer or similar is present: It works
- Sometimes it also helps if you set Steer Enable in steer settings to NONE and
  engage from the tablet. (We'll worry about the presence of the pyhsical button
  later.)

## Other links

If you want to learn how to sniff the CANBUS and find out joystick codes etc,
watch this: https://youtu.be/O01Fy4dBw6s

## CANBUS Glossary

All definitions in this glossary were LLM generated. Use with caution.

- **CANBUS (Controller Area Network Bus):** A robust vehicle bus standard
  designed to allow microcontrollers and devices to communicate with each other
  without a host computer, commonly used in automotive and agricultural
  machinery.
- **Transceiver:** An electronic device that both transmits and receives analog
  or digital signals, required for CANBUS communication.
- **MCP2562T-E/SN:** A specific CANBUS transceiver IC (integrated circuit) used
  to interface microcontrollers with the CANBUS.
- **CAN Controller:** A device or chip that manages CANBUS communication,
  handling the sending and receiving of CAN messages.
- **ISOBUS:** An international standard (ISO 11783) for communication between
  tractors and implements, based on CANBUS.
- **NMEA2000:** A communication standard used in marine electronics, also based
  on CANBUS.
- **V-Bus (Valve Bus):** A specific CANBUS network dedicated to communicating
  with hydraulic or steering valves.
- **Arduino IDE:** An open-source development environment used for programming
  microcontrollers like the Teensy.
- **Service Menu (over Serial):** A configuration interface accessed via serial
  communication (USB/COM port) to set up hardware parameters.
- **Panda Mode:** A specific CANBUS communication mode or protocol setting,
  often referring to a baud rate of 460k.
- **Pinout:** The arrangement or mapping of pins on a connector or device,
  showing their functions.
- **CAN Sniffer:** A tool or device used to monitor and analyze CANBUS traffic,
  useful for reverse engineering or troubleshooting.
- **Sourcecode (CAN_ALL_Brands):** The program code used to support multiple
  tractor brands in CANBUS communication.
- **Message Header:** The identifier part of a CANBUS message, used to
  distinguish between different types of data.
- **DT Connector:** A type of rugged, multi-pin electrical connector commonly
  used in automotive and agricultural equipment.
- **CAN Terminator:** A resistor placed at the end of a CANBUS network to
  prevent signal reflections and ensure reliable communication.
- **Quicksteer / SpeedSteer:** Factory or aftermarket systems that allow for
  faster or easier steering, sometimes requiring special handling in CANBUS
  setups.
- **PVED Valve:** A type of electrohydraulic valve used for steering control,
  often configurable via CANBUS.
- **Engage Message/Button:** A CANBUS message or physical button used to
  activate the steering system.
- **Hydraulic Lockout:** A safety feature that disables hydraulic functions,
  including steering, under certain conditions.
- **Road Lockout:** A feature that prevents automatic steering when the vehicle
  is on the road for safety reasons.
- **Serial Service Tool:** Software or interface used to configure hardware via
  serial communication.
- **Bus:** In electronics and computing, a bus is a communication system that
  transfers data between components inside a computer or between computers. In
  the context of CANBUS, it refers to the network or wiring system that allows
  multiple devices (controllers, sensors, actuators) to communicate with each
  other over shared signal lines.
