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

First pass from E01; to be refined after the stakeholder interviews (E01 step 5, carried over).

| Role | Concerns | Expectations of the architecture or documentation |
|---|---|---|
| Hardware developer | All electrical connections are correct (no shorts, reversed or missing connections); signals are clean. | Hardware requirements are listed and the vision is clear. Responsible for the component list, schematic and later the PCB design. |
| Software developer | Hardware is built and working, so software can be deployed and tested; hardware tests are documented so hardware faults can be ruled out; charging and operation take little time and effort. | Hardware components are listed and the schematic is readable, so the tech stack and software building blocks can be set up to match. |
| Potential employer or client | The project is clearly documented and tested; there are videos of the robot running. | Architecture and documentation are complete and easy to read, with summaries where helpful. |
| End user | Easy to use and operate; internals are protected, so the circuits are hard to damage in use. | A short project summary in the documentation, possibly with a brief operating guide. |
| Tester / QA | Individual functions can be verified; end-to-end behaviour can be verified. | Interfaces for testing are described in the documentation. |
| TODO(E01) | Further roles still to be added (see the review notes in `notes/progress.md`). | |
