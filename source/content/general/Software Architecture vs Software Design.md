---
title: "Software Architecture vs Software Design"
tags:
  - software-architecture
  - software-design
  - career
---

This note contrasts **architecture** (system-wide structure and constraints) with **design** (how individual parts are implemented).

## What is software architecture

In software, architecture is the strategic blueprint:

- What are the core components of the system?
- How will they communicate?
- What technologies and tools will be used?
- What qualities must the system uphold (scalability, availability, etc.)?

### Core responsibilities of architecture

- **High-Level Structure**: Breaks the system into services, layers, or modules
- **Integration Strategy**: Defines communication between components (e.g., APIs, events, queues)
- **Technology Stack**: Selects frameworks, databases, platforms
- **Quality Attributes**: Designs for scalability, performance, security, fault tolerance
- **Risk Management**: Mitigates long-term complexity and cost


## What is software design

Design is the detailed approach for implementing each part of the system:

- How is this feature structured?
- What classes and methods are involved?
- What data structures and algorithms are appropriate?
- How do we keep the code clean and testable?


### Core responsibilities of design

- **Implementation Strategy**: Plans out how features or modules will work internally
- **Code Structure**: Applies principles like abstraction, encapsulation, and responsibility
- **Design Principles**: Uses SOLID, DRY, and KISS principles to improve clarity and reuse
- **Design Patterns**: Leverages reusable solutions (e.g., Strategy, Factory, Observer)
- **Testability**: Structures code for unit testing and debugging