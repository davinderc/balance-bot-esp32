# E03: Quality goals, quality tree and quality scenarios

- **Learning goals:** LG 02-03 (R1), 02-04 (R1–R3); preview of 05-02 (R1)
- **Edits:** `docs/arc42/01-introduction-and-goals.md` (1.2), `docs/arc42/10-quality-requirements.md`
- **Time:** about 90 min

## Goal

Formulate measurable quality requirements as scenarios, name the trade-offs between them, and say how each one would be checked.

## Steps

1. **Two meanings of "quality" (LG 02-03).** Explain "quality as excellence" vs. "quality as a property of a system". Which one does the exam mean?
2. **Brainstorm using a taxonomy.** Go through ISO 25010 (and/or the arc42 Q42 model) and note which characteristics matter for the robot. The robot has a physical **safety** side, so think about where safety belongs.
3. **Top 3–5 quality goals.** Prioritise them and write them into section 1.2. Each goal gets one sentence of motivation.
4. **Quality tree.** Build a tree: characteristic → refinement → scenario IDs.
5. **Write scenarios (LG 02-04).** Write 8–10, each with **context/environment, stimulus (with source), response and measurement**. Mix the types:
   - **usage scenarios** (e.g. a push while balancing)
   - **change scenarios** (e.g. swap the IMU, add a new controller)
   - **failure/stress scenarios** (e.g. telemetry link drops, battery runs low, robot falls)
6. **Analysis method per scenario (LG 02-04 → 05-02).** Add a column for how each would be verified: runtime measurement, acceptance test, scenario walkthrough, metrics, and so on.
7. **Trade-offs (LG 02-03).** Find at least three conflicts between your scenarios. The curriculum names *configurability vs. reliability*; live tuning makes that one very real here. What else? (Telemetry rate vs. loop timing? OTA security vs. ease of use?)
8. **Goodhart's law (R2/R3).** Which of your measurements would turn bad if it became a target? (E.g. "loop runs at 1 kHz".)

## Done when

- Section 1.2 has 3–5 prioritised quality goals.
- Section 10 has a quality tree and at least 8 complete scenarios, each with an analysis method.
- You can write a scenario with all its parts from memory, for an arbitrary system.

## Notes for the sparring partner

- Reject vague responses ("quickly", "robust"). Insist on numbers or an observable outcome, even if the number is a first guess marked "to verify".
- Check that change scenarios have a measurement too (effort, number of modules touched).
- Transfer question idea: a performance scenario and a modifiability scenario for an online shop's checkout.
