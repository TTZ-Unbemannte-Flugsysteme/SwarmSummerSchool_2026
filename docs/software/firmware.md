# Firmware Setup

This section covers flashing the firmware to the flight controller and performing the initial configuration.

## 1. Flashing Firmware

Depending on your requirements, choose either **PX4 Autopilot** or **ArduPilot**.

### Using QGroundControl (QGC)
1. Download and install [QGroundControl](http://qgroundcontrol.com/).
2. Connect your flight controller via USB to your computer.
3. Open QGC and navigate to the **Vehicle Setup** menu (gear icon).
4. Select the **Firmware** tab on the left.
5. Unplug and re-plug the USB cable to initiate the flashing sequence.
6. Choose the desired firmware (PX4 Pro or ArduPilot) and follow the on-screen prompts to flash.

## 2. Sensor Calibration

Once the firmware is installed, you must calibrate the onboard sensors:
- **Compass**: Rotate the drone through all 6 axes as instructed by QGC. Ensure you do this away from metallic objects.
- **Gyroscope**: Place the drone on a level surface and remain still during calibration.
- **Accelerometer**: Similar to compass calibration, hold the vehicle steady on all 6 sides.

## 3. Radio Setup

Bind your RC transmitter to the receiver on the drone.
In QGC, go to the **Radio** tab and follow the prompts to calibrate the sticks and assign switches (e.g., Flight Mode switch, Kill switch).

## 4. Flight Modes

Set up at least three flight modes for initial testing:
- **Stabilize/Manual**: Fully manual control with self-leveling.
- **Position Mode (PosHold/Loiter)**: Uses GPS to hold position. Essential for outdoor flying.
- **Return to Launch (RTL)**: A safety mode that brings the drone back to the takeoff point.
