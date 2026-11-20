# 11. Risks and Technical Debt

> Exercises: **E02** (unvalidated assumptions), **E05** (top technical risks, iteration plan), **E11** (results of the assessment).

## 11.1 Candidate risks: questions raised during project setup (to discuss in E02, not yet verified)

These are **questions**, not findings. Check each one against the datasheets and your own measurements, then keep it, rephrase it or delete it.

| ID | Candidate risk / question | Related |
|---|---|---|
| CR-1 | The 12 V-rated N20 motors run from 2S (well below 12 V). How much speed and torque headroom is left for recovering from a push? | TC-2, TC-4 |
| CR-2 | Small gear motors often have noticeable gearbox backlash. How does that affect balance control? | TC-2 |
| CR-3 | Is the TB6612FNG's motor-supply limit compatible with a later 3S pack at full charge? Is its current rating enough for the N20 stall current? | TC-3, TC-4 |
| CR-4 | Battery voltage changes as the pack discharges, so the motor gain changes too. Does the controller need to compensate (e.g. using INA219 or ADC readings)? | TC-4, TC-6 |
| CR-5 | Is the MPU-6050 still in production? Clone quality varies. | TC-7 |
| CR-6 | Can 200–500 Hz control on one core coexist with Wi-Fi and micro-ROS on the other without timing jitter? (Unvalidated assumption from the hardware session.) | TC-1, D-9 |
| CR-7 | micro-ROS adds a learning curve and an extra agent process on the host. Does that fit the low-time constraint? | D-9, OC-3 |

## 11.2 Risks (assessed)

| ID | Risk | Probability | Impact | Mitigation | Status |
|---|---|---|---|---|---|
| | TODO(E05/E11) | | | | |

## 11.3 Technical debt

| ID | Debt | Why accepted | Repayment plan |
|---|---|---|---|
| | TODO(E11) | | |
