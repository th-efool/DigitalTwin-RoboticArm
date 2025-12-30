# Unity Robotic Arm Digital Twin

![Status](https://img.shields.io/badge/status-active%20development-yellow.svg)
![Engine](https://img.shields.io/badge/engine-Unity-black.svg)
![Domain](https://img.shields.io/badge/domain-robotics%20%7C%20digital%20twin-blue.svg)
![Realtime](https://img.shields.io/badge/sync-real--time-success.svg)
![Integration](https://img.shields.io/badge/integration-realvirtual.io-informational.svg)
![Platform](https://img.shields.io/badge/platform-PC-lightgrey.svg)

---

## Overview

**Unity Robotic Arm Digital Twin** is a real-time synchronization system that mirrors a physical robotic arm inside **Unity** with a one-to-one correspondence between hardware state and virtual representation.

The system streams live telemetry—such as joint angles, encoder values, velocities, or end-effector poses—from the physical robot and applies them directly to a virtual arm model in Unity.  
The result is a **low-latency digital twin** suitable for visualization, simulation, diagnostics, and remote monitoring.

This project is intended for **robotics development workflows**, not as a game-oriented animation system.

---

## Core Capabilities

- Real-time joint-level synchronization between physical and virtual arm
- Deterministic mapping of sensor data to Unity transforms
- Support for multiple communication backends (Serial, WebSocket, MQTT)
- Hardware-agnostic data pipeline (robot controller–independent)
- Modular joint and kinematic mapping layer
- Designed for extension into simulation, control feedback, or validation loops

---

## System Architecture

```

Physical Robotic Arm
(sensors, encoders, controller firmware)
│
│ telemetry (joint states)
▼
Communication Bridge
(Serial / WebSocket / MQTT)
│
│ structured packets (JSON / binary)
▼
Unity Receiver Layer

* Packet parsing
* Coordinate normalization
* Joint-to-bone mapping
* Transform updates
  │
  ▼
  Virtual Robotic Arm (Unity Scene)

```

The Unity scene reflects the physical arm’s motion continuously, with no pre-baked animation or keyframing.

---

## realvirtual.io Integration

This project is built on top of **realvirtual.io** (formerly *Game4Automation*), with **significant internal overrides and extensions**.

### Key Integration Details

- The required `realvirtual.io` prefab is present at the **root of the scene hierarchy**
- The `RealvirtualController` is retained for compatibility and scene-level configuration
- Core realvirtual behaviors are selectively bypassed to allow:
  - Custom telemetry ingestion
  - Direct joint control from external hardware
  - Deterministic transform updates instead of simulation-driven motion

### Why realvirtual.io

realvirtual.io provides:
- A structured industrial simulation baseline
- Scene validation and lifecycle management
- Scalable unit handling (mm ↔ Unity units)
- Runtime UI and tooling

This project **does not rely on default realvirtual motion logic** and instead uses it as an infrastructure layer rather than a closed simulation framework.

---

## Design Philosophy

- **Hardware-first**: Unity mirrors reality, not the other way around
- **Event-driven updates** instead of frame-based polling
- **Minimal abstraction** between telemetry and joint motion
- **Deterministic behavior** suitable for debugging and analysis
- **Extensible architecture** for future feedback/control loops

---

## Use Cases

- Robotics visualization and demos
- Remote monitoring of robotic systems
- Operator training with live hardware
- Validation of kinematics and motion envelopes
- Digital twin foundations for Industry 4.0 workflows

---

## Notes

- Communication backend is configurable and replaceable
- Joint mapping assumes consistent coordinate conventions between hardware and Unity
- Project is structured for expansion into bidirectional control, but currently focuses on **hardware → Unity synchronization**

---

## Credits

Built using **Unity** and **realvirtual.io**, with internal systems extended and overridden to support real-time robotic digital twin behavior.
```

