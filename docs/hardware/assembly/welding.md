# Welding & Soldering Guide

Proper welding/soldering is critical for the safety and reliability of your drone. Poor joints can lead to mid-air failures.

## Safety First

> [!WARNING]
> Soldering irons get extremely hot (typically 350°C - 400°C). Always place the iron in its stand when not in use. Work in a well-ventilated area to avoid inhaling flux fumes.

## Required Equipment

- **Soldering Iron**: Temperature-controlled is highly recommended.
- **Solder**: 60/40 Rosin-core (or lead-free equivalent if required by regulations).
- **Flux Pen/Paste**: For cleaning and aiding solder flow.
- **Helping Hands**: To hold wires and connectors while soldering.

## Best Practices

1. **Tin the wires and pads**: Apply a small amount of solder to the wire tip and the PCB pad *before* joining them.
2. **Heat the joint, not the solder**: Touch the iron to both the wire and the pad simultaneously, then feed solder into the joint.
3. **Inspect the joint**: A good solder joint should look shiny (if using leaded solder) and have a smooth, concave fillet. It should not look like a dull "blob" (cold joint).

## Specific Tasks

### ESCs to Power Distribution Board (PDB)
- Ensure correct polarity (Red to `+`, Black to `-`).
- Use ample heat for the thick gauge wires.

### Motor Wires to ESCs
- Often these are soldered directly or use bullet connectors. 
- If soldering directly, wait to shrink-wrap them until you have verified the motor spin direction (you can swap any two wires to reverse the motor direction).
