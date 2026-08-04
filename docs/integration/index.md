# Integration Overview

<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
    .glass-card {
        background: rgba(15, 23, 42, 0.75);
        backdrop-filter: blur(12px);
        border: 1px solid rgba(255, 255, 255, 0.08);
        box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
    }
</style>

Welcome to the Integration section. Here we will document the processes for combining hardware sub-systems and software configurations to ensure the drone is fully operational and ready for flight testing.

[**See full steps here**](connection_guide.md)

## Putting Everything Together

Once the individual components have been tested (Voltage verified, Motors spinning correctly), the final integration step involves:

1. **Physical Securing**: Ensure all zip-ties are snipped flush, velcro straps are tightened around the battery, and the flight controller stack is firmly mounted on its vibration dampeners.
2. **Peripheral Connections**: Double-check that the GPS/Compass, Receiver, and Companion Computer (Raspberry Pi) are plugged into their designated UART/I2C ports securely.
3. **Telemetry & Communication Test**: Power up the drone using the 4S LiPo and verify that MAVLink telemetry is successfully transmitting to your Ground Control Station (e.g., Mission Planner).
4. **Final Center of Gravity (CoG) Check**: Lift the drone by the center of the frame and ensure it balances evenly. Adjust the battery position forward or backward if it tilts heavily.


## Voltage Verification
![Check Voltage](../assets/CheckVolt.png)

## Motor Spin & Direction Test
![Check Motor](../assets/checkMotor.png)


## Binding the Receiver (FrSky X7s / RC XT7)

1. Power off the receiver.
2. Hold the receiver's F/S (bind) button while powering it on — LED goes solid or flashes rapidly, indicating bind mode.
3. On the transmitter: Model Setup → Internal/External RF → select D16 mode → Bind.
4. Wait a few seconds — receiver LED turns solid, confirming a successful bind.
5. Power cycle both without holding any buttons — LED should go solid immediately, confirming the bind persisted.

*LED behavior reference: blinking red = powered but not bound / no signal. Solid = bound and receiving.*

## Fixing Transmitter Channel Order

**Symptom hit in this session:** pushing the throttle stick moved the "Roll" value in QGC. 
**Cause:** the model's channel order was TAER (Throttle on channel 1) instead of the AETR order ArduPilot expects (Roll on channel 1).

The global "Default channel order" setting in Radio Setup only applies to newly created models — an existing model's order must be fixed directly in its Mixer page:

1. Select the model, press PAGE until reaching the Mixer screen (shows CH1–CH4 with sources like Thr/Ail/Ele/Rud).
2. Highlight the CH1 line, long-press ENTER → Move.
3. Move each channel until the order reads CH1: Ail, CH2: Ele, CH3: Thr, CH4: Rud (AETR).
4. Back in QGC, redo Radio Calibration so it re-learns the corrected channel positions.

*Alternative (FC-side, no transmitter changes): set RCMAP_ROLL / RCMAP_PITCH / RCMAP_THROTTLE / RCMAP_YAW parameters in QGC to match whatever channel numbers each function actually lands on.*
