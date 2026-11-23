# E01: Kick-off: vision, the architect's role, stakeholders

- **Learning goals:** LG 01-01 (R1), 01-02 (R1), 01-04 (R1), 01-05 (R3), 01-06 (R1), 02-01 (R1/R3)
- **Edits:** `docs/arc42/01-introduction-and-goals.md` (sections 1.1 and 1.3)
- **Time:** about 75 min of focused work; block about twice that (see the [timeline](README.md#timeline))

## Goal

Get the vocabulary of chapter 1 into your own words, using your own project, and find out who the stakeholders of a solo hobby project really are.

## Steps

1. **Definition in your own words (LG 01-01).** Write two or three sentences: "The software architecture of the Balance Bot is …". Then check them against the four commonalities in the curriculum: building blocks with interfaces and relationships, building blocks vs. components, structures and cross-cutting concerns and principles, decisions and their consequences.
2. **Where are the boundaries? (LG 01-05).** Classify these as software architecture, hardware/system architecture, or both: choosing the TB6612FNG, splitting work across the two ESP32 cores, the PCB layout, the format of the telemetry messages, using micro-ROS.
3. **Vision and scope.** Write a vision of three to five sentences for the *Balance Bot platform* (firmware, ground station, data lab, optional OTA). Decide what is **out of scope for v1**.
4. **Stakeholder discovery (LG 02-01).** List roles, not people. You hold several roles yourself. Note each role's concerns and what it expects from the architecture or the documentation.
5. **Role-play interviews.** The sparring partner plays two stakeholders; you interview each for about 5 minutes and add what you learn to the table:
   - a **hiring manager** who looks at your portfolio for 5 minutes
   - **you, six months from now**, picking the project up again after a break
6. **The architect's tasks (LG 01-04, 01-06).** Go through the curriculum's list of tasks. For each one, note how it shows up in this project and which are hard to do alone (hint: feedback).
7. **Elevator pitch (LG 01-02).** The sparring partner plays a skeptic who says "it's a hobby robot, just write the code". Convince them in 60 seconds that architecture work pays off here.

## Done when

- Sections 1.1 (requirements overview and vision) and 1.3 (stakeholders) are filled in.
- You can state the four commonalities of the definitions of architecture from memory.

## Notes for the sparring partner

- Push for more than one stakeholder: maintainer, operator at a demo, bystanders (safety), a technical interviewer, possibly open-source users.
- At step 2, steer toward this point: hardware choices are often **constraints** for the software architecture. That links to E02.
- Transfer question idea: the stakeholders of an online insurance portal, and which ones are often forgotten.
