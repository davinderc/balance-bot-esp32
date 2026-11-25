# 11. Risks and Technical Debt

> Exercises: **E02** (unvalidated assumptions), **E05** (top technical risks, iteration plan), **E11** (results of the assessment).

## 11.1 Candidate risks: questions raised during project setup (to discuss in E02, not yet verified)

These are **questions**, not findings. Check each one against the datasheets and your own measurements, then keep it, rephrase it or delete it.

| ID | Candidate risk / question | Related |
|---|---|---|
| CR-1 | The 12 V-rated N20 motors run from 2S (well below 12 V). How much speed and torque headroom is left for recovering from a push? | TC-2, TC-4 |
| CR-2 | Small gear motors often have noticeable gearbox backlash. How does that affect balance control? | TC-2 |
| CR-3 | Is the TB6612FNG's motor-supply limit compatible with a later 3S pack at full charge? Is its current rating enough for the N20 stall current? (Partly answered in E02: see AS-4, AS-5.) | TC-3, TC-4 |
| CR-4 | Battery voltage changes as the pack discharges, so the motor gain changes too. Does the controller need to compensate (e.g. using INA219 or ADC readings)? | TC-4, TC-6 |
| CR-5 | Is the MPU-6050 still in production? Clone quality varies. | TC-7 |
| CR-6 | Can 200–500 Hz control on one core coexist with Wi-Fi and micro-ROS on the other without timing jitter? (Unvalidated assumption from the hardware session.) | TC-1, D-9 |
| CR-7 | micro-ROS adds a learning curve and an extra agent process on the host. Does that fit the low-time constraint? | D-9, OC-3 |

## 11.1a Assumptions (E02)

Status: **validated** = checked against a source or a measurement; **plausible** = reasoned, not checked; **unvalidated** = taken over, no check. Unvalidated assumptions are risks until checked.

| ID | Assumption | Status | Evidence / source | Related |
|---|---|---|---|---|
| AS-1 | The control-loop computation (sensor fusion + PID) fits well within one period at 200–500 Hz (2–5 ms). | plausible | Forum figures from other projects: ~160 µs for a 6-axis complementary filter, ~600 µs for a 9-DOF EKF; flight controllers run PID + gyro at 2–8 kHz. Not measured on this hardware. Note: a FreeRTOS tick of ~1 ms (default to verify, `CONFIG_FREERTOS_HZ`) is too coarse to time the loop with `vTaskDelay`; a hardware timer (GPTimer or esp_timer) is the likely approach → E05/E08. | CR-6, TC-1 |
| AS-2 | The Wi-Fi/BT tasks can be pinned to core 0 by configuration; core 0 is the default. | validated | [ESP-IDF API guide: built-in task priorities](https://docs.espressif.com/projects/esp-idf/en/stable/esp32s3/api-guides/performance/speed.html#built-in-task-priorities) | TC-1, TC-10 |
| AS-3 | During flash writes the cache is disabled, so code running from flash stalls on both cores; code and data in IRAM/DRAM keep running. | validated | [ESP-IDF API reference: SPI flash concurrency](https://docs.espressif.com/projects/esp-idf/en/stable/esp32s3/api-reference/peripherals/spi_flash/spi_flash_concurrency.html). Opens a design option: a control path entirely in IRAM could keep running during flash writes, at the cost of a constraint on all code on that path → E05/E09. | F-15 |
| AS-4 | N20 motors rated for 12 V have enough speed and torque headroom on 2S. | plausible | Linear scaling from the motor datasheet: ~106 rpm at 6.4 V (empty), 120–140 rpm at 7.4–8.4 V; torque ~60–70 % of the rated 1.2 kg·cm. Headroom may be too small. Fallbacks: 3S pack or different wheel size (knock-on effects → step 5). | CR-1, TC-2, TC-4 |
| AS-5 | The TB6612FNG's current rating covers the N20 current. | plausible (tight) | [Toshiba TB6612FNG datasheet](https://toshiba.semicon-storage.com/info/TB6612FNG_datasheet_en_20141001.pdf?did=10660&prodName=TB6612FNG): 1.2 A per channel continuous; 2 A peak (20 ms pulse, < 20 % duty); 3.2 A single 10 ms pulse. Motor max current 1.1 A (stall current? to clarify). Margin is small. Protection against back-EMF spikes may need extra components [HW]. | CR-3, TC-3 |
| AS-6 | The MPU-6050 (or a clone) is accurate enough for balancing (pitch and pitch rate, with a complementary or Kalman filter). | plausible | Outdated part, but used successfully in similar balancing robots, e.g. [arXiv 2609.36091](https://arxiv.org/html/2609.36091v1). Not measured on this hardware. | CR-5, TC-7 |
| AS-7 | Gearbox backlash is small enough for balance control. | unvalidated | Needs a measurement of the play with wheels attached, which needs a printed wheel/axle adapter first. | CR-2, TC-2, TC-8 |
| AS-8 | The 21700 cells from the old power bank are healthy (capacity, internal resistance) and safe to reuse. | plausible | The power bank's control circuit appeared to have failed, not the cells. Not measured. Fallback: 18650 cells on hand (needs holders) or a new pack. | TC-4, RC-1 |
| AS-9 | LLM assistance bridges the C/C++ and ESP-IDF/FreeRTOS skill gaps in acceptable time. | unvalidated | Some support: new tech stacks learned before without LLM help; datasheet reading from control-engineering work with Arduino MCUs. | OC-6, D-10 |
| AS-10 | The wireless link is stable enough that the link-loss timeout rarely triggers. | unvalidated | Needs a test. | F-8 |
| AS-11 | Telemetry and logs are enough to debug the running control loop. | plausible | Reasoned in E01/E02 (breakpoints halt the loop; a cable changes the dynamics). | §1.1 |
| AS-12 | Documentation for basic ESP-IDF tasks (I²C, PWM) is easy to find, so the D-10 fallback trigger (2 evenings) is realistic. | plausible | ESP-IDF is described as well documented but dense ([comparison](https://hubble.com/community/comparisons/esp-idf-vs-arduino-framework-for-esp32-when-to-switch-and-why/), [production article](https://productionesp32.com/posts/prodesp2-use-esp-idf/)). The first source suggests starting with Arduino for a project like this one. TODO(E02): does this change D-10? | D-10 |
| AS-13 | Wi-Fi activity on core 0 causes no harmful timing jitter on the control loop on core 1. | unvalidated | Needs a measurement on the dev board, with Wi-Fi off and with telemetry streaming → spike in E05, TODO(E11). | CR-6, TC-1 |

## 11.2 Risks (assessed)

| ID | Risk | Probability | Impact | Mitigation | Status |
|---|---|---|---|---|---|
| | TODO(E05/E11) | | | | |

## 11.3 Technical debt

| ID | Debt | Why accepted | Repayment plan |
|---|---|---|---|
| | TODO(E11) | | |
