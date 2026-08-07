# Communication Links

## Architecture Overview

<iframe src="../communication_diagram.html" width="100%" height="400px" style="border: none; margin: 20px 0; border-radius: 12px; background-color: #0f172a;"></iframe>


## Companion Computer (Raspberry Pi)

Connects to a spare FC UART (TX/RX/GND) for direct MAVLink access, and is powered directly from the flight battery via a 5V/3A UBEC step-down regulator. Runs the SAR mission software. Independent of the telemetry link below.

## Wireless Telemetry Link

DroneBridge for ESP32, on a XIAO-ESP32-C6 (telemetry-only role).

Wires directly to a spare FC UART (independent of the Pi) and bridges MAVLink over standard WiFi to a ground station — replaces needing a wired/USB tether or traditional telemetry radio.
