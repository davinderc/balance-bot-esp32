# E11: Architecture analysis and assessment

- **Learning goals:** LG 05-01 (R1), 05-02 (R1/R3), 05-03 (R2)
- **Edits:** `docs/arc42/10-quality-requirements.md`, `docs/arc42/11-risks-and-technical-debt.md`
- **Time:** about 90 min of focused work; block about twice that (see the [timeline](README.md#timeline))

## Goal

Assess your own architecture against your own scenarios and choose a suitable analysis method for each quality.

## Steps

1. **Reasons for analysis (LG 05-01).** Name the four reasons in the curriculum. Which ones apply to this project now, before any code is written?
2. **Scenario-based analysis (ATAM-lite; ATAM itself is R3).** Take 5 scenarios from section 10. For each, walk through the architecture: which decisions support it? Record:
   - **risks** (decisions that may make the scenario fail)
   - **non-risks**
   - **sensitivity points** (where a small change affects the quality strongly)
   - **trade-off points** (decisions that affect several qualities in opposite directions)
3. **Analysis method per quality (LG 05-02).** For each scenario, check that its analysis method fits: acceptance test, quantitative runtime measurement (e.g. loop jitter via a GPIO toggle and a logic analyser), qualitative evaluation, scenario walkthrough, coupling metrics (incoming and outgoing dependencies), cost-benefit (R3).
4. **Sources of information (LG 05-02).** Which ones will you have, and when? Requirements, architecture docs, models, source code, code metrics (LOC, cyclomatic complexity), tests, error clusters, runtime logs, revision history (R3).
5. **Conformance (LG 05-03).** How will you check that the code keeps to your layers and dependency rules? (Code reviews; tool support such as the build system's declared component dependencies in ESP-IDF; dependency-graph tools.)
6. **Update risks and technical debt.** Move what you found into section 11, prioritised.

## Done when

- Section 10 shows the analysis method per scenario.
- Section 11 has prioritised risks with mitigations, plus a technical-debt list.

## Notes for the sparring partner

- Exam traps: "metrics alone are enough to assess architecture"; "analysis is only possible after implementation"; confusing sensitivity points with trade-off points.
- Transfer question idea: how to assess whether a monolith's code still follows its intended layering.
