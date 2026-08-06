# Bind with Remote Control

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

## Interactive Setup Simulator

Practice configuring your transmitter inputs, the mixer, and verifying them in Betaflight before trying it on real hardware.

<iframe src="simulator.html" width="100%" height="800px" style="border: none; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); margin-top: 20px;"></iframe>
