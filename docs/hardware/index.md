# Hardware Overview

Welcome to the Hardware section of the SwarmSummerSchool 2026 drone build. This section contains all the physical component details and assembly guides.

## Table of Contents

- **[Bill of Materials (BOM)](bom.md)**: A complete inventory checklist of all required drone parts, including motors, ESCs, the flight controller, and the companion computer.
- **Assembly Guides**:
  - **[Welding & Soldering Guide](assembly/welding.md)**: Detailed instructions on soldering the XT60 connectors, ESCs, and preparing the Power Distribution Board (PDB).
  - **[Nipping & Wiring Guide](assembly/nipping.md)**: Best practices for wire management, stripping, and securing cables cleanly to the quadcopter frame.
  - **[Motor Mounting](assembly/motors.md)**: Motor identification, fastener sizing, and thread orientation.

## System Architecture & Interconnect Matrix

### Power & Communication Topology Schema

**Power Line:**
- Gens ace 4S 5000mAh LiPo Battery (14.8V) -> XT90 Output
- XT90 Female to XT60 Male Adapter Lead (10AWG)
- F450 Main Frame Integrated Power Distribution Board (PDB)

**PDB Split Branches:**
- **4x 30A ESCs**: Direct LiPo Voltage -> 2212 Motors
- **5V 3A UBEC**: Step-Down Power -> Raspberry Pi 4
- **Matek H743-SLIM FC**: VBAT Pad Power + Battery Sensor

**Interconnect Link between Pi and FC:**
- Raspberry Pi 4 (Companion PC) <-> MAVLink2 Serial UART (TX1/RX1 <-> GPIO 14/15) <-> Matek H743 Flight Controller
