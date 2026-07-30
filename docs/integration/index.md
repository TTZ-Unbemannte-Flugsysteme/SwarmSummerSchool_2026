# Integration Overview

Welcome to the Integration section. Here we will document the processes for combining hardware sub-systems and software configurations to ensure the drone is fully operational and ready for flight testing.

## Voltage Verification
![Check Voltage](../assets/CheckVolt.png)

## Motor Spin & Direction Test
![Check Motor](../assets/checkMotor.png)

## Putting Everything Together

Once the individual components have been tested (Voltage verified, Motors spinning correctly), the final integration step involves:

1. **Physical Securing**: Ensure all zip-ties are snipped flush, velcro straps are tightened around the battery, and the flight controller stack is firmly mounted on its vibration dampeners.
2. **Peripheral Connections**: Double-check that the GPS/Compass, Receiver, and Companion Computer (Raspberry Pi) are plugged into their designated UART/I2C ports securely.
3. **Telemetry & Communication Test**: Power up the drone using the 4S LiPo and verify that MAVLink telemetry is successfully transmitting to your Ground Control Station (e.g., Mission Planner).
4. **Final Center of Gravity (CoG) Check**: Lift the drone by the center of the frame and ensure it balances evenly. Adjust the battery position forward or backward if it tilts heavily.

## RC XT7 Radio Connection & Binding

To manually pilot or take over the drone during flight tests, you must bind your **RC XT7** transmitter to the onboard receiver (e.g., FrSky SBUS receiver).

### 1. Hardware Connection
*   **Signal:** Ensure the receiver's SBUS/Signal out pin is connected to the **RX6 pad** on the Matek H743-SLIM flight controller.
*   **Power:** Ensure the receiver's 5V and GND pins are connected to a steady **5V pad** and **GND pad** on the flight controller.

### 2. Binding Process
*   Turn on your **RC XT7** transmitter and navigate to the Model Setup menu to put it into **Bind Mode** (it will typically start beeping).
*   On the drone, hold down the tiny **Bind button** on the receiver while simultaneously plugging in the drone's 4S LiPo battery.
*   The status LEDs on the receiver will flash to indicate a successful bind. Exit bind mode on the RC XT7 and power cycle the drone.

### 3. Software Calibration (Mission Planner)
Once bound, the stick movements must be calibrated in ArduPilot:
1. Connect the flight controller to your computer via USB and open **Mission Planner**.
2. Navigate to **Setup -> Mandatory Hardware -> Radio Calibration**.
3. Turn on the RC XT7. As you move the joysticks, you should see the green bars reacting on screen. 
4. Click **Calibrate Radio** and move all sticks and switches to their maximum physical extents to set the endpoints for Pitch, Roll, Yaw, and Throttle.
