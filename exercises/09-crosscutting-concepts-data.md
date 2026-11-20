# E09: Cross-cutting concepts and data models

- **Learning goals:** LG 03-10 (R1), 04-07 (R2), 01-07 (R2)
- **Edits:** `docs/arc42/08-crosscutting-concepts.md`
- **Time:** about 90 min

## Goal

Find the concerns that affect many building blocks, solve them once and consistently, and model the key data independently of how it is stored or sent.

## Steps

1. **Identify cross-cutting concerns (LG 03-10).** Brainstorm, then pick the relevant ones. Candidates: error handling and safety, concurrency (two cores, interrupts, shared data), configuration and parameter management (tuning values, calibration stored in NVS), logging and telemetry, time and units, testing (host unit tests, simulation, hardware-in-the-loop), energy efficiency (battery), security (Wi-Fi credentials, OTA signing), build and deployment.
2. **Design three concepts in depth.** Suggested: **error handling and safety**, **parameter management**, **telemetry and logging**. For each, write the problem, the solution, rules every building block must follow, and an example.
3. **Interdependencies (LG 03-10).** Where do concepts interact or conflict? (Telemetry vs. concurrency vs. timing; parameter changes at runtime vs. safety.)
4. **Data models (LG 01-07).**
   - Identify the data models that affect the architecture: telemetry sample, run/session metadata, parameter set, robot state.
   - **Products vs. sums:** model `TelemetrySample` as a product (record) and `RobotState` as a sum (e.g. `Idle | Balancing{…} | Fallen{reason}`). Why does this distinction matter?
   - **Decouple the model from its representation:** in-memory struct vs. wire format (CBOR, protobuf, or ROS messages) vs. storage in the data lab (CSV, Parquet, or a database).
   - The impact of data on decisions: storage size per run, rate, reliability of logging.
5. **Document and communicate (LG 04-07).** Who has to know each concept? How do you make sure your future self follows it (README section, code template, lint rule)?

## Done when

- Section 8 has at least three fully described concepts and a data-model section.

## Notes for the sparring partner

- Ask the user to explain *why* this is cross-cutting rather than just another building block.
- Transfer question idea: the cross-cutting concepts of a multi-tenant SaaS application (authentication, multi-tenancy, i18n, auditing).
