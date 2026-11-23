# E07: Architectural and design patterns

- **Learning goals:** LG 03-08 (R1/R3), 03-09 (R3); revisits 03-06 (dependency injection)
- **Edits:** `docs/arc42/04-solution-strategy.md` and `docs/arc42/05-building-block-view.md` (mark the patterns used); optionally an ADR
- **Time:** about 75 min of focused work; block about twice that (see the [timeline](README.md#timeline))

## Goal

Explain the three R1 patterns with confidence, recognise the R3 patterns, and use patterns as a means to qualities rather than for their own sake.

## Steps

1. **The R1 patterns.** For each of **Layers**, **Pipes and Filters** and **Microservices**: the structure, the qualities it supports, its typical drawbacks, and *where it fits or doesn't* in the Balance Bot platform. (Is the IMU → calibration → filter → angle chain pipes and filters? Strict or relaxed layers in the firmware? Why are microservices wrong on an MCU, and would they be right for the data lab?)
2. **R3 architectural patterns: quick scan.** For each, one sentence and a possible use or non-use: Ports and Adapters (simulation vs. real hardware), Plugin (controllers), Blackboard, Broker and messaging (what is micro-ROS/DDS?), MVC/MVVM/MVU (ground station UI), CQRS and event sourcing (data lab run logs?), dependency injection, RPC, SOA.
3. **Design patterns (R3).** Map to concrete places: Strategy (controller algorithm), Observer (telemetry), Adapter (MPU-6050 behind an IMU interface), Facade (motor subsystem), Proxy, Template Method (control-loop skeleton).
4. **Compare alternatives.** Problem: get data from the hard-real-time control loop (core 1) to telemetry (core 0) without disturbing the loop's timing. Compare at least two of: a shared double buffer, a FreeRTOS queue, a lock-free ring buffer, publishing directly from the loop. Evaluate against your scenarios from E03.
5. **Patterns are means to qualities (LG 03-08).** For each pattern you actually use, state which quality goal it serves.

## Done when

- Sections 4 and 5 name the patterns used, with the reason each one is used.
- You can explain Layers, Pipes and Filters and Microservices, including their drawbacks, without notes.

## Notes for the sparring partner

- Exam traps: confusing *layers* (logical) with *tiers* (physical); claiming microservices automatically improve performance; claiming pipes and filters suit interactive, stateful workflows.
- Transfer question idea: which pattern fits an ETL pipeline, a plugin-based IDE, or a large e-commerce platform with independent teams?
