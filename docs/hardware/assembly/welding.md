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

## Power Distribution Board (PDB) Soldering & Assembly Log

![PDB Soldering Workstation](../../assets/Screenshot%202026-07-29%20at%2014.06.17.jpg)

### 4.1 XT60 Main Battery Lead & ESC Soldering Technique

**Thermal Mass Preparation:** Temperature-controlled soldering station set to 380°C - 400°C to compensate for the significant copper plane heat dissipation on the F450 board.

**Pre-Tinning Copper Pads & Wires:**

- Both the heavy-gauge 12AWG silicone XT60 battery wires and high-current PCB contact pads are pre-tinned with high-grade rosin-core solder prior to joining.
- Fine solder wire is fed directly onto the heated joint to establish a solid chemical bond.

![XT60 Battery Cable Soldering Detail](../../assets/Screenshot%202026-07-29%20at%2014.06.34.jpg)

**Polarity Verification:**

- **Positive Cable (Red):** Soldered directly to the central pad marked `+`.
- **Negative Cable (Black):** Soldered to the opposing pad marked `-`.

**ESC Power Cables:** 4x 30A ESC DC supply wires pre-tinned and attached to designated corner arm power rails.
