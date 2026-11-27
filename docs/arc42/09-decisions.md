# 9. Architecture Decisions

> Exercises: **E02** (decision log), **E05** (first ADR), **E07**, **E10** (more ADRs and interdependencies).
> Significant decisions get a full ADR in `docs/adr/`. Smaller ones get a line in the log below.

## 9.1 Decision log

Reversibility: **cheap** = swap the part, little or no code change; **costly** = rework wiring, drivers or mechanics; **redesign** = affects many building blocks or the PCB. Reversibility grows once the PCB exists (D-8).

| ID | Decision | Date | Status | Why (reviewed in E02) | Reversibility | ADR |
|---|---|---|---|---|---|---|
| D-1 | MCU: ESP32-S3 | 2026-11 | accepted (before architecture work) | Fast enough for the control computations; the needed peripherals on one chip (motor-control PWM, pulse counters for the encoders, precise timers, USB/JTAG). | **redesign**: new PCB, and all firmware tied to ESP-IDF (D-10) | – |
| D-2 | Motors: N20 12 V gear motors with Hall encoders (not steppers, not JGA25-370) | 2026-11 | accepted (before architecture work) | Slightly underpowered on 2S but sufficient for a first attempt (torque and speed estimate, AS-4). | **costly**: new parts, long delivery; a stronger motor (e.g. ~1.8 A stall) would also need a different driver (D-3) | – |
| D-3 | Motor driver: TB6612FNG | 2026-11 | accepted; reviewed in E02 | Drives both motors from one chip; 1.2 A continuous per channel covers the N20 (tight margin, AS-5); supply limit 13.5 V leaves room for 3S. Main reason vs. the L298N: much lower voltage drop. L298N: 1.8–3.2 V at 1 A, up to 4.9 V at 2 A ([ST datasheet](https://www.st.com/resource/en/datasheet/l298.pdf)), which would leave little for the motors on an empty 2S pack (6.4 V). TB6612FNG: ~0.5 Ω on-resistance, ~0.7 V at 1 A ([Toshiba datasheet](https://toshiba.semicon-storage.com/info/TB6612FNG_datasheet_en_20141001.pdf?did=10660&prodName=TB6612FNG)). | **costly** if rewiring is needed. SW: small, if motor control sits behind an interface (direction pins + PWM may differ for another driver) | TODO(E10) |
| D-4 | Power: 2S Li-ion + BMS, 3S optional later | 2026-11 | accepted (parts on hand) | Cost: parts on hand, only a connector needed. Other parts were chosen to tolerate 3S. | **cheap** (but see step 5 questions on 3S) | – |
| D-5 | Buck converter: MP1584EN | 2026-11 | accepted (ordered) | Readily available, inexpensive, enough current for all logic (3 A, to verify for the module). | **cheap**: may need a mounting adapter | – |
| D-6 | Power sensing: INA219 | 2026-11 | accepted | Cheap; measures voltage and current together. | **cheap**: rewiring for another pinout; SW changes limited (I²C) | – |
| D-7 | IMU: MPU-6050, replace if needed | 2026-11 | accepted | Well known, cheap; only one rotation axis (pitch) is needed. | **cheap** in HW (wiring adapter). SW: more effort if the data format or protocol changes, unless the IMU is hidden behind an interface (E06) | TODO(E10) |
| D-8 | Custom 2-layer PCB only after the prototype works | 2026-11 | accepted | A PCB gives clean signals and a compact, mountable layout, but takes time to design and manufacture; doing it after the prototype avoids re-spins. | **cheap** as a sequencing decision. Once the PCB exists, it raises the cost of reversing D-1, D-3, D-6, D-7 (and D-2 indirectly); a new design means another manufacturing and shipping round | – |
| D-9 | micro-ROS on the MCU (instead of an SBC with ROS 2 on the robot) | 2026-11 | **open**: micro-ROS vs. custom protocol | | | ADR-0001 (E05) |
| D-10 | Firmware framework: ESP-IDF directly, in C++ (not Arduino-ESP32) | 2026-11-26 | accepted (E02), confirmed after reading AS-12's sources; fallback Arduino-ESP32 (trigger: TC-10) | Expected to give the fine control needed for precise, uninterrupted control-loop timing. Trade-off: slower start (OC-3, ~4 h/week). Based on earlier experience of having to rebuild a library because configuration options weren't exposed. Cheap to try out first (fallback trigger). Note: Arduino-ESP32 can also call ESP-IDF/FreeRTOS APIs; which configuration options it lacks is to verify. | **costly** once drivers are written | – |
| D-12 | Wheels: existing laser-printer rollers or 3D-printed wheels, with printed axle adapters | 2026-11 | accepted | Parts on hand; adapters are little effort to design in hard plastic. TPU wheels or tyres are a bit more effort, but the printer can print multiple materials. | **cheap** | – |
| D-11 | Ground station platform | 2026-11-25 | **open**: preference web browser (also usable from a phone) → E05. v1 runs on the home network only; demos without it (e.g. the ESP32 as its own access point) → v2. | | | – |

## 9.2 Interdependencies between decisions

TODO(E10)
