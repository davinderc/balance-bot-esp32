# 1. Introduction and Goals

## 1.1 Requirements overview

> Exercises: **E01** (vision, scope), **E02** (functional requirements).

**Vision** (agreed in E01):
A small, low-cost, two-wheeled self-balancing robot and its tooling: a ground station for tuning and telemetry, and a data lab for analysing runs. It is a portfolio project. It shows potential employers and clients end-to-end engineering skills (software architecture, embedded firmware, control engineering, PCB design and data analysis), so they can see what they would be paying for. It also gives its builder evidence, and confidence, that these skills hold up in a real project.

**System scope for v1** (decided in E01; boundaries refined in E04):

The vision describes where the project is going; v1 is the smallest release that is still a convincing portfolio piece (low time, low money: OC-2, OC-3).

| Part | In v1? | Reason |
|---|---|---|
| Robot firmware (ESP32-S3) | yes | Core of the project. Control loop 200–500 Hz. |
| Ground station: live parameter tuning | yes | Fast tuning iterations; avoids re-flashing for every gain change. |
| Ground station: telemetry display and log capture | yes | Needed for debugging; also produces the logs the data lab will use. |
| Ground station: remote control (driving) | later | v1 only needs to balance. |
| Data lab (analysing runs, comparing controllers) | later | Simple PID control is enough at first; logs are already captured in v1. |
| OTA updates | later | High time cost (partitioning, update and rollback, security), little portfolio value. If built: only while the robot is not balancing, because flash writes stall both cores (to verify). |
| micro-ROS integration | open, decide in E05 | Not researched yet. Must be decided before the robot–ground station link is built, because switching later means rewriting both ends. |

**Decision (E02):** while the robot balances, debugging uses telemetry and logs over the wireless link. Breakpoints (USB/JTAG) are only for non-critical code on the bench: a breakpoint halts the control loop and the robot falls, and a cable changes the robot's dynamics.
**Assumption behind it (E01, status *plausible*: reasoned, not tested):** telemetry and logs are enough to find faults in the running control loop. This is based on limited experience with mobile embedded projects.

**Functional requirements** (E02). Each row says *what* the system does; *how well* (response times, thresholds, smoothness) goes to the quality scenarios in E03.
Priority: **must** = v1 is not done without it; **should** = v1 if time allows; **later** = v2 or beyond.

| ID | The system shall … | Tag | Priority | Notes |
|---|---|---|---|---|
| F-1 | Balance in place. | [SW] | must | "No jittery or oscillating movement" → quality scenario (E03). |
| F-2 | Hold a position or follow a velocity setpoint while balancing. | [SW] | later | Driving by remote control is also "later" (scope table above). |
| F-3 | Operate untethered: no cable for power, communication or debugging while balancing. | [SW+HW] | must | Realised by TC-4 (battery) and the wireless link. Rules out e.g. running the controller on a laptop over USB. |
| F-4 | Detect a fall (tilt beyond a threshold) and disable motor power. | [SW] | must | Response time → E03. Threshold value: later. |
| F-5 | After any motor cutoff (fall, kill command, link loss, low battery), stay disarmed until re-armed by a command from the ground station. | [SW] | must | Re-arm button on the robot [HW]: later. Automatic re-arm when upright again: rejected for now (bystander safety); revisit only with a safety argument. |
| F-6 | Disable motor power on a kill command from the ground station, at any time. | [SW] | must | Needs a working link; the physical switch (F-7) is the fallback. |
| F-7 | Provide a physical switch that disables motor power. | [HW] | must | Cuts the motor supply only; the MCU stays powered and keeps logging. |
| F-8 | Disable motor power if no message has arrived from the ground station within a timeout (link loss). | [SW] | must | The timeout must bridge short dropouts: keep balancing while the link recovers. Timeout value → E03. Revisit after measuring how often and how long the link drops. |
| F-9 | Raise a low-battery warning on the ground station, from the battery voltage in the telemetry (F-10). | [SW] | must | Minimal cost: uses data that is already sent. Threshold must sit above the BMS cutoff (to check). Warning on the robot itself (a distinct motion): later. Buzzer rejected (effort). |
| F-10 | Stream live telemetry: newest data has priority, old samples may be dropped. | [SW] | must | Content: see list below. |
| F-11 | Stream complete telemetry for experiments (no loss). | [SW] | later | |
| F-12 | Show telemetry as live graphs on the ground station. | [SW] | later | Until then: log files plus offline plotting. |
| F-13 | Record telemetry to log files on the ground station, for debugging and later analysis. | [SW] | must | Each log records the parameter set that produced it (maintainer concern, TODO(E09)). |
| F-14 | Change control parameters from the ground station while the robot runs; they take effect at once. | [SW] | must | v1: parameters live in robot RAM only. After power-on, the ground station sends a parameter set and then the arm command. |
| F-15 | Keep tuned parameters across power cycles: load them from flash at power-on; save them to flash only while not balancing. | [SW] | later | Not needed for v1, because the ground station sends the parameters and arms the robot anyway (F-14, F-16). Save points: after a kill command, after a fall, or when picked up and set down. Reason: flash writes stall both cores (to verify). Source of truth (repo, ground station or robot) → TODO(E09). |
| F-16 | Arm the motors only on a command from the ground station, and only when a valid parameter set is loaded and the robot is held near upright. Otherwise refuse and report why. | [SW] | must | No compiled-in default parameters; no automatic arming (a robot lying down or half-upright on a table must not lurch). Optional: an LED pattern confirms the arm command (if the board has a usable LED, to verify). "Near upright" range → E03. |

**Telemetry content (F-10):** estimated pitch angle; accelerometer tilt angle (raw); pitch rate (gyroscope); raw accelerometer and gyroscope axes; forward/backward linear velocity; wheel positions (encoder counts); wheel speeds (optional); motor commands (PWM duty); PID contributions (P, I, D); battery voltage; current and energy (INA219); ID of the active parameter set; timestamps on a common time base.

## 1.2 Quality goals

> Exercise: **E03**. The 3–5 most important quality goals, in priority order.

| Priority | Quality goal | Motivation |
|---|---|---|
| 1 | TODO(E03) | |

## 1.3 Stakeholders

> Exercise: **E01**. List roles, not people; one person can hold several roles.

Agreed in E01. The repository is public.

| Role | Concerns | Expectations of the architecture or documentation |
|---|---|---|
| Hardware developer | All electrical connections are correct (no shorts, reversed or missing connections); signals are clean. | Hardware requirements are listed and the vision is clear. Responsible for the component list, schematic and later the PCB design. From the software architecture: which peripherals and pins it needs, timing needs, debug access. |
| Software developer (also builds and tests features) | Hardware is built and working, so software can be deployed and tested; hardware tests are documented so hardware faults can be ruled out; charging and operation take little time and effort. | Hardware components are listed and the schematic is readable, so the tech stack and software building blocks can be set up to match. |
| Maintainer (the builder, coming back later, e.g. for v2 features) | How to do one-time or infrequent tasks (calibrating sensors, charging the battery, wiring the robot). The last known working state (hardware and software configuration and parameters) and how to reproduce it. A quick overview or index, to find things fast. The latest progress and the planned next steps. Current issues. Secrets (e.g. Wi-Fi credentials) stay out of the public repository. Every run log records which parameter set produced it. | Everything needed to get the project running again quickly: detailed, but structured so the exact piece is easy to find. Hardware state, software parameters and configuration, library versions and build environment, and what was left in progress. An ignored file for secrets, with an example template in the repository. TODO(E09): configuration management (source of truth for parameters, link between run logs and parameter sets). |
| Tester / QA | Individual functions can be verified; end-to-end behaviour can be verified. | Interfaces for testing are described in the documentation. |
| Demo operator | Easy to operate; can shut the robot down safely if something goes wrong. | A short operating guide, including how to shut down. |
| Bystander (near the robot, no technical background) | No exposed wires or battery terminals; no injury if the robot falls over. | Does not read the documentation. Their concerns become safety requirements (TODO(E02)). |
| Hiring manager / recruiter (5-minute skim) | The project is clearly documented and tested; there are videos of the robot running. Documentation is open and honest and does not hide assumptions. Numbers are shown quickly, in a variety of forms, rather than in long text. The engineer's thought process is visible ("show your work"): what was done and why, what was rejected and why, what was removed and why, and notes for future readers. The README must hook the reader quickly, or they close the tab. | Documentation that is concise but does not leave out the reasoning behind the project. TODO(E03): turn "hooks the reader quickly" into a quality scenario. |
| Technical reviewer (interviewer or fellow engineer, in-depth read) | Quality of the engineering. | Decisions with their reasons, code, tests. |
| Open-source rebuilder (builds their own robot from the public repo) | A (possibly shallow) mix of the concerns of the hardware developer, software developer, maintainer, tester, technical reviewer and demo operator. | TODO(E02): what they need to rebuild it (parts list, wiring, build and flash instructions?). |
