# Input Protection

The v1 schematic accepts external DC power at J1 and routes the positive supply through a fuse and a reverse-polarity protection stage before it reaches the regulator input. A bidirectional TVS diode is connected across the incoming supply rails.

## Components and arrangement

| Reference | Part/value shown | Role |
| --- | --- | --- |
| J1 | 177195-0004 | External power connector |
| F1 | 1812L075/24DR | Resettable input fuse in series with the positive supply |
| D4 | SMBJ18CA | Bidirectional TVS across the input supply rails |
| Q1 | AO4407A, 30 V P-channel MOSFET | Reverse-polarity protection |
| RP, RG | 100 kΩ each | MOSFET gate-bias network |
| CIN | 22 µF | Bulk capacitance at the regulator input |

The fuse limits sustained overcurrent, while D4 shunts short-duration voltage transients across the supply rails. Q1 is arranged as a high-side reverse-polarity protection element; its gate-bias resistors establish the gate drive needed for correct-polarity operation and keep the device in its intended state when input conditions change. The protection stage is intended for the 12 V electrical environment used in FRC robots.

## Reverse-polarity protection losses

The gate-control network uses two 100 kΩ resistors in series across the 12 V input. Its current and total dissipation are:

`I = 12 V / (100 kΩ + 100 kΩ) = 60 µA`

`P = 12 V × 60 µA = 0.72 mW`

Each resistor dissipates approximately 0.36 mW.

Q1's conduction loss is set by its on-resistance and the input current through it:

`P_Q1 = I_IN² × R_DS(on)`

The converter's **0.6 A maximum output current is specified at 5 V**; it is not the current through Q1. Assuming 90% converter efficiency at 12 V input and full output load:

`I_IN ≈ (5 V × 0.6 A) / (12 V × 0.90) ≈ 0.278 A`

With `R_DS(on) = 17 mΩ`, Q1's conduction loss is approximately:

`P_Q1 = I_IN² × R_DS(on) ≈ (0.278 A)² × 0.017 Ω ≈ 1.31 mW`

This estimate excludes switching and transient losses; actual on-resistance varies with gate drive and junction temperature.

## Operating limits

The SMBJ18CA has an 18 V working-standoff voltage and begins avalanche breakdown at approximately 20 V. Under its specified pulse conditions, its clamping voltage may reach approximately 29 V. This transient clamp is below the LMR14006's 40 V maximum input rating and is selected to protect the regulator from input transients in the intended FRC application. 

In an FRC robot, the nominal 12 V battery bus varies with battery state and load but is normally below the TVS's 18 V standoff. Brief spikes can occur during switching or changes in motor load; the TVS conducts on sufficiently high spikes and may let the rail reach about 29 V during a rated pulse. It is not intended to absorb sustained overvoltage or unlimited surge energy.


F1 is a resettable fuse rather than a precision current limiter. Its hold and trip behavior varies with ambient temperature and fault conditions. Q1's voltage stress, dissipation, and gate drive are bounded by the AO4407A ratings and the applied input conditions.



The protection network reduces risk from reverse-polarity connection, overcurrent, and transient events within the components' ratings. It does not protect against arbitrary sustained overvoltage or unlimited surge energy.
