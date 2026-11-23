# Exercises: schedule and coverage

Exam: **Friday 2026-12-11**. Baseline: curriculum **2025.1-rev2 (EN)**.
Each session takes about 60–90 minutes. Buffer days absorb overruns; skip them if you're on track.

## Timeline

*Revised 2026-11-23. The first plan (one exercise a day from 11-21) is out of date: E01 was planned at 75 min and has taken three sittings so far.*

### How long the sessions take

- **Plan** is the focused working time from each exercise file.
- **Budget** is plan × 2. That's what to block in the calendar: E01 showed that discussion, role-play and writing the docs take about twice the planned time, or more.
- After each session, record the actual time in [notes/progress.md](../notes/progress.md). After E02 and E03, compare actual with budget and adjust the factor.

| Session | Topic | R1 share | Plan | Budget |
|---|---|---|---|---|
| [E01](01-kickoff-role-stakeholders.md) (rest) | Transfer question and exam check | high | 15 min | 30 min |
| [E02](02-requirements-constraints-assumptions.md) | Requirements, constraints, explicit assumptions | high | 90 min | 3 h |
| [E03](03-quality-goals-scenarios.md) | Quality goals, quality tree, scenarios | high | 90 min | 3 h |
| [E04](04-context-and-interfaces.md) | Business and technical context, interfaces | high | 75 min | 2.5 h |
| [M1](mock-exams.md) | Mini mock exam: chapters 1–2 (15 questions) | – | 45 min | 1 h |
| [E05](05-solution-strategy-approaches.md) | Solution strategy, design approaches, iterations | high | 90 min | 3 h |
| [E06](06-building-blocks-principles-dependencies.md) | Building blocks, design principles, coupling | **highest** | 90 min | 3 h |
| [E07](07-patterns.md) | Architectural and design patterns | medium (3 R1 patterns, rest R3) | 75 min | 2.5 h |
| [E08](08-runtime-deployment-notations.md) | Runtime and deployment views, notations, distribution | medium (views R1, rest R2/R3) | 90 min | 3 h |
| [E09](09-crosscutting-concepts-data.md) | Cross-cutting concepts, data models | medium | 90 min | 3 h |
| [E10](10-decisions-and-documentation.md) | Decisions (ADRs), documentation for audiences | high | 90 min | 3 h |
| [M2](mock-exams.md) | Mini mock exam: chapters 3–4 (20 questions) | – | 60 min | 1 h |
| [E11](11-analysis-and-assessment.md) | Architecture analysis and assessment | high | 90 min | 3 h |
| [M3](mock-exams.md) | Full timed mock, plus the **official iSAQB mock exam**, plus review | – | 2.5 h | 3 h |
| [M4](mock-exams.md) | Second full mock, or weak-spot review | – | 1.5 h | 2 h |
| **Total remaining** | | | **≈ 20 h** | **≈ 37 h** |

### Calendar (weekdays during work hours; weekends are buffer)

There are 13 weekdays left before the exam. About 36 h of the budget falls on them, which is roughly **3 h per weekday**. If you get less than that, use the levers below early rather than late.

| Date | Session(s) | Budget | Cumulative |
|---|---|---|---|
| Tue 11-24 | E01 rest + E02 | 3.5 h | 3.5 h |
| Wed 11-25 | E03 | 3 h | 6.5 h |
| Thu 11-26 | E04 | 2.5 h | 9 h |
| Fri 11-27 | M1 + catch-up | 1 h (+ slack) | 10 h |
| **Checkpoint A, Fri 11-27** | **Chapters 1–2 done (E01–E04, M1).** If not, finish them at the weekend and switch to the lean track. | | |
| Sat/Sun 11-28/29 | Buffer (optional) | – | |
| Mon 11-30 | E05 | 3 h | 13 h |
| Tue 12-01 | E06 | 3 h | 16 h |
| Wed 12-02 | E07 | 2.5 h | 18.5 h |
| Thu 12-03 | E08 | 3 h | 21.5 h |
| Fri 12-04 | E09 | 3 h | 24.5 h |
| **Checkpoint B, Fri 12-04** | **Chapter 3 done (E05–E09).** If not, switch to the lean track for the rest. | | |
| Sat 12-05 | M2 (optional weekend slot) | 1 h | 25.5 h |
| Sun 12-06 | Buffer (optional) | – | |
| Mon 12-07 | E10 | 3 h | 28.5 h |
| Tue 12-08 | E11 | 3 h | 31.5 h |
| Wed 12-09 | M3: full mock + official iSAQB mock + review | 3 h | 34.5 h |
| Thu 12-10 | M4 light: weak spots and glossary only; stop early | 2 h | 36.5 h |
| **Fri 12-11** | **Exam** | | |

If M2 doesn't fit at the weekend, do it on Mon 12-07 before E10 (that day becomes 4 h).

### Lean track: if you fall behind

Use these levers in this order. Each one saves time with little exam risk, because it cuts R3 content (not examined) or polishing:

| # | Lever | Saves |
|---|---|---|
| 1 | **Exam-first docs until 12-11:** write results into `docs/` as bullet drafts and polish them after the exam. The exam rewards the thinking, not the prose. | ≈ 30 % of each session |
| 2 | **Skip R3-only steps** (each exercise names them), e.g. E05's DDD/evolutionary/model-based step, E07's R3 pattern scan, E08's deployment principles and distributed systems, E10's long-term impact. | ≈ 30–60 min per exercise |
| 3 | **Merge E07 into E06:** cover only the three R1 patterns (Layers, Pipes and Filters, Microservices) at the end of E06. | ≈ 2 h |
| 4 | **Replace M4 with weak-spot review** of `notes/progress.md`. | ≈ 1 h |
| 5 | **Shorten role-plays** to about 5 minutes per role. | ≈ 20 min per session |

**Don't cut:** E03, E06 and E11 (mostly R1), the exam check at the end of each session, and M3 with the official mock exam.

## Learning-goal coverage

R1 = examinable (must master) · R2 = may be examined · R3 = not examined.

| LG | Title (short) | Level | Exercise |
|---|---|---|---|
| 01-01 | Definitions of software architecture | R1 | E01 |
| 01-02 | Goals and benefits of architecture | R1 | E01 |
| 01-03 | Long-term impact | R3 | E10 |
| 01-04 | Tasks and responsibilities of architects | R1 | E01 |
| 01-05 | Software vs. other architecture domains | R3 | E01 |
| 01-06 | Architects and other stakeholders | R1 | E01 |
| 01-07 | Importance of data and data models | R2 | E09 |
| 02-01 | Stakeholder concerns | R1, R3 | E01, E02 |
| 02-02 | Clarify requirements and constraints | R1–R3 | E02 |
| 02-03 | Qualities of a software system | R1 | E03 |
| 02-04 | Formulate quality requirements (scenarios) | R1–R3 | E03 |
| 02-05 | Explicit statements over implicit assumptions | R1 | E02 (and every session) |
| 03-01 | Fulfilling requirements through architecture | R1 | E05 |
| 03-02 | Design software architectures (black box/white box, refinement) | R1 | E05, E06 |
| 03-03 | Approaches and heuristics (top-down, bottom-up, view-based) | R1, R3 | E05 |
| 03-04 | Design principles | R1–R3 | E06 |
| 03-05 | Feedback loops and risks | R1, R2 | E05 |
| 03-06 | Dependencies and coupling | R1 | E06 |
| 03-07 | Design and define interfaces | R1–R3 | E04 |
| 03-08 | Architectural patterns | R1, R3 | E07 |
| 03-09 | Design patterns | R3 | E07 |
| 03-10 | Cross-cutting concerns | R1 | E09 |
| 03-11 | Deployment principles | R3 | E08 |
| 03-12 | Challenges of distributed systems | R3 | E08 |
| 04-01 | Requirements of technical documentation | R1 | E10 |
| 04-02 | Describe and communicate architectures | R1–R3 | E10 |
| 04-03 | Notations and models (UML and others) | R2–R3 | E08 |
| 04-04 | "Learning Goal not Found" (intentional joke LG) | R3 | — |
| 04-05 | Architectural views | R1 | E04, E06, E08 |
| 04-06 | Document interfaces | R1 | E04 |
| 04-07 | Document cross-cutting concerns | R2 | E09 |
| 04-08 | Architecture decisions and ADRs | R1–R2 | E05, E10 |
| 04-09 | Further resources and tools (arc42, C4, ISO 42010) | R3 | E10 |
| 05-01 | Reasons for architecture analysis | R1 | E11 |
| 05-02 | Analyse qualities (methods, information sources) | R1, R3 | E03, E11 |
| 05-03 | Conformance to architecture decisions | R2 | E11 |
| 06-xx | Examples | not examined | — |
