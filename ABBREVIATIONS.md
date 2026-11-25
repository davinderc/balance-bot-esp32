# Abbreviations and ID conventions

Every abbreviation and ID prefix used in this repository. Architecture *concepts* (what a quality scenario or a building block is) belong in the glossary, [docs/arc42/12-glossary.md](docs/arc42/12-glossary.md).
When you introduce a new abbreviation or ID prefix, add it here.

## 1. Project IDs

These prefixes number items inside this repository.

| ID | Meaning | Defined in |
|---|---|---|
| **E01–E11** | Exercise (one practice session) | [exercises/](exercises/README.md) |
| **M1–M4** | Mock exam session | [exercises/mock-exams.md](exercises/mock-exams.md) |
| **F-n** | Functional requirement | [01-introduction-and-goals.md](docs/arc42/01-introduction-and-goals.md) §1.1 |
| **TC-n** | Technical constraint (hardware, toolchain) | [02-constraints.md](docs/arc42/02-constraints.md) §2.1 |
| **OC-n** | Organisational constraint (budget, time, team) | [02-constraints.md](docs/arc42/02-constraints.md) §2.2 |
| **CV-n** | Convention (documentation format, coding style) | [02-constraints.md](docs/arc42/02-constraints.md) §2.3 |
| **RC-n** | Regulatory constraint (battery safety, radio, legal) | [02-constraints.md](docs/arc42/02-constraints.md) §2.4 |
| **D-n** | Entry in the decision log (smaller decisions) | [09-decisions.md](docs/arc42/09-decisions.md) §9.1 |
| **ADR-NNNN** | Architecture Decision Record (significant decisions, one file each) | [docs/adr/](docs/adr/0000-template.md) |
| **QS-n** | Quality scenario | [10-quality-requirements.md](docs/arc42/10-quality-requirements.md) §10.2 |
| **CR-n** | Candidate risk: an unverified question raised during setup | [11-risks-and-technical-debt.md](docs/arc42/11-risks-and-technical-debt.md) §11.1 |
| **AS-n** | Assumption, with its validation status | [11-risks-and-technical-debt.md](docs/arc42/11-risks-and-technical-debt.md) §11.1a |
| **TODO(Exx)** | Open point, to be resolved in exercise Exx | anywhere in `docs/` |
| **§n** | Section n of the arc42 documentation | `docs/arc42/` |

## 2. iSAQB exam and curriculum

| Abbreviation | Meaning |
|---|---|
| **iSAQB** | International Software Architecture Qualification Board (the certification body) |
| **CPSA-F** | Certified Professional for Software Architecture, Foundation Level (the exam) |
| **LG xx-yy** | Learning Goal: chapter xx, goal yy of the curriculum (e.g. LG 03-04 = design principles) |
| **R1 / R2 / R3** | Relevance of a learning goal for the exam. **R1** = can be examined, must master. **R2** = may be examined, understand it. **R3** = not examined, nice to know. |
| **A-, P-, K-type** | Exam question types. **A** = single choice. **P** = pick multiple ("which TWO are true?"). **K** = classify each statement (e.g. true/false). |
| **EN / DE** | English / German (the language versions of the curriculum) |
| **IREB** | International Requirements Engineering Board (cited in the curriculum) |

## 3. Software architecture

| Abbreviation | Meaning |
|---|---|
| **arc42** | Template for architecture documentation (12 sections); used in `docs/arc42/` |
| **ADR** | Architecture Decision Record (format by Michael Nygard: context, decision, consequences) |
| **C4** | C4 model: Context, Containers, Components, Code (a notation for architecture diagrams) |
| **ISO/IEC/IEEE 42010** | Standard defining the concepts of architecture description (stakeholder, concern, view, viewpoint) |
| **ISO 25010** | Standard quality model for software products (quality characteristics) |
| **Q42** | The arc42 quality model |
| **UML** | Unified Modeling Language |
| **SysML** | Systems Modeling Language (UML extension for systems engineering and mechatronics) |
| **BPMN** | Business Process Model and Notation |
| **ER** | Entity-relationship (diagram) |
| **ATAM** | Architecture Tradeoff Analysis Method (scenario-based assessment); "ATAM-lite" = a simplified version |
| **DDD** | Domain-Driven Design |
| **SOLID** | Single responsibility, Open/closed, Liskov substitution, Interface segregation, Dependency inversion |
| **KISS** | Keep It Simple, Stupid |
| **YAGNI** | You Aren't Gonna Need It |
| **DRY** | Don't Repeat Yourself |
| **CQRS** | Command Query Responsibility Segregation |
| **MVC / MVVM / MVU** | Model-View-Controller / Model-View-ViewModel / Model-View-Update |
| **SOA** | Service-Oriented Architecture |
| **RPC** | Remote Procedure Call |
| **ETL** | Extract, Transform, Load (data pipeline) |
| **LOC** | Lines of Code |
| **SaaS** | Software as a Service |
| **UI** | User Interface |
| **QA** | Quality assurance (testing role) |
| **MVP** | Minimum viable product: the smallest release that is still useful |
| **v1 / v2** | First / second release of the Balance Bot platform (scope in §1.1) |

## 4. Hardware and electronics

| Abbreviation | Meaning |
|---|---|
| **MCU** | Microcontroller unit (here the ESP32-S3) |
| **SBC** | Single-board computer (e.g. a Raspberry Pi); possible later upgrade for ROS 2 |
| **PCB** | Printed circuit board |
| **IMU** | Inertial measurement unit: accelerometer + gyroscope (here the MPU-6050) |
| **BMS** | Battery management system (protects the Li-ion pack) |
| **2S / 3S** | Battery pack with 2 or 3 cells in series |
| **N8R8** | ESP32-S3 module variant: 8 MB flash, 8 MB PSRAM |
| **PSRAM** | Pseudo-static RAM (external RAM next to the MCU) |
| **RF** | Radio frequency (the radio part of the ESP32-S3 module) |
| **GPIO** | General-purpose input/output (pin) |
| **PWM** | Pulse-width modulation (motor speed control) |
| **PCNT** | Pulse counter: ESP32 peripheral that can decode quadrature encoders |
| **MCPWM** | Motor Control PWM: ESP32 peripheral for motor drive signals |
| **LEDC** | LED Control: general-purpose ESP32 PWM peripheral |
| **ADC** | Analog-to-digital converter |
| **I²C** | Inter-Integrated Circuit: 2-wire sensor bus (IMU, INA219) |
| **AB (encoder)** | Two-phase (A and B) quadrature encoder signals: they give direction as well as speed |
| **USB-OTG** | USB On-The-Go: the MCU can act as a USB device or host |
| **JTAG** | Hardware debugging interface |

## 5. Embedded software and communication

| Abbreviation | Meaning |
|---|---|
| **ESP-IDF** | Espressif IoT Development Framework (official ESP32 SDK) |
| **FreeRTOS** | Real-time operating system used by ESP-IDF |
| **NVS** | Non-volatile storage: ESP32 key-value store in flash (calibration, parameters) |
| **OTA** | Over-the-air (firmware update via Wi-Fi) |
| **ROS 2** | Robot Operating System, version 2 |
| **micro-ROS** | ROS 2 for microcontrollers; talks to a "micro-ROS agent" on the host |
| **DDS** | Data Distribution Service (publish/subscribe middleware underneath ROS 2) |
| **UDP / TCP** | User Datagram Protocol / Transmission Control Protocol |
| **CBOR** | Concise Binary Object Representation (compact binary data format) |
| **CSV** | Comma-separated values |
| **ML** | Machine learning |
| **SI units** | International System of Units (m, s, rad, …) |
| **IDE** | Integrated development environment |
