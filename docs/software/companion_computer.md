# Companion Computer Setup

A companion computer (e.g., Raspberry Pi, Jetson Nano) allows for high-level algorithm execution (like computer vision or swarm logic) that the flight controller cannot handle.

## 1. Operating System

- Flash the OS image (e.g., Ubuntu Server 20.04/22.04 or a JetPack image for Nvidia hardware) to an SD card.
- Configure Wi-Fi and enable SSH before inserting the SD card into the companion computer to allow headless access.

## 2. Hardware Connection (UART & UBEC)

Because the Flight Controller's internal 5V regulator cannot supply enough current (the Raspberry Pi requires ~3A), you **must** use an external UBEC and wire the data connection directly via UART. Do not use a USB cable for flight!

### Power Wiring (UBEC)
1. Solder the input of a **5V/3A UBEC** directly to the drone's battery pads (or Power Distribution Board).
2. Connect the UBEC's 5V output to **Pin 2 or 4 (5V Power)** on the Raspberry Pi GPIO header.
3. Connect the UBEC's GND output to **Pin 6 (Ground)** on the Raspberry Pi.

### Data Wiring (UART)
Connect the Raspberry Pi's GPIO UART pins to a spare UART on the Matek Flight Controller (e.g., UART2 / TELEM2):
- **FC TX2** connects to **Pi RXD** (Pin 10 / GPIO 15)
- **FC RX2** connects to **Pi TXD** (Pin 8 / GPIO 14)
- **FC GND** connects to **Pi GND** (Pin 14 or any ground pin)

!!! important
    RX always connects to TX, and TX connects to RX. You must also connect the ground wire between the FC and Pi to ensure stable data transmission!

## 3. Flight Controller Configuration (MAVLink)

To tell the Flight Controller to send MAVLink data over this UART connection:
1. Open your Ground Control Station (QGroundControl or Mission Planner) and connect to the drone.
   - **In QGroundControl:** Go to **Vehicle Setup -> Parameters**.
   - **In Mission Planner:** Go to **Config -> Full Parameter List**.
2. Search for the `SERIALx` parameter that matches your chosen UART (e.g., if using UART2, look for `SERIAL2`).
3. Set **`SERIALx_PROTOCOL`** to `2` (MAVLink 2).
4. Set **`SERIALx_BAUD`** to `921` (921600 baud rate for high bandwidth).
5. Write/Save the parameters and reboot the flight controller.

On the Raspberry Pi side, ensure your `MAVROS` launch file or custom script is configured to read from `/dev/serial0` (or `/dev/ttyAMA0`) at `921600` baud.

## 3. ROS / ROS 2 Setup (Optional but Recommended)

If using the Robot Operating System (ROS) for your algorithms:

1. Follow the official installation instructions for your chosen ROS distribution (e.g., ROS 2 Humble).
2. Install the necessary middleware to communicate with the flight controller:
   - For ArduPilot: Install `MAVROS`.

## 4. Network Configuration

Set up a static IP for the companion computer when connected to the ground station network, or configure it to broadcast its own Wi-Fi hotspot for easy field access.
