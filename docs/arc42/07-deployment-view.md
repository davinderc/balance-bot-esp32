# 7. Deployment View

> Exercise: **E08**. Nodes, channels, artifacts; mapping of building blocks → artifacts → nodes.

## 7.1 Infrastructure (nodes and channels)

Known hardware so far (see section 2). The diagram and channels are TODO(E08).

| Node | Hardware | Runs (artifacts) |
|---|---|---|
| Robot controller | ESP32-S3 dev board (8 MB flash, 8 MB PSRAM) | TODO(E08): firmware image |
| Sensors and actuators (not software nodes; discuss in E04/E08) | MPU-6050, INA219 (I²C); TB6612FNG + 2× N20 with encoders | – |
| Host | Laptop | TODO(E08): ground station, micro-ROS agent?, data lab |

| Channel | Between | Technology |
|---|---|---|
| TODO(E08) | | |

## 7.2 Mapping of building blocks to artifacts and nodes

TODO(E08)

## 7.3 Deployment principles (LG 03-11)

TODO(E08): automated deployment, repeatable builds, consistent environments, version control, releases that are easy to undo.
