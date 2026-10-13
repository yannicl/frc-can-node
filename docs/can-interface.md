# CAN Bus Interface

The v1 schematic uses a TI **SN65HVD231DR** 3.3 V CAN transceiver (U3) to connect the XIAO's logic-level transmit and receive signals to the differential CANH and CANL bus.

## Circuit details

| Reference | Part/value shown | Function |
| --- | --- | --- |
| U3 | SN65HVD231DR | CAN physical-layer transceiver |
| D1 | PESD1CAN,215 | CAN-line ESD protection device |
| R5, R6 | 33 Ω each | Series resistors on the transceiver's logic-side signals |
| C2 | 100 nF | Local transceiver supply decoupling |
| SW1 | DS-02-R-T | Enables/disables the optional bus termination |
| R3, R4 | 60.4 Ω each | Split-termination resistors |
| C1 | 4.7 nF | Split-termination midpoint capacitor to ground |

U3 is powered from V3.3. Its RS pin is tied low in the schematic, selecting the transceiver's high-speed operating mode. The 33 Ω resistors are between the transceiver logic pins and the MCU signals; they are not CANH/CANL termination resistors. D1 is connected at the CAN interface for line-transient/ESD protection. C2 should be placed close to the transceiver supply and ground pins.

## Optional termination

SW1 connects the two CAN lines to a split termination made from R3 and R4. When enabled, the two 60.4 Ω resistors provide approximately **120.8 Ω differential termination** between CANH and CANL, with C1 bypassing their midpoint to ground for high-frequency common-mode noise. When disabled, this board does not provide that termination.

Only terminate a CAN bus at its two physical ends, as required by the network topology. Do not enable termination on every node; extra termination loads the bus and can prevent reliable communication.

## Capabilities and limits

The SN65HVD231 is a 3.3 V high-speed CAN physical-layer transceiver. The RS pin is low in this implementation. Supported signaling rates and electrical limits are defined by the transceiver datasheet.

The transceiver provides the physical interface only; CAN protocol behavior, message IDs, bitrate configuration, and application compatibility are determined by firmware and the connected network. The schematic implements a conventional high-speed CAN interface and does not specify CAN FD operation.

The PESD1CAN device and switchable termination provide line protection and bus termination respectively, within their component ratings and network topology. They do not provide protection from arbitrary wiring faults or unlimited surge energy.
