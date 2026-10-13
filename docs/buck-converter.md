# 5 V Buck Converter

U1, marked **LMR14006XDDCR** in the v1 schematic, is configured as an asynchronous step-down converter. It converts the protected input supply to the board's **5 V** rail, which powers the XIAO module and the WS2812B LED chain.

The support-component values follow the LMR14006 datasheet design guidance. The output stage is designed to supply **0.6 A** at the nominal 5 V rail. The board has been prototyped and checked.

The regulator IC itself is rated for input voltages up to 40 V and can operate with an input as low than 5 V, so the buck stage accommodates the expected variation in an FRC battery supply. This IC rating is not the board's input rating: the board's input-protection circuitry is designed for a maximum continuous input of 18 V. Do not treat inputs above 18 V as supported for continuous board operation.



## Support components shown

| Reference | Value/part shown | Function in the converter |
| --- | --- | --- |
| CIN | 22 µF | Input bulk capacitor at VIN |
| CBOT | 100 nF | Bootstrap capacitor between BOOT and SW |
| D2 | SS14_C83852 | Schottky catch diode for the asynchronous switching stage |
| L1 | 10 µH | Output inductor |
| COUT1, COUT2 | 22 µF each | Output filtering on the 5 V rail |
| R1 | 54.9 kΩ | Upper feedback-divider resistor from output to FB |
| R2 | 10 kΩ | Lower feedback-divider resistor from FB to ground |

When the internal switch turns off, D2 provides the inductor-current path. L1 and the output capacitors smooth the switched waveform. R1 and R2 feed a scaled version of the output to FB to regulate the nominal 5 V output. The schematic also shows U1's enable tied to the input supply.

## Component and operating limits

The switching-current loop comprises the input capacitor, U1, and D2; the SW node is the converter's high-voltage switching node. The feedback divider senses the 5 V output and should be routed away from the SW node, following the regulator manufacturer's layout guidance.

The effective capacitance depends on capacitor dielectric and DC bias. D2's reverse-voltage, current, and thermal ratings, and L1's saturation current, RMS rating, and DCR, bound operation under input and load conditions. The board's operating range and thermal capability are therefore determined by the complete component set and PCB implementation, not by the regulator IC ratings alone.
