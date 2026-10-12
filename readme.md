# FRC CAN Node

A compact, general-purpose controller for FRC robotics applications built around the Seeed Studio XIAO ESP32-C3. The design is intended to serve as a small CAN-connected node for sensors, actuators, and other peripherals in a robot system, while remaining easy to integrate into a distributed electrical architecture.

## Overview

This board is designed to operate from a standard 12 V DC input and provide a robust power and communications interface for an embedded controller. It includes:

- reverse-polarity protection at the input
- input fuse protection
- transient suppression for automotive-style electrical noise
- a DC-DC regulator to generate clean logic power
- a CAN bus transceiver for reliable communication on the robot network
- an I²C bus and multiple user-configurable 3-pin ports for external devices

The result is a compact CAN-capable node that is suitable for distributed sensor hubs, actuator interfaces, and experimental robot electronics.

## Key Features

- 12 V DC input support
- Reverse-polarity protection using AO4407A MOSFET
- Fuse protection via 1812L075/24DR
- Bidirectional transient protection with SMBJ18CA TVS diode
- Efficient step-down power conversion using LMR14006CDDCR
- CAN bus interface using SN65HVD231DR with PESD1CAN protection
- XIAO ESP32-C3 as the main MCU
- Optional upgrade path to XIAO ESP32-S3 for increased performance
- I²C connectivity for peripherals
- Three 3-pin user ports for sensors and accessories

## Hardware Architecture

The design follows a practical robotics power and signal layout:

1. 12 V input enters the board
2. Input protection limits damage from faults and transients
3. Reverse-polarity MOSFET prevents incorrect wiring from destroying the system
4. DC-DC converter creates the internal logic rail
5. MCU runs control logic and communicates with the rest of the robot
6. CAN transceiver connects the node to the FRC CAN bus
7. I²C and user ports expose additional peripheral connections

This architecture keeps the module compact while providing the protection needed for real-world robot environments.

## Main Components

- 1812L075/24DR — input fuse
- SMBJ18CA — TVS transient protection
- AO4407A — reverse-polarity protection MOSFET
- LMR14006CDDCR — DC-DC converter
- Seeed Studio XIAO ESP32-C3 — main microcontroller
- XIAO ESP32-S3 — potential higher-performance alternative
- SN65HVD231DR + PESD1CAN — CAN bus transceiver and protection

## Intended Use Cases

This CAN node is intended for:

- sensor aggregation in robot subsystems
- low-cost distributed control nodes
- actuator interfaces
- experimental robotics prototyping
- expansion of a robot's CAN network with compact local intelligence

## Design Notes

The board is intentionally compact and modular, making it useful for custom robot electronics where a small, robust node is needed. The selected components target reliability: transient suppression protects against voltage spikes, reverse-polarity circuitry prevents damage during installation, and the CAN interface provides a standard bus connection for interoperability with other robot devices.

## Repository Layout

- `hardware/` — PCB and schematic assets (to be added)
- `firmware/` — microcontroller firmware and examples (to be added)
- `docs/` — design notes and documentation (to be added)
- `LICENSE` and `LICENSES/` — licensing information

## License

This project is released under open hardware and software-friendly licensing terms:

- MIT License for software/code where applicable
- CERN-OHL-P-2.0 for hardware design content

## Status

This repository currently contains the project summary and licensing materials, with the hardware and firmware assets to be expanded as the design progresses.
