# 2. Architecture Constraints

> Constraints limit the freedom of design. Unlike requirements, they are not up for negotiation, at least for now.
> Exercise: **E02**. Every constraint needs a **reason or source**. Mark unverified datasheet figures "to verify".

## 2.1 Technical constraints (hardware, chosen 2026-11, before architecture work started)

| ID | Constraint | Reason (as recorded) | Reversibility | Notes / to verify (E02) |
|---|---|---|---|---|
| TC-1 | MCU: **ESP32-S3** (dev board "ESP32-S3-DEV-KIT-N8R8": 8 MB flash, 8 MB PSRAM) | Hardware peripherals for quadrature encoders, fast floating-point maths, 2 cores (control loop on one, comms and telemetry on the other), 36+ GPIOs, native USB-OTG and JTAG debugging, vector instructions for later ML | TODO(E02) | Target loop rate 200–500 Hz. Which peripheral counts the encoders (PCNT?) and which generates PWM (MCPWM or LEDC)? Verify in the datasheet. |
| TC-2 | Motors: **N20 micro gear motors, 12 V, ~200 rpm no-load**, with AB (quadrature) magnetic Hall encoders | Lower current than steppers; cheaper than JGA25-370 | TODO(E02) | Rated at 12 V but supplied from 2S (see TC-4): effect on speed and torque headroom? Encoder counts per wheel revolution? Gearbox backlash? |
| TC-3 | Motor driver: **TB6612FNG** (dual H-bridge) | Suggested in the hardware session as more efficient and cooler than the L298N; **taken over without detailed review** | TODO(E02) | Motor supply voltage limit vs. a 3S upgrade? Continuous and peak current per channel vs. N20 stall current? |
| TC-4 | Power: **2S Li-ion 18650 or 21700** (21700 from an old power bank) with BMS; maybe 3S later | Parts already on hand; charging with an existing hobby charger | TODO(E02) | Voltage range from empty to full? Low-voltage cutoff by the BMS or in firmware? |
| TC-5 | Logic supply: **MP1584EN buck module** (from Eckstein) | Small, enough current for the logic | TODO(E02) | Output voltage set before connecting? Which dev-board power pin is fed? |
| TC-6 | Current/power sensing: **INA219** (I²C) | Energy data for comparing control algorithms | TODO(E02) | Measures which rail (battery or motor)? Shunt range? |
| TC-7 | IMU: **MPU-6050** (I²C, accelerometer and gyroscope) | Well known, cheap, enough to start; can be replaced later | TODO(E02) | Production status and clone quality? This is a reason to put the IMU behind an abstraction (see E06). |
| TC-8 | Wheels: laser-printer rollers (with printed adapters) or 3D-printed wheels | Parts on hand, good grip | TODO(E02) | Diameter → speed and torque at the wheel. |
| TC-9 | PCB: **2-layer custom PCB, later**, once the breadboard/prototype works | Cost; avoid re-spins | TODO(E02) | |
| TC-10 | Toolchain / framework | TODO(E02): ESP-IDF, Arduino or PlatformIO? C or C++? | | |

## 2.2 Organisational constraints

| ID | Constraint | Reason | Notes |
|---|---|---|---|
| OC-1 | **Solo project**, private, not commercial | | One person holds all roles: architect, developer, PCB designer, tester, operator. |
| OC-2 | **Low money**: budget limit TODO(E02): € ___ | Private project | Make it explicit (LG 02-05). |
| OC-3 | **Low time**: TODO(E02): ___ hours/week | Private project, alongside work | Make it explicit (LG 02-05). |
| OC-4 | Exam on 2026-12-11: architecture documentation takes priority until then; hardware build afterwards | Exam preparation | |
| OC-5 | Should work as a **portfolio project** | Career goal | Documentation must be readable by outsiders. |

## 2.3 Conventions

| ID | Convention | Notes |
|---|---|---|
| CV-1 | Architecture documentation follows **arc42**; decisions as **ADRs** (Nygard format) | |
| CV-2 | TODO(E02): coding style, units convention (SI units?), version control and branching | |

## 2.4 Regulatory constraints (R2: keep this short)

TODO(E02): battery safety (charging, BMS), radio (the ESP32-S3 module's certification), nothing commercial.
