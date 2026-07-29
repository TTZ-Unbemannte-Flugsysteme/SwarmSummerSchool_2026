# Simulation Testing

Before flying real hardware, you must test your algorithms in a simulated environment to prevent crashes and verify logic safely.

## Simulator Setup

We recommend using **Gazebo** (or Gazebo Classic depending on your ROS version) paired with Software In The Loop (SITL).

### PX4 SITL Setup
1. Clone the PX4 Autopilot repository.
2. Run the simulation environment:
   ```bash
   make px4_sitl gazebo
   ```
3. You should see a 3D environment open with a drone model.

## Running Algorithms

1. **Connect your Algorithm to the Simulator**: Ensure your ROS nodes or Python scripts (using MAVSDK/DroneKit) are pointing to the simulator's IP address (typically `localhost` or `127.0.0.1:14540`).
2. **Takeoff Sequence**: Test basic commands like arming, taking off, and holding a hover.
3. **Complex Logic**: Execute your specific Swarm or navigation logic. Monitor the console output and the drone's behavior in Gazebo.

## Verification Checklist

Before moving to real hardware, ensure:
- [ ] The algorithm does not send conflicting commands.
- [ ] Emergency stop / Land commands work reliably.
- [ ] The drone correctly handles losing communication (failsafe testing).
