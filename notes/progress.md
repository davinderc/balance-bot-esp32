# Progress log

## Status

| Session | Status | Date | Exam-question score |
|---|---|---|---|
| E01 Kick-off, stakeholders | in progress (steps 1–4 first pass done) | 2026-11-21 → 23 | pending |
| E02 Requirements, constraints, assumptions | open | | |
| E03 Quality goals and scenarios | open | | |
| E04 Context and interfaces | open | | |
| M1 Mock: chapters 1–2 | open | | |
| E05 Solution strategy | open | | |
| E06 Building blocks, principles, dependencies | open | | |
| E07 Patterns | open | | |
| E08 Runtime, deployment, notations | open | | |
| E09 Cross-cutting concepts, data | open | | |
| E10 Decisions and documentation | open | | |
| M2 Mock: chapters 3–4 | open | | |
| E11 Analysis and assessment | open | | |
| M3 Full mock + official iSAQB mock | open | | |
| M4 Full mock | open | | |

## Weak spots (keep this list current; mock exams draw on it)

- LG 01-01 (R1): could not recall the four commonalities of architecture definitions. Answered with goals/benefits (LG 01-02) instead.
- LG 01-01 (R1): building block vs. component. Used "specific vs. generic" as the test; the right test is "encapsulated behind an interface, replaceable".
- Architecture vs. architecture description (ISO 42010): said architecture "is a description". Every system has an architecture; not every system has a description.
- Product scope vs. project plan: used "not needed for the exam" as a scope reason.

## Session entries

<!-- Template:
### YYYY-MM-DD: Exx <title>
- Score: x/y
- Wrong / shaky: LG xx-yy (<topic>): <what went wrong>
- Follow-ups: <open TODOs carried over>
-->

### 2026-11-21 to 2026-11-23: E01 Kick-off, vision, stakeholders (paused, continue next session)
- Done: warm-up; step 1 (definition, revised to cover all four commonalities); step 2 (boundaries, all five correct with nuances); step 3 (vision confirmed, v1 scope decided, written to §1.1); step 4 first pass (5 roles, written to §1.3).
- Score: exam check not done yet.
- Carry over to the start of the next session, before E02 (about 35–45 min):
  - Step 4 review. Notes: role-based format is right. Hints for missing roles: who maintains it later, who runs it at a demo, who stands *near* it (safety: battery, falling robot), who reads the repo in depth vs. who skims it for 5 minutes. Challenge: who is the "end user" of a solo hobby robot (implicit assumption)? Hardware-developer expectations should say what they need *from the software architecture* (pin and peripheral needs, timing).
  - Step 5 role-play interviews (hiring manager; you in six months).
  - Step 6 architect's tasks (LG 01-04, 01-06), step 7 elevator pitch (LG 01-02).
  - Transfer question (stakeholders of an online insurance portal), exam check (3–5 questions), close E01.
- Follow-ups found in E01:
  - TODO(E02): telemetry "live only" (drop oldest) or "complete for experiments" (local logging)? Local flash logging conflicts with "no flash writes while balancing".
  - TODO(E02): verify in ESP-IDF docs that Wi-Fi/BT is pinned to core 0 (CONFIG_ESP_WIFI_TASK_PINNED_TO_CORE, CONFIG_BT_BLUEDROID_PINNED_TO_CORE) and the flash/NVS stall behaviour (source so far: Gemini).
  - TODO(E02): TC-10 is a *framework* choice (ESP-IDF vs. Arduino), not an IDE choice (PlatformIO supports both).
  - TODO(E02): define what counts as telemetry; if core 0 samples current separately, a common timestamp is needed.
  - TODO(E04): PCB pin map and I²C bus sharing act as an interface between hardware and software.
  - TODO(E05): micro-ROS vs. own protocol vs. full ROS 2 on an SBC; must be decided before the link is built.
  - TODO(E06): sensor fusion inside the IMU driver or in a separate state estimator?
  - TODO(E11): risk "ESP32-S3 fast enough for the control loop" (assumption from Gemini); check: measure worst-case loop time on the dev board before the PCB.
  - Candidate principles from E01: bounded execution time on the control path; no blocking calls, no dynamic allocation, no I/O waits there; no flash writes while balancing.

