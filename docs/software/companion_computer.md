# Companion Computer Setup

A companion computer (e.g., Raspberry Pi, Jetson Nano) allows for high-level algorithm execution (like computer vision or swarm logic) that the flight controller cannot handle.

## 1. Operating System

- Flash the OS image (e.g., Ubuntu Server 20.04/22.04 or a JetPack image for Nvidia hardware) to an SD card.
- Configure Wi-Fi and enable SSH before inserting the SD card into the companion computer to allow headless access.

## 2. Hardware Connection

Connect the companion computer to the flight controller:
- Typically, this is done via a UART (Serial) connection from the companion computer's GPIO pins (or USB) to the flight controller's `TELEM 2` port.
- **Baud Rate**: Ensure both ends are configured to the same baud rate (e.g., `921600` for high-bandwidth telemetry).

## 3. ROS / ROS 2 Setup (Optional but Recommended)

If using the Robot Operating System (ROS) for your algorithms:

1. Follow the official installation instructions for your chosen ROS distribution (e.g., ROS 2 Humble).
2. Install the necessary middleware to communicate with the flight controller:
   - For ArduPilot: Install `MAVROS`.

## 4. Network Configuration

Set up a static IP for the companion computer when connected to the ground station network, or configure it to broadcast its own Wi-Fi hotspot for easy field access.
