# Progress log

## Status

| Session | Status | Date | Exam-question score | Actual time |
|---|---|---|---|---|
| E01 Kick-off, stakeholders | **done** | 2026-11-21 → 24 | 4.8/5 (96%) | ≈ 4–5 h over 4 sittings (estimate; plan 90 min) |
| E02 Requirements, constraints, assumptions | **done** | 2026-11-24 → 27 | 5/5 (100%) | TODO: fill in hours (5 sittings) |
| E03 Quality goals and scenarios | open | | | |
| E04 Context and interfaces | open | | | |
| M1 Mock: chapters 1–2 | open | | | |
| E05 Solution strategy | open | | | |
| E06 Building blocks, principles, dependencies | open | | | |
| E07 Patterns | open | | | |
| E08 Runtime, deployment, notations | open | | | |
| E09 Cross-cutting concepts, data | open | | | |
| E10 Decisions and documentation | open | | | |
| M2 Mock: chapters 3–4 | open | | | |
| E11 Analysis and assessment | open | | | |
| M3 Full mock + official iSAQB mock | open | | | |
| M4 Full mock | open | | | |

## Weak spots (keep this list current; mock exams draw on it)

- LG 01-01 (R1): could not recall the four commonalities of architecture definitions. Answered with goals/benefits (LG 01-02) instead.
- LG 01-01 (R1): building block vs. component. Used "specific vs. generic" as the test; the right test is "encapsulated behind an interface, replaceable".
- Architecture vs. architecture description (ISO 42010): said architecture "is a description". Every system has an architecture; not every system has a description.
- Product scope vs. project plan: used "not needed for the exam" as a scope reason.
- LG 01-04 (R1): mixed up decomposing the *work* (tasks, project planning) with decomposing the *system* (building blocks with interfaces).
- LG 01-02 (R1): elevator pitch was abstract at first; missed "structures understood by stakeholders" (the strongest benefit for a portfolio project) and "systematically reduce complexity". Keep LG 01-01 (what architecture is) apart from LG 01-02 (why we do it).
- LG 01-02 (R1), **third miss (E02 warm-up)**: gave "documentation" instead of "structures and concepts understood by all relevant stakeholders", and "risk awareness" (an architect's *task*, LG 01-04) as a benefit. Pattern: naming the *measure* instead of the *goal*. Same pattern in E02 step 6 (goal phrased as an activity).
- LG 02-02 (R1): requirement vs. constraint, mixed up in both directions: "runs on battery" (a constraint, TC-4) as a functional requirement; in the transfer question, "admins can correct mistakes" and "app and web must not contradict" (requirements) as constraints. Test: does it say what the system does / how well (requirement), or does it limit how we may build it, non-negotiable for now (constraint)?
- LG 02-02 (R2): Conway's law: first described implicit decisions; then reversed the direction (teams follow the platforms). Correct: the system mirrors the *existing* communication structure of the organisation.
- LG 02-05 (R1): strength of evidence: forum figures make an assumption *plausible*, not *validated*; "can be configured" ≠ "is the default".
- LG 01-02 (R1), **repeat**: in the E01 exam check, marked "ensure structures and concepts are understood by all relevant stakeholders" as *not* a benefit (it is one, nearly verbatim). Same benefit was missing from the pitch. Exam tip: "all *relevant* stakeholders" is curriculum wording; "all stakeholders", "guarantee", "always", "every" without qualification are the overgeneralisation flags.

## Session entries

<!-- Template:
### YYYY-MM-DD: Exx <title>
- Score: x/y
- Wrong / shaky: LG xx-yy (<topic>): <what went wrong>
- Follow-ups: <open TODOs carried over>
-->

### 2026-11-21 to 2026-11-23: E01 Kick-off, vision, stakeholders (first part)
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

### 2026-11-24: E01 continued (steps 4–7 done; paused before transfer question and exam check)
- Step 4: stakeholder table finalised in §1.3 (9 roles: hardware dev, software dev, maintainer, tester/QA, demo operator, bystander, hiring manager/recruiter, technical reviewer, open-source rebuilder).
- Step 5: role-play interviews done. Hiring manager: README must hook in ~30 s; honest docs; numbers over text; "show your work"; known limitations. Maintainer: build/flash from a fresh clone, pin map matching reality, parameters in the repo (robot flash is only a copy), run logs record their parameter set, secrets out of the public repo, parking note + tag of last known-good firmware.
- Step 6: architect's tasks mapped to the project. Good: identified feedback as the main difficulty when working alone. Corrections: decomposition is about the system, not the work; task 7 depends on task 1; feedback also comes from measurements, prototypes and tests (LG 03-05).
- Step 7: pitch abstract, comeback concrete (flash writes stall both cores → random falls). Lesson: one concrete failure beats three correct principles.
- **Pending at the start of the next session (about 15 min), then close E01:**
  - Transfer question: insurance customer portal; team listed customers, product owner, developers, testers. Name 3–4 forgotten stakeholders, each with one concern that affects the architecture.
  - Exam check, 5 questions, already posed (answer from memory, no links):
    - Q1 (P, pick THREE): commonalities of definitions. a) building blocks with interfaces and relationships; b) architecture exists only if documented in an architecture description; c) decisions and their consequences for the whole system and lifecycle; d) primarily about selecting languages and frameworks; e) structures, cross-cutting concerns and principles; f) detailed implementation of every class.
    - Q2 (A): building block vs. component. a) component is the general term, building blocks a special form; b) building block is the general term, components a special form; c) synonyms in all definitions; d) building blocks only at runtime, components only in source code.
    - Q3 (K, true/false: goal or benefit of architecture?): a) systematically reduce complexity; b) structures and concepts understood by all relevant stakeholders; c) guarantee delivery within budget; d) specify architecturally relevant guidelines for implementation and operation; e) make separate requirements engineering unnecessary.
    - Q4 (P, pick TWO): tasks of architects. a) clarify and scrutinize requirements and constraints, agree refinements with stakeholders; b) define budget and staffing plan; c) analyze and evaluate the architecture regarding risks to meeting requirements; d) personally write all source code for critical components; e) approve the final release to customers.
    - Q5 (A): stakeholder concerns. a) every concern must become a documented requirement; b) stakeholders who don't read the docs are not relevant; c) identify short-term vs. long-term conflicts and involve the relevant stakeholders; d) project vs. maintainability conflicts are resolved by the architect alone.
- New follow-ups:
  - TODO(E02): safety requirements from the bystander and demo operator (tilt cutoff, low-battery cutoff, shutdown: physical switch [HW], kill command [SW], or both?).
  - TODO(E02): what the open-source rebuilder needs (parts list, wiring, build and flash instructions); reproducible build (pinned framework and library versions) as a convention (CV-2).
  - TODO(E02): spare "timing" GPIO plus a low-cost logic analyser for testability (small extra cost; decide).
  - TODO(E03): quality scenario "README hooks a hiring manager within ~30 s".
  - TODO(E09): configuration management: source of truth for parameters (repo vs. robot flash), run log ↔ parameter set, secrets handling.
  - TODO(E10): proportional documentation rule (e.g. 5-minute parking note per session; full ADR only for decisions that are expensive to reverse); layered docs (README for the skim, arc42/ADRs for depth).
  - TODO(E11): conformance checks (e.g. control code must not include Wi-Fi headers), LG 05-03.

### 2026-11-24: E01 closed
- Transfer question (insurance portal, forgotten stakeholders): good. Named claim reviewers, policy authors/legal, government/regulator, DevOps. Feedback: "follows local laws" too vague; concerns only help the architecture when concrete (health data in uploads, retention, audit trail; claim spikes after storms → scalability). Also often forgotten: data protection/security officer, call-centre agents, owners of back-end systems, brokers.
- Score: 4.8/5 (Q1 ✔, Q2 ✔, Q3 4/5, Q4 ✔, Q5 ✔).
- Wrong / shaky: LG 01-02 (R1): Q3b, "structures and concepts understood by all relevant stakeholders" is a benefit (marked false).
- Follow-ups: all TODOs listed in the two E01 entries above. Next: E02.

### 2026-11-24 to 25: E02 in progress (paused before step 3 part B)
- Warm-up: W1 1/3 exact (LG 01-02: "documentation" given instead of "understood by all relevant stakeholders", **third miss**; "risks" given, but risk analysis is an architect's *task*, LG 01-04, not a benefit). W2 correct verdict; architecture comes from decisions and structures, not from the vision.
- Step 1 done: F-1 to F-16 in §1.1 with priorities. Debugging decision recorded (telemetry and logs while balancing; assumption *plausible*). Caught: "runs on battery" was a constraint (TC-4), micro-ROS a technology decision, "no jitter" a quality requirement; live tuning vs. "parameters only when lying down" conflicted.
- Step 2 done: TC-10 = ESP-IDF in C++ (D-10, fallback trigger 2 evenings), OC-6 skills, CV-2 to CV-5, RC-1 to RC-3, D-11 ground station platform open → E05.
- Step 3 part A done: OC-2 € 100 (≈ € 50 spent), OC-3 ≈ 4 h/week after the exam, milestones open.
- Shaky: Conway's law (LG 02-02, R2): first answer described implicit decisions instead of "structure mirrors communication structure"; second attempt (3 teams → 3 subsystems) right.
- Implicit assumptions found: FreeRTOS seen as optional (it comes with ESP-IDF); auto-arming assumes someone holds the robot upright; ground station assumes the home network.
- Step 3 part B done (2026-11-25, evening): AS-1 to AS-13 rated, with sources, in §11.1a. Good: looked up primary sources (ESP-IDF docs, Toshiba datasheet). Learned: forum figures make an assumption *plausible*, not *validated*; "can be configured" ≠ "is the default"; compare stall current with the *continuous* rating, not the peak.
- **Resume with:** decide whether AS-12's sources change D-10 (ESP-IDF vs. Arduino first); step 4 (one "why" line + reversibility per hardware choice in §9.1, mostly prepared by the AS work); step 5 (3S margin 12.6 V vs. 13.5 V driver limit, back-EMF, remaining € 50); step 6; skip step 7 (R3); transfer question; exam check.

### 2026-11-26 to 27: E02 closed
- Step 4 done: why line + reversibility for D-1 to D-8 and new D-12 (wheels) in §9.1; reversibility copied into §2.1. Strong: D-2 ↔ D-3 dependency found unprompted; HW vs. SW reversibility separated; D-8 seen as the decision that keeps the others cheap. D-3 reason sharpened with the L298N voltage-drop comparison (datasheets). D-10 confirmed (ESP-IDF); its reason contains an unverified assumption (Arduino-ESP32 can also call ESP-IDF/FreeRTOS APIs).
- Step 5 done: CR-3 and CR-4 extended, CR-8 to CR-12 added as questions to check. CR-12 (IMU swap) is input for a modifiability scenario in E03. CR-9 (shared I²C bus) is a pin-map question for E04.
- Step 6 done: three short- vs. long-term conflicts in §1.3 (docs first vs. hardware now; ESP-IDF vs. Arduino; IMU abstraction). Needed a clarification of what "short- vs. long-term" means; exam vs. portfolio was short vs. short.
- Step 7 skipped (R3, lean lever 2).
- Transfer question (bank payment-initiation constraints): 2 of 4 clean (core banking system technical; authentication regulatory, with correct design consequence MFA). 2 of 4 were requirements in disguise. Conway reversed at first. Feedback: PSD2 strong customer authentication vs. GDPR are different regulatory concerns; Conway predicts payment logic duplicated per channel team.
- Score: 5/5 (Q1 b ✔, Q2 a, c ✔, Q3 R R C C C ✔, Q4 c ✔, Q5 a, c ✔, unsure on c).
- Follow-ups:
  - TODO(E03): quality scenarios for: fall response time (F-4), "near upright" range for arming (F-16), link-loss timeout (F-8), no jitter/oscillation (F-1), IMU swap effort (CR-12, modifiability), README hooks a hiring manager in ~30 s.
  - TODO(E04): pin map with a spare timing GPIO; one or two I²C buses (CR-9); robot–ground station protocol as a defined interface (Conway point).
  - TODO(E05): timer-driven control loop (tick too coarse, AS-1); spike for jitter with Wi-Fi (AS-13); micro-ROS (D-9); ground station platform (D-11).
  - TODO(E06): IMU abstraction boundary (raw data vs. orientation estimate); control path in IRAM as an option (AS-3).
  - TODO(E10): open-source rebuilder docs (parts list, wiring, build and flash).

