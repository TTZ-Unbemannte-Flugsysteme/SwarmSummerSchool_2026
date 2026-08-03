# QGroundControl & Matek H7A3-SLIM Setup

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

## 1. Board & Firmware Identification

Connecting the board to QGroundControl via USB-C and reading the MAVLink Console boot log confirmed:

```text
MatekH7A3 00410019 3231510A 31313531
ChibiOS: 8fc176ac
ArduCopter V4.6.0-dev (d2c8bdf0)
```

This is a **Matek H7A3-SLIM** flight controller (STM32H7A3RIT6 MCU) running ArduCopter (ArduPilot) — not PX4. It has no built-in compass and no built-in current sensor.

## 2. Connecting to QGroundControl

1. Install QGroundControl from qgroundcontrol.com if not already installed.
2. Connect the flight controller via USB-C directly to the computer (not through a hub).
3. QGC auto-connects within a few seconds — connection icon (top-left) goes from "Not Ready" once a link is established.
4. Gear icon (Vehicle Setup) → Summary shows live Firmware Version, Vehicle Type, and Frame status.

![Flashing Firmware in QGroundControl](../assets/flashing.png)

## 3. ArduCopter Configuration Checklist

Do all of this connected via USB with props off, vehicle on a stand:

1. **Frame class & type** — Vehicle Setup → Frame. Must match physical motor layout exactly.
2. **Accelerometer calibration** — Vehicle Setup → Sensors → Accelerometer (6-position capture).
   <br>![Accelerometer Calibration](../assets/acc_cal.png)
3. **Compass calibration** — Vehicle Setup → Sensors → Compass (only if an external compass is added; this board has none built-in).
4. **Radio calibration** — Vehicle Setup → Radio (after channel order is fixed per section 7).
5. **Flight modes** — assign Stabilize / AltHold / Loiter / RTL to switch positions.
6. **Battery monitor & failsafes** — Vehicle Setup → Power (monitor type, cell count, voltage calibration) and → Safety (battery + RC-loss failsafe actions).
7. **ESC calibration** — only needed for standard PWM ESCs, not DShot.
8. **Motor direction test** — Vehicle Setup → Motors → Motor test, props off, confirm correct spin order/direction per Frame Type.
9. **Safety switch** — press/hold hardware safety button if present; confirm all pre-arm messages clear before arming.
10. **First flight** — Stabilize mode, brief hover, then AltHold hover 30s hands-off, then AutoTune via an assigned Aux switch.

## 4. Troubleshooting Notes From This Session

| Symptom | Cause / Fix |
| :--- | :--- |
| "PreArm: Battery 1 low voltage failsafe" despite battery showing charged | Battery monitor not calibrated, or no real battery connected (USB-only power) — configure Vehicle Setup → Power and connect an actual flight battery. |
| Receiver LED completely dark after wiring | FC powered by USB only — 5V BEC pad stays unpowered until a battery is connected via Vbat. |
| Throttle stick moves "Roll" field in QGC | Transmitter channel order (TAER) doesn't match ArduPilot's expected order (AETR) — fix via Mixer page or RCMAP parameters. |
| Need to bypass a specific pre-arm check (e.g. compass) for bench testing | QGC Parameters → search ARMING_CHECK → uncheck the specific check. Not recommended to leave disabled for actual GPS-mode flight. |

## 5. Optional: PX4 Simulation via Gazebo

Since this board runs ArduPilot (not PX4), trying PX4 itself is only practical via simulation, not on this hardware (no official PX4 target for this MCU/board). Covered separately if needed — see the ArduPilot+Gazebo section below instead, which matches your actual firmware.

ArduPilot + Gazebo SITL (for testing without touching hardware): clone ardupilot repo, run the Ubuntu prereqs script, install Gazebo + the ardupilot_gazebo plugin, then launch with:

```bash
sim_vehicle.py -v ArduCopter -f gazebo-iris --model JSON --map --console
```
