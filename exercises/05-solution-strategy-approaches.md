# E05: Solution strategy, design approaches and iterations

- **Learning goals:** LG 03-01 (R1), 03-02 (R1), 03-03 (R1/R3), 03-05 (R1/R2), 04-08 (R1/R2, first ADR)
- **Edits:** `docs/arc42/04-solution-strategy.md`, `docs/adr/0001-*.md`
- **Time:** about 90 min

## Goal

Derive the fundamental architectural approach from the quality goals and constraints. Plan the iterations that reduce the biggest risks first.

## Steps

1. **Pick an approach (LG 03-03).** Top-down, bottom-up, or both? The hardware is already chosen; what does that do to your approach? Explain view-based development. For R3 awareness, say in one sentence each where DDD, evolutionary architecture and model-based design (familiar from controls) could fit.
2. **Quality goals → approaches (LG 03-01).** Fill a table: *quality goal | architectural approach or decision | what it costs (trade-off) | risk*. For example: timing determinism, swapping controllers, testability without hardware, observability.
3. **Separate domain from technical (LG 03-02).** What is the *domain* of a balance robot (state estimation, control law, robot model, operating modes)? What is *technical* (ESP-IDF, FreeRTOS, drivers, Wi-Fi stack, micro-ROS)? Why separate them, and what does that mean for the source code?
4. **Feedback loops and risks (LG 03-05).** List your top 3–5 technical risks. Plan **spikes or iterations** that address them in order of risk. Example: "Spike 1: read the IMU and encoders at 500 Hz on core 1 while streaming telemetry from core 0; measure jitter." What feedback does each one give you, and from whom?
5. **First ADR (LG 04-08).** Decide *micro-ROS vs. a lightweight custom protocol* for robot ↔ ground station (or take a different open question if you prefer). Use the template in `docs/adr/0000-template.md`. List the alternatives, the decision, the consequences, and which quality goals it serves.

## Done when

- Section 4 has the approach, the goal→approach table, the domain/technical split and the iteration plan.
- ADR-0001 exists with the status *accepted* or *proposed*.

## Notes for the sparring partner

- Challenge micro-ROS against the low time and money constraint: learning curve, extra agent process, debugging effort, compared with portfolio value and the path to ROS 2 later. Make the user weigh it; don't decide for them.
- Link to LG 03-05: deciding *later* is a legitimate option when uncertainty is high. Ask what the last responsible moment for this decision is.
- Transfer question idea: why an iterative approach reduces risk when migrating a legacy insurance system.
