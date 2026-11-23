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

**Explicit assumption (E01):** debugging will rely on logs, so a data link to the ground station is needed in v1. This is based on limited experience with mobile embedded projects. TODO(E02): confirm.

**Functional requirements:** TODO(E02)

| ID | Requirement | Priority |
|---|---|---|
| F-1 | | |

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
