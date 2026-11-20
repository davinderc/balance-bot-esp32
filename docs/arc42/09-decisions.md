# 9. Architecture Decisions

> Exercises: **E02** (decision log), **E05** (first ADR), **E07**, **E10** (more ADRs and interdependencies).
> Significant decisions get a full ADR in `docs/adr/`. Smaller ones get a line in the log below.

## 9.1 Decision log

| ID | Decision | Date | Status | Reversibility | ADR |
|---|---|---|---|---|---|
| D-1 | MCU: ESP32-S3 | 2026-11 | accepted (before architecture work) | TODO(E02) | – |
| D-2 | Motors: N20 12 V gear motors with Hall encoders (not steppers, not JGA25-370) | 2026-11 | accepted (before architecture work) | TODO(E02) | – |
| D-3 | Motor driver: TB6612FNG | 2026-11 | accepted **without review**, to be reviewed in E02 | TODO(E02) | TODO(E10) |
| D-4 | Power: 2S Li-ion + BMS, 3S optional later | 2026-11 | accepted (parts on hand) | TODO(E02) | – |
| D-5 | Buck converter: MP1584EN | 2026-11 | accepted (ordered) | TODO(E02) | – |
| D-6 | Power sensing: INA219 | 2026-11 | accepted | TODO(E02) | – |
| D-7 | IMU: MPU-6050, replace if needed | 2026-11 | accepted | TODO(E02) | TODO(E10) |
| D-8 | Custom 2-layer PCB only after the prototype works | 2026-11 | accepted | – | – |
| D-9 | micro-ROS on the MCU (instead of an SBC with ROS 2 on the robot) | 2026-11 | **open**: micro-ROS vs. custom protocol | | ADR-0001 (E05) |

## 9.2 Interdependencies between decisions

TODO(E10)
