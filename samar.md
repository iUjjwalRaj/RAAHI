# 2. Samar Kumar

## **Role: Team Lead & AI/ML Engineer**

### Primary Responsibility

Samar Kumar served as the **Team Lead and AI/ML Engineer** for RAAHI.

His role combines two important responsibilities:

1. **Team-level leadership and coordination**, ensuring that the different parts of the project remain aligned with the SIH problem statement and the team's overall objective.
2. **AI/ML engineering**, particularly around the computer-vision and machine-learning components that form the intelligence layer of RAAHI-Edge.

While Ujjwal's role covers the overall system architecture and cross-layer technical integration, Samar's technical responsibility is primarily concentrated around the **AI/ML side of the system** and his role in coordinating the team.

---

# 2.1 Team Leadership

As **Team Lead**, Samar is responsible for helping coordinate the six-member team throughout the development of RAAHI.

RAAHI is not a single-module project. It contains:

```text
Android Sensing
       ↓
Edge AI
       ↓
Backend
       ↓
Database
       ↓
GIS Dashboard
       ↓
Testing & Demonstration
```

Samar's leadership role exists across these different areas, helping ensure that individual contributions remain connected to the overall project objective.

His team-level responsibilities include:

- Coordinating team members
- Helping divide responsibilities
- Keeping development aligned with the SIH problem statement
- Participating in technical discussions
- Helping coordinate integration between different contributors
- Supporting project planning
- Helping prepare the team for demonstrations and evaluation
- Maintaining the team's overall development direction

The distinction between his role and Ujjwal's is important:

> **Samar leads the team and owns the AI/ML responsibility, while Ujjwal owns the overall technical architecture and system integration.**

This gives the project both a **team leadership layer** and a **technical architecture layer**.

---

# 2.2 AI/ML Engineering

Samar's primary technical domain within RAAHI is the **AI/ML and computer-vision pipeline**.

The AI system operates primarily on RAAHI-Edge rather than directly on the Android device.

The general processing pipeline is:

```text
Camera Stream
      ↓
RTSP
      ↓
RAAHI-Edge
      ↓
Frame Processing
      ↓
YOLO11n
      ↓
Object Detection
      ↓
ByteTrack
      ↓
Object Tracking
      ↓
Traffic / Event Analytics
```

This architecture allows the Android phone to concentrate on sensing and streaming while the computationally heavier AI workload is handled by the Edge machine.

---

# 2.3 YOLO11n-Based Detection

Samar's AI/ML responsibility centers around the use of **YOLO11n-based computer vision** within RAAHI-Edge.

The system uses computer vision to interpret the video captured from the public-transport vehicle.

Important detection areas include:

### Pothole Detection

The pothole detection pipeline is intended to identify road-surface defects from the vehicle's camera stream.

A detection can subsequently become part of a structured RAAHI event containing information such as:

- Detection type
- Confidence
- Timestamp
- GPS position
- Vehicle identity
- Evidence reference

This is what turns a visual AI prediction into useful road-intelligence data.

---

### Vehicle Detection

The Edge pipeline also performs vehicle detection.

Vehicle detections form the foundation for additional transport analytics, including:

- Vehicle counting
- Traffic-density estimation
- Occupancy-style measurements
- Tracking
- Multi-frame analysis

---

# 2.4 ByteTrack Integration

Detection alone does not tell the system whether the same vehicle appearing in consecutive frames is actually one vehicle.

For this reason, RAAHI incorporates **ByteTrack** into the Edge pipeline.

The conceptual flow is:

```text
Frame 1
 ├── Vehicle A
 ├── Vehicle B
 └── Vehicle C

        ↓ ByteTrack

Frame 2
 ├── Vehicle A → same track
 ├── Vehicle B → same track
 └── Vehicle C → same track
```

Tracking allows RAAHI to maintain object identity across frames.

This is particularly useful for traffic analysis because the system can reason about tracked objects rather than treating every individual frame detection as an entirely new observation.

---

# 2.5 AI Output to Transport Intelligence

An important part of Samar's AI/ML responsibility is connecting computer-vision outputs to the broader RAAHI intelligence pipeline.

The model is not treated as the final product.

Instead:

```text
AI Detection
      +
Object Tracking
      +
GPS
      +
Timestamp
      +
Vehicle Identity
      ↓
Structured Observation
      ↓
RAAHI Event
```

This distinction is important.

RAAHI is not simply:

> "We trained a YOLO model that detects potholes."

It is intended to transform those detections into **geographically and temporally meaningful transport observations**.

---

# 2.6 Traffic Intelligence

Vehicle detection and tracking are also used as inputs to RAAHI's traffic-analysis functionality.

The system can derive traffic-related information from the number and movement of tracked vehicles in the camera stream.

The Edge layer incorporates measurements related to:

- Vehicle density
- Occupancy-style analysis
- Vehicle-per-minute observations
- Traffic conditions
- Multi-bus observations

These measurements can subsequently be correlated with geographic and temporal information in the Central layer.

---

# 2.7 Multi-Bus Intelligence

One of the broader objectives of RAAHI is to use **multiple public-transport vehicles as distributed sensing nodes**.

This changes the problem from:

```text
One camera → one observation
```

to:

```text
Bus A ──┐
Bus B ──┤
Bus C ──┼──→ RAAHI Central → Urban Intelligence
Bus D ──┤
Bus E ──┘
```

The AI layer therefore acts as the first stage of a larger distributed sensing network.

Individual vehicles can independently detect and report observations, while Central-side logic can combine observations using their:

- Location
- Timestamp
- Vehicle identity
- Event type

This allows the system to move toward fleet-level intelligence rather than isolated camera detections.

---

# 2.8 AI and Edge Architecture

A major design decision in RAAHI was keeping the AI inference on the Edge computer instead of placing it on the Android phone.

The resulting architecture is:

```text
                 RAAHI-Eye
              Samsung Galaxy
                    │
             H.264 + GPS
                    │
                    ▼
              RAAHI-Edge
                    │
          ┌─────────┴─────────┐
          │                   │
       YOLO11n             ByteTrack
          │                   │
          └─────────┬─────────┘
                    │
             Event Analytics
                    │
                    ▼
             RAAHI-Central
```

This architecture reduces the computational burden on the mobile sensing device.

It also makes the AI pipeline easier to upgrade independently of the Android sensing application.

---

# 2.9 AI Pipeline Performance

The RAAHI-Edge AI pipeline was validated on Apple Silicon using MPS acceleration.

During the later live USB test, the pipeline reported:

- **30.0 FPS input**
- **29.9 FPS processing**
- **13.5 ms inference latency**
- **1920×1080 resolution**
- YOLO11n: **LIVE**
- Traffic tracker: **LIVE**

The full pipeline was simultaneously receiving camera data and GPS telemetry.

This demonstrates that the AI pipeline was not merely implemented as an isolated model but integrated into a functioning real-time processing system.

---

# 2.10 AI/ML and Event Generation

The AI pipeline feeds into the RAAHI event engine.

Conceptually:

```text
Camera
  ↓
Detection
  ↓
Tracking
  ↓
Condition / Event Logic
  ↓
Event ID
  ↓
GPS Association
  ↓
Evidence
  ↓
Central Backend
```

This allows AI detections to become structured events that can be stored, correlated, visualized, and reviewed.

For example, a pothole detection can eventually be represented as an observation containing:

```text
Event ID
Event Type
Vehicle ID
Latitude
Longitude
Timestamp
Confidence
Evidence
```

The AI therefore becomes one component of the larger event-generation system.

---

# 2.11 AI Reliability and Practical Engineering

Samar's AI/ML responsibility also exists within the practical constraints of deploying computer vision on a moving public-transport platform.

The project therefore considers:

- Real-time processing
- Inference latency
- Frame rate
- Model size
- Edge hardware capability
- Camera resolution
- Tracking stability
- GPS synchronization
- Event generation

This is important because a model that performs well in an isolated notebook is not necessarily suitable for a live vehicle-mounted sensing system.

RAAHI's AI pipeline is therefore evaluated as part of the **complete operational system**.

---

# 2.12 Team Coordination Around AI

Because the AI system sits between the sensing and event-processing layers, Samar's AI/ML work also requires coordination with other parts of the team.

For example:

### With Ujjwal

AI output must integrate correctly with:

- Edge architecture
- GPS
- Event engine
- Evidence generation
- Central transmission

### With Anjali

AI-generated events eventually need to reach the backend and centralized storage.

### With Kunal

AI-generated observations ultimately need to be represented meaningfully on the GIS dashboard.

### With Molly

AI behavior and system outputs need to be tested and demonstrated.

### With Utkarsh

The AI architecture needs to be documented clearly enough for evaluators to understand it.

Thus, Samar's AI responsibility naturally interacts with the other five team roles.

---

# 2.13 Team Leadership During Integration

As Team Lead, Samar's responsibility extends beyond his own technical area.

The project contains multiple parallel workstreams:

```text
AI / ML
Frontend
Backend
Android
Testing
Documentation
```

His leadership role helps maintain coordination between these workstreams so that development does not become six independent mini-projects.

The goal is to keep everyone working toward the same integrated RAAHI system.

---

# 2.14 Role Within the Final RAAHI Architecture

Samar's position within the system can be summarized as:

```text
                    RAAHI
                      │
             ┌────────┴────────┐
             │                 │
       Team Leadership      AI / ML
             │                 │
             │          ┌──────┴──────┐
             │          │             │
             │       YOLO11n      ByteTrack
             │          │             │
             │          └──────┬──────┘
             │                 │
             │          Traffic / Events
             │                 │
             └─────────┬───────┘
                       │
                 Overall Project
```

His role therefore connects **team-level coordination** with the **AI intelligence layer** of the platform.

---

# 2.15 Contribution Summary

### **Samar Kumar — Team Lead & AI/ML Engineer**

Samar's contribution to RAAHI centers around:

- **Team leadership**
- **Project coordination**
- **AI/ML engineering**
- **YOLO11n computer vision**
- **Pothole detection**
- **Vehicle detection**
- **ByteTrack object tracking**
- **Traffic analytics**
- **AI-to-event integration**
- **Edge AI architecture**
- **Real-time inference considerations**
- **Coordination between AI and other RAAHI subsystems**
- **Support for SIH demonstration and project direction**

### Overall contribution

> **Samar Kumar served as the Team Lead and AI/ML Engineer, coordinating the team while contributing to the computer-vision intelligence layer of RAAHI, including YOLO11n-based detection, ByteTrack-based tracking, traffic analytics, and the integration of AI outputs into the broader event-processing pipeline.**