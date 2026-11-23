# E02: Requirements, constraints and explicit assumptions

- **Learning goals:** LG 02-01 (R1), 02-02 (R1–R3), 02-05 (R1)
- **Edits:** `docs/arc42/01-introduction-and-goals.md` (1.1), `docs/arc42/02-constraints.md`, `docs/arc42/09-decisions.md` (decision log), `docs/arc42/11-risks-and-technical-debt.md` (assumptions)
- **Time:** about 90 min of focused work; block about twice that (see the [timeline](README.md#timeline))

## Goal

Separate **requirements**, **constraints** and **assumptions**. Turn the hardware choices you have already made (some taken over from another AI session without much questioning) into documented, justified constraints.

## Steps

1. **Functional requirements.** List the 8–10 most important ones (e.g. balance in place, drive on command, tune live, stream telemetry, log runs, detect a fall and stop the motors, monitor the battery, compare controllers). Prioritise them: must, should, later.
2. **Classify constraints (LG 02-02).** Sort everything in `02-constraints.md` into **technical**, **organisational** and **regulatory/conventions**. Add what's missing: toolchain (ESP-IDF, Arduino or PlatformIO), language, skills, time.
3. **Make the implicit explicit (LG 02-05).** "Not too time- or money-intensive" is an implicit statement. Quantify it: total budget in €, hours per week, and any milestones (e.g. "balancing before …"). Then list every assumption from the hardware-selection session and mark each one *validated*, *plausible* or *unvalidated*.
4. **Retroactive decision review.** For each hardware choice, write one line on **why** it was chosen, and rate how easy it is to reverse (cheap, costly, or a redesign). The TB6612FNG is the first candidate: what *is* the reason?
5. **Interplay of constraints.** Find at least two places where constraints affect each other or a quality (e.g. 12 V motors on a 2S pack; the motor driver's voltage limit vs. a later 3S upgrade). Write these down as **questions to check**, not as facts.
6. **Short-term vs. long-term conflicts (LG 02-01).** Find two (e.g. cheap N20 motors now vs. torque headroom later; micro-ROS now vs. a custom protocol). Who decides, and when?
7. **Concerns that don't become requirements (LG 02-01, R3).** Name one concern that stays a concern rather than a requirement.

## Done when

- `02-constraints.md` has every constraint classified, quantified and given a source or reason.
- The decision log in `09-decisions.md` has one line per hardware choice, including its reversibility.
- The unvalidated assumptions are recorded as risks in `11-…`.

## Notes for the sparring partner

- Don't give hardware answers. Ask: "What is the supply range of the pack from full to empty? What does that mean for a 12 V motor? Where would you look this up?"
- Name Conway's law (R2) briefly: a solo developer means a single team, so what does Conway predict here? (Hint: not much. Ask why the law is still worth knowing.)
- Regulatory constraints (R2) here: battery safety, radio equipment. Keep this light.
- Transfer question idea: constraints in a bank's payment system (regulation, legacy core banking, team structure).
