# E10: Architecture decisions and documentation for audiences

- **Learning goals:** LG 04-08 (R1/R2), 04-01 (R1), 04-02 (R1–R3), 04-09 (R3), 01-03 (R3)
- **Edits:** `docs/adr/`, `docs/arc42/09-decisions.md`, `docs/arc42/12-glossary.md`, `README.md`
- **Time:** about 90 min

## Goal

Document decisions systematically, write for specific audiences, and test the documentation against those audiences.

## Steps

1. **More ADRs (LG 04-08).** Review ADR-0001. Write 2–3 more, including at least one *retroactive* ADR for a hardware choice (e.g. TB6612FNG or MPU-6050). Be honest: "decided with limited analysis; reviewed on …".
2. **Interdependencies between decisions.** Draw or list them: e.g. ESP32-S3 → micro-ROS is possible → agent runs on the laptop → deployment view. What happens to the chain if one decision changes?
3. **Requirements for documentation (LG 04-01).** Understandability, correctness, efficiency, appropriateness, maintainability. Only the target audience can judge understandability, so:
4. **Audience review (role-play).** The sparring partner reviews your docs as:
   - **a hiring manager with 5 minutes:** what do they read, and what do they take away?
   - **a firmware developer joining the project:** can they find where to add a new sensor?
   Adapt the README or section 1 based on the feedback.
5. **Templates and frameworks (LG 04-02, 04-09).** Benefits of template-based documentation. What are arc42, C4 and ISO/IEC/IEEE 42010, and how do they differ (template vs. model/notation vs. standard of concepts)?
6. **Long-term impact (LG 01-03, R3).** Which decisions would break under these changes: moving to a 3S pack, a new IMU, an SBC with ROS 2?
7. **Glossary.** Fill section 12, with German terms in brackets for exam vocabulary.

## Done when

- At least 3 ADRs exist and are linked from section 9.
- The README has a short portfolio-ready summary.
- The glossary has 20 or more entries.

## Notes for the sparring partner

- In the audience review, give concrete and slightly uncomfortable feedback; don't be polite.
- Transfer question idea: which documentation is appropriate for a 3-person startup vs. a regulated medical-device company?
