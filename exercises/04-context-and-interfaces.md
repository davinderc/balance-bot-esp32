# E04: System context and interfaces

- **Learning goals:** LG 04-05 (R1, context view), 03-07 (R1–R3), 04-06 (R1)
- **Edits:** `docs/arc42/03-context-and-scope.md`
- **Time:** about 75 min

## Goal

Draw the system boundary on purpose, tell the business context apart from the technical context, and design and document one interface properly.

## Steps

1. **Draw the system boundary.** Is the ground station inside or outside the system? The micro-ROS agent? The data lab? Argue both sides, then decide and record the reason.
2. **Business context.** Treat the system as a black box. Draw the neighbours (users, external systems, the physical environment) and what flows between them in domain terms (e.g. "drive command", "tuning parameters", "run log").
3. **Technical context.** The same neighbours, now with channels and protocols: USB serial/JTAG, Wi-Fi (UDP or TCP?), I²C to the IMU and INA219, PWM and GPIO to the motor driver, encoder pulses. Are hardware devices *neighbours* of the software system? Decide.
4. **Classify each interface (LG 03-07, R3 list).** Local or remote, sync or async, binary or textual, stateful or stateless, point-to-point or multicast, request/response or streaming.
5. **Design one interface in depth (LG 03-07, R1).** Take the **tuning and telemetry interface** between the robot and the ground station. Make it:
   - easy to learn, use and extend
   - hard to misuse (units, ranges, what happens with a bad value, versioning)
   - functionally complete for its users
6. **Internal vs. external (R2).** Why should this interface be treated differently from the internal interface between the control loop and the motor driver code?
7. **Document it (LG 04-06).** Use a fixed structure: purpose, participants, operations or messages, data with units and ranges, quality properties (rate, latency), error handling, versioning, an example.

## Done when

- Section 3 has the system boundary decision, the business context, the technical context with a mapping table, and the interface specification.

## Notes for the sparring partner

- If the user jumps straight to micro-ROS topics, ask what the interface looks like **independent** of the transport. That separates the interface from its implementation (LG 03-07, R1).
- Ask "what happens if a client sends Kp = 10000?" to test "hard to misuse".
- Transfer question idea: the business vs. technical context of a hotel booking system with a payment provider.
