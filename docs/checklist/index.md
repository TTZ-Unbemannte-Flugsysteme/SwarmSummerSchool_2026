# End-to-End Build & Flight Checklist

This checklist provides a linear, chronological guide from bare components to your very first flight. Use this as your master guide to ensure no steps are skipped during the integration process!

---

## Phase 1: Hardware Assembly
- [ ] **Frame Assembly**: Assemble the F450 frame arms and bottom plate ([Guide](../hardware/assembly/frame.md)).
- [ ] **Motor Mounting**: Secure the motors to the frame arms, ensuring cables route cleanly towards the center ([Guide](../hardware/assembly/motors.md)).
- [ ] **Welding & Power**: Solder the battery XT60/XT90 connector and ESC power cables to the Power Distribution Board (PDB) ([Guide](../hardware/assembly/welding.md)).
- [ ] **Nipping & Wiring**: Trim excess cables, secure ESCs to the arms, and wire ESC signal lines to the Flight Controller ([Guide](../hardware/assembly/nipping.md)).
- [ ] **Flight Controller Mounting**: Mount the Matek H7A3-SLIM securely on its vibration dampeners, paying attention to the forward arrow.

## Phase 2: Wiring & Integration
- [ ] **Initial Power Check**: Connect the battery to the PDB and use a multimeter to verify the 5V and 9V BEC rails are outputting correctly *before* connecting peripherals.
- [ ] **Connect Peripherals**: Plug in the GPS (UART3), Compass (I2C1), and RC Receiver to their designated ports on the Flight Controller ([Connection Guide](../integration/connection_guide.md)).
- [ ] **Companion Computer**: If using a Raspberry Pi, wire it to the dedicated telemetry UART and step-down power supply.

## Phase 3: Software & Flashing
- [ ] **Install Ground Control**: Download and open Mission Planner or QGroundControl on your laptop.
- [ ] **Flash Firmware**: Connect the flight controller via USB (do not plug in the battery) and flash the latest **ArduCopter** firmware.
- [ ] **Frame Configuration**: In your Ground Control Station, set the Frame Class (Quad) and Frame Type (X) to match the physical drone.

## Phase 4: Mandatory Calibration
- [ ] **AHRS Orientation**: If the flight controller is mounted upside down, navigate to the Autopilot Rotation menu and set `AHRS_ORIENTATION` to `8` (Roll180) *before* accelerometer calibration.
- [ ] **Accelerometer Calibration**: Perform the 6-position accelerometer calibration.
- [ ] **Compass Calibration**: Wait for a 3D GPS fix (outdoors or near a window), ensure the external compass is detected, and perform the MagFit rotation calibration.
- [ ] **Radio Bind & Calibration**: Bind the RC transmitter to the receiver, then perform Radio Calibration in the software to set stick endpoints and verify channel mapping (AETR vs TAER).

## Phase 5: Pre-Flight Testing
- [ ] **ESC Calibration**: (Skip if using DShot). For standard PWM ESCs, perform the throttle-max to throttle-min calibration sequence.
- [ ] **Motor Spin Test**: **WITH PROPELLERS OFF**, use the Motor Test tab to verify each motor spins in the correct direction (A, B, C, D) corresponding to your frame layout.
- [ ] **Flight Modes Setup**: Assign your transmitter switches to Stabilize, AltHold, and RTL (Return to Launch).
- [ ] **Failsafe Setup**: Configure Battery and RC-Loss failsafes to trigger an RTL or Land sequence.

## Phase 6: Final Flight Prep
- [ ] **Center of Gravity (CoG)**: Lift the drone by the exact center point. Adjust the battery forward or backward until it balances perfectly level.
- [ ] **Install Propellers**: **(Absolute Last Step)** Match the CW and CCW propellers to the correct motors and tighten the nuts securely.
- [ ] **First Flight**: Take the drone to an open, safe area. Arm in Stabilize mode, perform a brief hover to verify control, then switch to AltHold.
