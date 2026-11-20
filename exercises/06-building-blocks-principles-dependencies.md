# E06: Building blocks, design principles and dependencies

- **Learning goals:** LG 03-02 (R1), 03-04 (R1–R3), 03-06 (R1), 04-05 (R1, building-block view)
- **Edits:** `docs/arc42/05-building-block-view.md`
- **Time:** about 90 min. **This is the heaviest R1 session; don't skip it.**

## Goal

Break the system into building blocks, apply the design principles deliberately, and analyse the coupling.

## Steps

1. **Level 1 (white box of the whole system).** Robot firmware, ground station and data lab as black boxes, plus their interfaces (taken from E04).
2. **Level 1 of the firmware.** 5–8 building blocks, each with **one sentence of responsibility** and its interfaces. Example names only: Sensor Acquisition, State Estimation, Balance Control, Motor Control, Safety Supervisor, Comms, Parameter Store.
3. **Black box vs. white box, stepwise refinement (LG 03-02).** Refine one block (e.g. Balance Control or State Estimation) to level 2. Explain why level 1 must stay valid as a black box.
4. **Design principles (LG 03-04).** For each principle, point to a concrete place in your design, or say why it doesn't apply:
   - abstraction / interfaces as abstractions (R2)
   - information hiding, separation of concerns, high cohesion, loose coupling (R1)
   - open/closed: add a new controller without changing the loop (R1)
   - dependency inversion: does the controller depend on the TB6612FNG driver or on an abstraction? (R1)
   - conceptual integrity: do all drivers follow the same pattern? (R2)
   - expect errors / robustness (R2): what if an I²C read fails?
   - KISS, YAGNI, DRY, SOLID, Liskov (R3): one example each, briefly
5. **Dependencies and coupling (LG 03-06).** Draw the dependency graph. For each edge, name the **type**: use/delegation, messaging/events, composition, creation, inheritance, temporal coupling, coupling via data or data types, **coupling via hardware**. Count efferent (outgoing) and afferent (incoming) coupling per block. Which block is the riskiest to change?
6. **Static vs. dynamic coupling.** Explain with your telemetry: if you swap direct calls for publish/subscribe, does the coupling go away? (Curriculum: replacing static with dynamic dependencies doesn't necessarily reduce coupling.)
7. **Consequences for the source code (LG 03-02).** Sketch the folder or component layout that mirrors the building blocks.

## Done when

- Section 5 has level 1 of the system and of the firmware, one level-2 refinement, and a dependency table with the coupling types.
- You can define efferent vs. afferent and static vs. dynamic coupling, and name 5 dependency types without notes.

## Notes for the sparring partner

- R1-heavy session: run 5 exam questions instead of 3.
- If a block's responsibility needs "and" twice, ask about cohesion.
- Transfer question idea: is a shared "Customer" database table between two services coupling? What kind?
