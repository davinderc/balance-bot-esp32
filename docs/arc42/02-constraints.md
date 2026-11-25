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
| TC-10 | Framework and language for the robot firmware: **ESP-IDF directly, in C++** | Decided in E02 (D-10): more control than Arduino-ESP32 (which abstracts a lot away), e.g. pinning tasks to cores. PlatformIO is a build tool that supports both frameworks, so it is not the choice here. | Costly once drivers are written (fallback: Arduino-ESP32) | ESP-IDF runs on FreeRTOS, so FreeRTOS tasks come with it. Fallback trigger (E02): if reading the IMU over I²C and driving one motor with PWM don't both work within **2 evenings**, switch to Arduino-ESP32. |

## 2.2 Organisational constraints

| ID | Constraint | Reason | Notes |
|---|---|---|---|
| OC-1 | **Solo project**, private, not commercial | | One person holds all roles: architect, developer, PCB designer, tester, operator. |
| OC-2 | **Low money**: **€ 100** for v1 in total; about € 50 already spent on electronics (no PCB yet) | Private project | Stated in E02. Tools already on hand (charger, soldering iron, 3D printer) do not count against the budget: their cost can't be attributed to this project. What the remaining ~€ 50 must cover (PCB, shipping, missing parts): to check. |
| OC-3 | **Low time**: **about 4 hours/week** after the exam (OC-4) | Private project, alongside work | Stated in E02. May change depending on visible progress. Milestones: open. |
| OC-4 | Exam on 2026-12-11: architecture documentation takes priority until then; hardware build afterwards | Exam preparation | |
| OC-5 | Should work as a **portfolio project** | Career goal | Documentation must be readable by outsiders. |
| OC-6 | **Available skill set** (one person): strongest in Python; comfortable with C++, some C; fairly familiar with Arduino; new to ESP-IDF and FreeRTOS | Stated in E02 | Gaps in C/C++ and ESP-IDF to be bridged partly with LLM assistance: an assumption, see §11. |

## 2.3 Conventions

| ID | Convention | Notes |
|---|---|---|
| CV-1 | Architecture documentation follows **arc42**; decisions as **ADRs** (Nygard format) | |
| CV-2 | **SI units** in code, telemetry and logs | Agreed in E02. Avoids unit mix-ups between robot, ground station and data lab. |
| CV-3 | **Pinned versions** of framework and libraries (reproducible build) | Agreed in E02. Serves the maintainer and the open-source rebuilder. |
| CV-4 | **Git, trunk-based on `main`** | Agreed in E02. |
| CV-5 | Coding style | TODO: pick one (later, before the first firmware code). |

## 2.4 Regulatory constraints (R2: keep this short)

| ID | Constraint | Notes |
|---|---|---|
| RC-1 | **Battery safety**: Li-ion cells only with a BMS, charged with a suitable charger | Protects against over-charge, over-discharge and short circuit. |
| RC-2 | **Radio**: use a pre-certified ESP32-S3 module, no changes to the RF part | Certification of the module: to verify. |
| RC-3 | **Not sold commercially** | Private portfolio project; no product regulations (e.g. CE marking of a product) apply. |
