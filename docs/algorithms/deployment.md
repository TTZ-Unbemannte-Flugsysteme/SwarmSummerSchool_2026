# Real Hardware Deployment

Once algorithms have been thoroughly tested in simulation, you can deploy them to the physical drone.

> [!CAUTION]
> Always remove the propellers when testing new software on the bench for the first time.

## 1. Bench Testing

1. Connect the battery (propellers removed).
2. SSH into the companion computer.
3. Start your algorithm.
4. Arm the drone and observe the motor responses (they should spin up predictably).
5. Disarm.

## 2. Field Testing

### Pre-flight Checks
- Ensure battery is fully charged.
- Verify GPS lock (LED indicators on flight controller or via QGroundControl).
- Check weather conditions (avoid high winds).

### Execution
1. Take off manually in Position mode to verify the drone is physically sound and the tune is stable.
2. Switch to **Offboard / Guided mode** (the mode where the companion computer takes control).
3. Monitor the flight. Have your finger ready on the RC transmitter's **Flight Mode switch** to immediately switch back to Manual/Position mode if the drone behaves erratically.

## 3. Data Logging and Analysis

After the flight:
- Download the `.ulog` (PX4) or `.bin` (ArduPilot) files from the flight controller via QGroundControl.
- Analyze the logs using tools like [Flight Review](https://logs.px4.io/) to check vibration levels, PID performance, and CPU load.
- Review ROS bags (if recorded on the companion computer) to analyze algorithm performance.
