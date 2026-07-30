# Nipping & Wiring Guide

Proper wire management and preparation are essential for a clean and reliable drone build.

## Wire Stripping and Nipping

![Nipping Wiring](../../assets/Nipping%20Wiring.png)

1. **Measure Twice, Cut Once**: Plan the routing of your wires before cutting them. Leave a small amount of slack to prevent tension during flight vibrations, but not so much that wires can get caught in propellers.
2. **Nipping**: Use flush cutters (nippers) to make clean, straight cuts on wires and zip ties.
3. **Stripping**: Use wire strippers matched to the gauge (AWG) of the wire. Typically, strip about 3-5mm of insulation for soldering to PDB pads or connectors.

## Cable Management

> [!TIP]
> Keep signal wires (e.g., receiver, GPS, I2C) away from high-current power wires (ESC, Battery) to minimize electromagnetic interference (EMI).

- **Zip Ties**: Use small zip ties to secure ESCs to the arms and bundle wires together. Use flush cutters to snip the excess tail of the zip tie completely flat so it doesn't leave a sharp edge.
- **Heat Shrink**: Cover all exposed solder joints with heat shrink tubing to prevent short circuits.
- **Braided Sleeving** (Optional): Protects wires from abrasion against the carbon fiber frame edges.

## Connectors

Familiarize yourself with common drone connectors:
- **XT60 / XT90**: Main battery connectors.
- **JST / DuPont**: Often used for low-power peripherals and receiver signals.
- **JST-GH**: Commonly used on modern Pixhawk flight controllers for GPS, Telemetry, and I2C peripherals. Be gentle when plugging/unplugging these.
