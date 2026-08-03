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



## 3. Power / Battery Wiring

**Key finding:** USB-C power alone does NOT power the FC's 5V BEC output pad — confirmed by measuring only ~0.3V across 5V/G while on USB power. The BEC is driven from the battery input (Vbat), not USB VBUS.

*   If your FC sits on a 4-in-1 ESC stack: the battery plugs into the ESC's XT60/XT30 connector; the ESC feeds Vbat sense to the FC through the same signal cable used for motor outputs.
*   If bench-testing the bare FC: wire a battery pigtail directly — Battery+ → Vbat pad, Battery− → G pad (Vbat accepts 6–36V / 2–8S LiPo directly). Double-check polarity before connecting; there is no reverse-polarity protection.
*   Peripherals wired to the 5V pad (like the receiver) will not power up until the battery is connected — this explained the dead receiver LED earlier in this session.

## 4. ESC / Motor Wiring

For **4 individual ESCs** (non-4-in-1): connect each ESC's signal wire to S1–S4 respectively, matching each motor's physical position to the numbering shown in Vehicle Setup → Frame. ESC ground wires go to any G pad (shared/common ground); ESC power leads (+/-) go to the battery, not the FC.

For a **4-in-1 ESC**: it plugs directly into the FC via a matching JST-SH 1.0 8-pin connector/cable — this single connector carries S1–S4 plus power sensing.

Outputs are grouped for DShot: Group1 (S1/S2), Group2 (S3/S4), Group3 (S5/S6), Group4 (S9/S10), Group5 (S11) — all outputs sharing a group must use the same protocol (all DShot or all PWM).

## 5. Receiver Wiring — FrSky Archer Plus R8

This board's RC input only accepts serial protocols on UART2 — no raw PWM/PPM input is supported, so the receiver's SBUS output (not its 8 individual PWM channel ports) is what gets used.

<div class="glass-card rounded-2xl p-6 border border-slate-800 my-6 max-w-3xl mx-auto">
    <h3 class="text-lg font-bold text-slate-200 mb-6 text-center flex justify-center items-center">
        <i class="fa-solid fa-plug text-purple-400 mr-3"></i> Receiver Wiring Diagram
    </h3>
    
    <div class="flex flex-col md:flex-row items-center justify-between gap-4">
        
        <!-- FrSky Archer Plus R8 -->
        <div class="w-full md:w-5/12 bg-slate-900 border-2 border-slate-700 rounded-xl p-4 shadow-lg flex flex-col items-center">
            <h4 class="font-bold text-sky-400 mb-4 text-center">FrSky Archer Plus R8</h4>
            <div class="flex flex-col space-y-4 w-full">
                <div class="bg-slate-800 rounded p-2 flex justify-between items-center border border-sky-500/30">
                    <span class="text-xs text-slate-300 font-mono">SBUS OUT (signal)</span>
                    <div class="w-3 h-3 rounded-full bg-yellow-400 shadow-[0_0_8px_rgba(250,204,21,0.6)]"></div>
                </div>
                <div class="bg-slate-800 rounded p-2 flex justify-between items-center border border-red-500/30">
                    <span class="text-xs text-slate-300 font-mono">+ / VCC</span>
                    <div class="w-3 h-3 rounded-full bg-red-500 shadow-[0_0_8px_rgba(239,68,68,0.6)]"></div>
                </div>
                <div class="bg-slate-800 rounded p-2 flex justify-between items-center border border-slate-500/30">
                    <span class="text-xs text-slate-300 font-mono">− / GND</span>
                    <div class="w-3 h-3 rounded-full bg-black border border-slate-500 shadow-[0_0_8px_rgba(0,0,0,0.6)]"></div>
                </div>
            </div>
        </div>

        <!-- Connection Lines -->
        <div class="hidden md:flex flex-col justify-between h-32 w-2/12 space-y-8 relative px-2">
            <div class="w-full h-1 bg-yellow-400/50 flex items-center justify-center relative mt-2">
                <i class="fa-solid fa-arrow-right text-yellow-400 absolute text-xs"></i>
            </div>
            <div class="w-full h-1 bg-red-500/50 flex items-center justify-center relative">
                <i class="fa-solid fa-arrow-right text-red-500 absolute text-xs"></i>
            </div>
            <div class="w-full h-1 bg-slate-500/50 flex items-center justify-center relative mb-2">
                <i class="fa-solid fa-arrow-right text-slate-500 absolute text-xs"></i>
            </div>
        </div>

        <!-- Matek H7A3-SLIM FC -->
        <div class="w-full md:w-5/12 bg-slate-900 border-2 border-slate-700 rounded-xl p-4 shadow-lg flex flex-col items-center">
            <h4 class="font-bold text-purple-400 mb-4 text-center">Matek H7A3-SLIM FC</h4>
            <div class="flex flex-col space-y-4 w-full">
                <div class="bg-slate-800 rounded p-2 flex justify-start items-center border border-purple-500/30 gap-3">
                    <div class="w-3 h-3 rounded-full bg-yellow-400 shadow-[0_0_8px_rgba(250,204,21,0.6)]"></div>
                    <span class="text-xs text-slate-300 font-mono font-bold">Rx2</span>
                </div>
                <div class="bg-slate-800 rounded p-2 flex justify-start items-center border border-red-500/30 gap-3">
                    <div class="w-3 h-3 rounded-full bg-red-500 shadow-[0_0_8px_rgba(239,68,68,0.6)]"></div>
                    <span class="text-xs text-slate-300 font-mono font-bold">5V pad</span>
                </div>
                <div class="bg-slate-800 rounded p-2 flex justify-start items-center border border-slate-500/30 gap-3">
                    <div class="w-3 h-3 rounded-full bg-black border border-slate-500 shadow-[0_0_8px_rgba(0,0,0,0.6)]"></div>
                    <span class="text-xs text-slate-300 font-mono font-bold">G pad</span>
                </div>
            </div>
        </div>

    </div>
</div>

*   **SBUS IN** on the receiver is only for the redundancy feature (chaining a second receiver) — not used in a single-receiver setup.
*   After wiring, set `SERIAL2_OPTIONS = 3` in Parameters so ArduPilot correctly reads SBUS's inverted signal (`SERIAL2_PROTOCOL = 23` is already the default for RC input).
*   The receiver only powers up once the battery (not just USB) is connected, per section 3.

## 6. Binding the Receiver (FrSky X7s transmitter, ACCST D16)

1. Power off the receiver.
2. Hold the receiver's F/S (bind) button while powering it on — LED goes solid or flashes rapidly, indicating bind mode.
3. On the transmitter: Model Setup → Internal/External RF → select D16 mode → Bind.
4. Wait a few seconds — receiver LED turns solid, confirming a successful bind.
5. Power cycle both without holding any buttons — LED should go solid immediately, confirming the bind persisted.

*LED behavior reference: blinking red = powered but not bound / no signal. Solid = bound and receiving.*

## 7. Fixing Transmitter Channel Order (X7s, EdgeTX/OpenTX)

**Symptom hit in this session:** pushing the throttle stick moved the "Roll" value in QGC. 
**Cause:** the model's channel order was TAER (Throttle on channel 1) instead of the AETR order ArduPilot expects (Roll on channel 1).

The global "Default channel order" setting in Radio Setup only applies to newly created models — an existing model's order must be fixed directly in its Mixer page:

1. Select the model, press PAGE until reaching the Mixer screen (shows CH1–CH4 with sources like Thr/Ail/Ele/Rud).
2. Highlight the CH1 line, long-press ENTER → Move.
3. Move each channel until the order reads CH1: Ail, CH2: Ele, CH3: Thr, CH4: Rud (AETR).
4. Back in QGC, redo Radio Calibration so it re-learns the corrected channel positions.

*Alternative (FC-side, no transmitter changes): set RCMAP_ROLL / RCMAP_PITCH / RCMAP_THROTTLE / RCMAP_YAW parameters in QGC to match whatever channel numbers each function actually lands on.*
