# E08: Runtime view, deployment view, notations and distribution

- **Learning goals:** LG 04-05 (R1), 04-03 (R2/R3), 03-11 (R3), 03-12 (R3)
- **Edits:** `docs/arc42/06-runtime-view.md`, `docs/arc42/07-deployment-view.md`
- **Time:** about 90 min

## Goal

Describe the dynamic behaviour and the mapping onto hardware, choosing the right notation for each.

## Steps

1. **Runtime scenarios.** Document three, each in a different notation, and justify the choice:
   - **one control-loop tick:** sequence diagram (timer → sensors → estimation → controller → motors → telemetry buffer)
   - **startup and calibration:** activity diagram or numbered list
   - **operating modes:** state machine (e.g. IDLE, CALIBRATING, BALANCING, FALLEN, LOW_BATTERY, FAULT) with the transitions and their triggers
2. **Notations (LG 04-03).** Quiz yourself: which UML diagram for which purpose? Class, package, component, deployment, sequence and activity are R2; composite structure and state machine are R3. Alternatives (R3): C4, **SysML** (relevant for mechatronics), ArchiMate, ER diagrams, BPMN.
3. **Deployment view.** Nodes (ESP32-S3, laptop, storage for the data lab), channels (Wi-Fi, USB), artifacts (firmware image, ground-station app, micro-ROS agent, notebooks or scripts). Map building blocks → artifacts → nodes. Are the two ESP32 cores separate *nodes*? Discuss.
4. **Deployment principles (LG 03-11, R3).** For each, how this project meets it: automated deployment, repeatable builds, consistent environments, everything under version control, releases that are easy to undo. (Hint: the ESP32 OTA dual-partition rollback.)
5. **Distributed-system challenges (LG 03-12, R3).**
   - Communication fails: Wi-Fi drops while balancing. What must happen?
   - Ordering of events: robot timestamps vs. laptop timestamps in the data lab.
   - Split-brain: two ground stations sending commands.

## Done when

- Section 6 has the three scenarios.
- Section 7 has the deployment diagram, the mapping table and the deployment principles.

## Notes for the sparring partner

- Check that the runtime scenarios use the building-block names from section 5 (consistency, LG 04-02).
- Most of this session is R2/R3, so keep the exam questions on views (R1) and UML diagram purposes (R2).
- Transfer question idea: the deployment view of a web application with a load balancer, two app servers and a database.
