# Balance Bot: an iSAQB CPSA-F practice project

A small self-balancing robot, used for two things:

1. **Learning by doing for the iSAQB CPSA-F exam** (2026-12-11, in English, based on curriculum 2025.1). Each exercise covers a set of learning goals and produces a piece of real architecture documentation.
2. **A portfolio project** covering software architecture, embedded firmware, control engineering, PCB design and data analysis.

## Folder layout

```
CLAUDE.md            rules for the AI sparring partner (loaded automatically by Claude Code)
exercises/           one file per session, plus schedule and coverage matrix (exercises/README.md)
docs/arc42/          the architecture documentation (arc42 template, one file per section)
docs/adr/            architecture decision records
notes/progress.md    session log: scores, weak spots, follow-ups
reference/           curriculum PDFs and text extracts (private; never publish, see .gitignore)
```

## How to run a session

Open a new Claude Code session in this folder and say:

> Let's do exercise 03.

Or just "next exercise". The sparring partner reads the exercise, your progress log and the relevant learning goals, then works through the exercise with you, mostly by asking rather than telling. Each session ends with exam-style questions and a progress-log entry.

## The system

The documented system is the **Balance Bot platform**, not just the firmware:

- **Robot firmware:** ESP32-S3 running sensor fusion, the balance controller, motor control and safety logic.
- **Ground station:** a laptop app for live tuning, telemetry and remote driving.
- **Data lab:** stores the run logs and analyses them (comparing controllers, fault analysis, maybe ML).
- **Optional:** over-the-air (OTA) firmware updates.

Making the system this wide gives enough to work on for every chapter of the curriculum. Hardware details are in [docs/arc42/02-constraints.md](docs/arc42/02-constraints.md).
