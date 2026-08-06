# Real Hardware Deployment

Once algorithms have been thoroughly tested in simulation, you can deploy them to the physical drone.

!!! caution
    Always remove the propellers when testing new software on the bench for the first time.

## 1. Bench Testing

1. Connect the battery (propellers removed).
2. SSH into the companion computer.
3. Start your algorithm.
4. Arm the drone and observe the motor responses (they should spin up predictably).
5. Disarm.

## 2. Field Testing

### Pre-flight Checks
- Ensure battery is fully charged.
- Verify GPS lock (LED indicators on flight controller or via Mission Planner).
- Check weather conditions (avoid high winds).
- **RC Transmitter**: Ensure you are using the **RC XT7** controller for the flight test.

### Execution
1. Take off manually in Loiter mode to verify the drone is physically sound and the tune is stable.
2. Switch to **Guided mode** (the mode where the companion computer takes control).
3. Monitor the flight. Have your finger ready on the RC XT7's **Flight Mode switch** to immediately switch back to manual control if the drone behaves erratically.

## 3. Data Logging and Analysis

After the flight:
- Download the `.bin` log files from the flight controller via Mission Planner.
- Analyze the logs to check vibration levels, PID performance, and CPU load.
- Review ROS bags (if recorded on the companion computer) to analyze algorithm performance.
