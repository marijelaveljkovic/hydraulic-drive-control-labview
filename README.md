# Hydraulic Drive Control – LabVIEW Real-Time

Control system for a hydraulic drive with three cylinders, developed in LabVIEW on an NI CompactRIO controller, with a SCADA interface on a host PC.

University project for the course *Real-Time Control Algorithms*, Faculty of Technical Sciences, University of Novi Sad.

## Architecture
| Component | Runs on | Role |
|---|---|---|
| `UpravljanjeHidraulicnomPumpom.vi` | CompactRIO | Main control logic |
| `scada.vi` | Host PC | Operator interface |

The controller and the SCADA interface communicate through **network-published shared variables**.

## Control logic
The control program is implemented as a **state machine** with the states *System On*, *System Off*, *Left*, *Centre*, *Right* and *Emergency Off*.

- **Edge detection** on pushbuttons, so each command is handled as a one-time event
- **Controlled shutdown:** System Off stops the actuators only after the current stroke is completed
- **Emergency Off** with fault indication and fault reset
- **Status indication** with signal lamps for system state and cylinder positions

## I/O map
| Input | Signal | Output | Signal |
|---|---|---|---|
| DI0 | S1 – System On | DO0 | H1 – System On |
| DI1 | S2 – System Off | DO1 | H2 – Cylinder retracted |
| DI2 | S3 – Retract cylinder | DO2 | H3 – Intermediate position |
| DI3 | S4 – Intermediate position | DO3 | H4 – Cylinder extended |
| DI4 | S5 – Extend cylinder | DO4 | H5 – Fault |
| DI5 | S6 – Emergency Off | DO9 | Y1 – Extend cylinder 1 |
| DI8–DI10 | B1–B3 – Cylinder 1 back / centre / forward | DO10 | Y2 – Retract cylinder 1 |
| DI11–DI12 | B4–B5 – Cylinder 2 back / forward | DO11 | Y3 – Extend cylinder 2 |
| DI13–DI14 | B6–B7 – Cylinder 3 back / forward | DO12 | Y4 – Extend cylinder 3 |

## Tools
LabVIEW 2014 with the Real-Time Module · NI CompactRIO

## Documentation
- [Project report (Serbian)](docs/project-report-sr.pdf)
- [Presentation (Serbian)](docs/presentation-sr.pdf)

