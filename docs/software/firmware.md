# Firmware Setup (ArduPilot)

!!! info "Official ArduPilot Documentation"
    For comprehensive details on all calibration and setup steps, we highly recommend referencing the official [ArduPilot Hardware Configuration Guide](https://ardupilot.org/copter/docs/configuring-hardware.html#).

This section covers flashing the ArduPilot firmware to the flight controller and performing the initial configuration.
## 1. Flashing Firmware

For this project, we exclusively use **ArduPilot (ArduCopter)**.

### Using Mission Planner
1. Download and install [Mission Planner](https://ardupilot.org/planner/docs/mission-planner-installation.html) on a Windows PC (or via Mono on Linux/Mac, though Windows is highly recommended).
2. Connect your flight controller via USB to your computer.
3. Open Mission Planner, but **do not connect** (leave the connection state as disconnected).
4. Navigate to the **Setup** menu -> **Install Firmware**.
5. Select the **ArduCopter** firmware (usually a multirotor icon).
6. Follow the on-screen prompts to download and flash the firmware to your flight controller.

## 2. Sensor Calibration

Once the firmware is installed, connect to the flight controller in Mission Planner and calibrate the onboard sensors:
- **Accelerometer**: Go to Setup -> Mandatory Hardware -> Accel Calibration. Follow the prompts to place the drone level, on its left, right, nose down, nose up, and on its back.

## 3. GPS & Compass Setup (GEP-M10 / M9N)

If you are using a GPS module like the **GEP-M10** or **M9N**, you will need to configure the serial port and calibrate the external compass (since the Matek H7A3-SLIM has no internal compass).

### Parameter Configuration
Since the GPS is wired to **UART3**, ensure the following parameters are set in Mission Planner (Config &rarr; Full Parameter List):
* `SERIAL3_PROTOCOL = 5` (GPS)
* `SERIAL3_BAUD = 115` (115200 baud is standard for M10; M9N may use 38 or 115. ArduPilot usually auto-detects this).
* `GPS_TYPE = 1` (Auto - ArduPilot will probe for the U-blox protocol).

### Compass Calibration
1. Navigate to **Setup &rarr; Mandatory Hardware &rarr; Compass**.
2. Because the flight controller has no built-in compass, you should only see one compass checked as "Use" (the external one on the GPS module via I2C).
3. **Orientation:** Modern ArduPilot versions (like 4.7.0) can auto-detect the compass orientation during the MagFit calibration. If auto-detect fails, you may need to manually set the orientation drop-down (common values for GEP modules are `ROTATION_NONE`, `ROTATION_YAW_90`, or `ROTATION_YAW_270` depending on how the arrow on the GPS puck is aligned with the drone's nose).
4. Click **Start** under Onboard Mag Calibration.
5. Slowly rotate the drone around all of its axes (pitch, roll, yaw, and upside down) until the progress bar completes.

## 4. Radio Setup

Bind your RC transmitter to the receiver on the drone.
In Mission Planner, go to **Setup -> Mandatory Hardware -> Radio Calibration** and follow the prompts to calibrate the sticks and assign switches (e.g., Flight Mode switch, Kill switch/Arming).

## 5. ESC Calibration

If you are using standard PWM ESCs (not DShot), you must calibrate them so they know the minimum and maximum throttle limits of your radio:
1. Turn on your transmitter and push the throttle stick to the **maximum** (top) position.
2. Connect the battery to the drone. The flight controller's LEDs will cycle.
3. Disconnect the battery immediately, then reconnect it.
4. The ESCs will emit a musical tone, followed by a set of beeps (indicating they registered the maximum throttle).
5. Pull the throttle stick down to its **minimum** (bottom) position. The ESCs will emit a long beep to confirm calibration is complete.
6. Disconnect the battery. Your ESCs are now calibrated.

*(Note: If you are using DShot ESCs, calibration is not required.)*

## 6. Flight Modes

Set up at least three flight modes in **Setup -> Mandatory Hardware -> Flight Modes** for initial testing:
- **Stabilize**: Fully manual control with self-leveling.
- **Loiter**: Uses GPS and barometer to hold position and altitude. Essential for outdoor flying.
- **RTL (Return to Launch)**: A safety mode that brings the drone back to the takeoff point and lands automatically.
