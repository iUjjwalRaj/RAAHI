# 6. Utkarsh Patwa

## **Role: Documentation & Technical Communications**

Utkarsh Patwa's role in RAAHI is centered around **technical documentation, project communication, organization of technical information, and making the system understandable to people who were not involved in building every component**.

RAAHI is a fairly large distributed system. Without proper documentation, the project quickly becomes six repositories' worth of mysterious commands and screenshots that nobody remembers how to reproduce. Humanity has apparently decided this is a recurring software-engineering problem. 😭

---

## 6.1 Documentation Responsibility

Utkarsh's primary responsibility is supporting the documentation layer surrounding RAAHI.

This includes helping communicate:

- What RAAHI is
- What problem it addresses
- How the system is structured
- What each subsystem does
- How the components communicate
- How the project should be demonstrated
- What technologies are involved
- What the project's capabilities and limitations are

The documentation therefore acts as the bridge between the **engineering implementation** and the **evaluation/presentation layer**.

---

# 6.2 Understanding the RAAHI Architecture

RAAHI consists of three major software layers plus the Android sensing component:

```text
┌───────────────────────┐
│     RAAHI-Eye         │
│   Android Sensing     │
└───────────┬───────────┘
            │
       Video + GPS
            ↓
┌───────────────────────┐
│     RAAHI-Edge        │
│   AI / CV Processing  │
└───────────┬───────────┘
            │
       Events + Evidence
            ↓
┌───────────────────────┐
│    RAAHI-Central      │
│ Backend + Database    │
└───────────┬───────────┘
            │
            ↓
┌───────────────────────┐
│     GIS Dashboard     │
│ Visualization / Ops   │
└───────────────────────┘
```

Documentation responsibility involves representing this architecture clearly so that someone reviewing the project can understand the data flow without needing to inspect the source code.

---

# 6.3 Technical Communication

One of the main challenges of RAAHI is that several different technologies are involved.

The project includes technologies such as:

- Android
- Kotlin
- RTSP
- MediaMTX
- Python
- YOLO11n
- ByteTrack
- OpenCV
- GPS
- SQLite
- Node.js
- Express
- MongoDB
- React
- Leaflet
- Google Drive
- Apple Silicon / MPS

A technical document needs to explain **why these technologies exist in the architecture**, rather than simply dumping a dependency list onto the reader.

For example:

```text
Technology
    ↓
Purpose
    ↓
Subsystem
    ↓
Role in RAAHI
```

This makes the architecture much easier to communicate.

---

# 6.4 Project Documentation

Documentation can cover the major project components individually.

### RAAHI-Eye

Documentation can explain:

- Android sensing
- Camera capture
- GPS acquisition
- RTSP streaming
- Edge endpoint configuration
- Device configuration
- Physical-device operation

### RAAHI-Edge

Documentation can explain:

- RTSP ingestion
- AI inference
- YOLO11n
- ByteTrack
- Traffic analytics
- GPS association
- Evidence generation
- SQLite offline queue
- Central transmission

### RAAHI-Central

Documentation can explain:

- API layer
- Event ingestion
- MongoDB
- Event processing
- Evidence handling
- Geographic correlation
- Dashboard integration

### Dashboard

Documentation can explain:

- GIS visualization
- Fleet observations
- Events
- Road/traffic intelligence
- Geographic context

---

# 6.5 Installation and Setup Documentation

A distributed project is only useful if another person can understand how to run it.

Documentation therefore supports the creation or maintenance of instructions covering areas such as:

```text
Environment
   ↓
Dependencies
   ↓
Configuration
   ↓
Services
   ↓
Network
   ↓
Startup
   ↓
Verification
```

This is especially important for RAAHI because the system requires multiple services to communicate correctly.

A person attempting to reproduce the project should be able to determine:

- Which component starts first
- Which ports are used
- What endpoints exist
- Which devices need to be connected
- What configuration values are required
- How to verify that each component is operational

---

# 6.6 Architecture Documentation

Another important part of the role is explaining **why the architecture looks the way it does**.

For example, RAAHI deliberately separates sensing, Edge intelligence, and Central processing.

```text
RAAHI-Eye
   │
   │ Raw sensing
   ↓
RAAHI-Edge
   │
   │ AI + local intelligence
   ↓
RAAHI-Central
   │
   │ Aggregation + storage
   ↓
Dashboard
```

This separation makes the system easier to understand and allows individual components to be developed and tested independently.

Documentation should communicate this architectural reasoning rather than merely naming folders.

---

# 6.7 Documenting the Offline-First Design

RAAHI's Edge layer contains an offline queue so that temporary network failures do not necessarily result in immediate loss of generated events.

The conceptual flow is:

```text
Event Generated
      ↓
SQLite
      ↓
Pending
      ↓
Network Available?
    /       \
  NO         YES
  ↓           ↓
Retry       Send
  ↓           ↓
Pending      Central
```

Documenting this behavior is important because it demonstrates that the system was designed for **real-world mobile deployment**, where connectivity cannot be assumed to be perfect.

---

# 6.8 Documenting Evidence Generation

RAAHI does not merely produce a detection label.

The Edge system can associate an event with recorded video evidence.

The documentation therefore needs to explain the relationship between:

```text
Detection
   +
Timestamp
   +
GPS
   +
Video Buffer
   ↓
Evidence Clip
```

This helps evaluators understand that the event can be independently reviewed rather than existing only as an abstract AI prediction.

---

# 6.9 Documenting System Limitations

Good technical communication is not just marketing.

It should also make clear what the prototype **does not currently guarantee**.

RAAHI's SIH problem statement is broad, while the implemented prototype focuses on a subset of the requested capabilities.

Documentation should therefore avoid presenting every item in the problem statement as though it were already fully implemented.

This distinction is particularly important:

```text
SIH Requirement
      ≠
Implemented Prototype Capability
```

Being explicit about that makes the technical documentation more credible.

---

# 6.10 Supporting the SIH Submission

Documentation also contributes to preparing material required for the Smart India Hackathon submission and evaluation.

This includes organizing information such as:

- Project title
- Problem statement
- Project description
- Abstract
- Architecture
- Technology stack
- Team information
- Demonstration material
- Project links
- Prototype capabilities

The goal is to maintain consistency across all these materials.

For example:

```text
README
   ↕
SIH Description
   ↕
Presentation
   ↕
Demo
   ↕
Technical Architecture
```

The same project should not magically become a completely different system depending on which PDF someone opens. Humanity has suffered enough from that particular form of documentation drift. 😭

---

# 6.11 Technical Presentation Support

Utkarsh's documentation role also supports the presentation of RAAHI to evaluators.

A technically complex project can be presented progressively:

### Level 1: Problem

> Public transport vehicles can act as mobile sensing platforms.

### Level 2: Solution

> RAAHI turns those vehicles into distributed urban intelligence nodes.

### Level 3: Architecture

> Android sensing → Edge AI → Central intelligence → GIS dashboard.

### Level 4: Technical depth

> YOLO11n, ByteTrack, GPS association, evidence buffering, SQLite, MongoDB, and GIS.

This progression allows both technical and non-technical evaluators to understand the project.

---

# 6.12 Maintaining Technical Consistency

Documentation also helps maintain consistent terminology throughout the project.

For example:

- **RAAHI-Eye** = sensing layer
- **RAAHI-Edge** = AI/edge-processing layer
- **RAAHI-Central** = central backend/data layer
- **Dashboard** = visualization and operational interface

Maintaining these definitions avoids confusion when multiple people are preparing README files, presentations, diagrams, and demonstrations.

---

# 6.13 Collaboration With Other Members

Utkarsh's work naturally connects to the entire team.

### With Ujjwal

Receives architectural information and converts the underlying system design into understandable technical documentation.

### With Samar

Documents the AI/ML pipeline and explains how computer vision contributes to RAAHI.

### With Kunal

Documents the dashboard and GIS-facing aspects of the platform.

### With Anjali

Documents backend integration, APIs, data flow, and central processing.

### With Molly

Coordinates documentation with testing results, demonstrations, and presentation material.

This gives Utkarsh a role that spans the whole project rather than one isolated subsystem.

---

# 6.14 Documentation as a Project Asset

The documentation itself becomes an important project asset.

A well-documented system allows:

- New developers to understand the architecture
- Team members to reproduce the environment
- Evaluators to understand the implementation
- Judges to follow the demonstration
- Future contributors to navigate the repository
- The team to maintain the system after the hackathon

Thus, documentation contributes to the **long-term maintainability** of RAAHI.

---

# 6.15 Role Within the Overall System

Utkarsh's position can be represented as:

```text
                    RAAHI
                      │
              ┌───────┴───────┐
              │               │
          Engineering      Research
              │               │
              └───────┬───────┘
                      ↓
               Technical Facts
                      ↓
             Utkarsh Patwa
                      ↓
          Documentation Layer
                      ↓
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
    README        Presentation      Demo
       │              │              │
       └──────────────┼──────────────┘
                      ↓
                  Evaluators
```

His contribution therefore acts as a **communication layer across the project**.

---

# 6.16 Contribution Summary

### **Utkarsh Patwa — Documentation & Technical Communications**

Utkarsh's role includes supporting:

- **Technical documentation**
- **Architecture documentation**
- **Project descriptions**
- **Installation/setup guidance**
- **Technology-stack documentation**
- **System workflow documentation**
- **SIH submission material**
- **Technical presentation**
- **README organization**
- **Demonstration explanations**
- **Technical terminology consistency**
- **Communication of project capabilities and limitations**
- **Coordination between technical and presentation material**

### Overall contribution

> **Utkarsh Patwa served as the Documentation & Technical Communications contributor for RAAHI, supporting the organization and communication of the project's architecture, implementation, setup, workflows, capabilities, and evaluation material, helping translate the team's technical work into documentation and presentation material that could be understood by evaluators and future contributors.**

---

## **Complete team structure**

| Member | Role |
|---|---|
| **Ujjwal Raj** | Lead Developer & System Architect |
| **Samar Kumar** | Team Lead & AI/ML Engineer |
| **Kunal** | Frontend & GIS Developer |
| **Anjali Mishra** | Backend & Integration Engineer |
| **Molly Arora** | Research, Testing & Media Lead |
| **Utkarsh Patwa** | Documentation & Technical Communications |

That gives you the full six-person contribution structure without pretending everyone secretly wrote half the code while you weren't looking. 😭