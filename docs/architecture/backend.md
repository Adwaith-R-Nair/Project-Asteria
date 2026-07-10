# Backend Architecture

> **Title:** Backend Architecture
>
> **Version:** 1.0
>
> **Status:** Draft
>
> **Owner:** Project Asteria Team
>
> **Last Updated:** July 10, 2026
>
> **Related Documents:**
>
> * `docs/architecture/hld.md`
> * `docs/architecture/lld.md`
> * `docs/architecture/core-domain.md`
> * `docs/architecture/system-flows.md`

---

# Purpose

This document defines the internal organization of the Asteria backend.

The backend is responsible for executing software engineering workflows, coordinating workflow stages, managing execution state, publishing engineering events, and interacting with external systems.

The backend is the source of truth for all engineering operations.

---

# Architectural Goals

The backend architecture is designed to achieve the following goals:

* Clear separation of responsibilities
* High cohesion
* Low coupling
* Extensibility
* Testability
* Provider independence
* Transparent workflow execution

---

# Architectural Layers

The backend is organized into five primary layers.

```text
Interfaces

↓

Application

↓

Domain

↓

Infrastructure

↓

Shared
```

Each layer owns a distinct responsibility.

---

# Layer Responsibilities

## Interfaces

The Interfaces layer exposes the backend to external clients.

Responsibilities:

* HTTP endpoints
* Streaming endpoints
* Request validation
* Response formatting
* Authentication integration (future)

This layer contains no business logic.

---

## Application

The Application layer coordinates software engineering workflows.

Responsibilities:

* Workflow Engine
* Workflow Registry
* Workflow Executor
* Execution Context
* Workflow lifecycle
* Use case orchestration

The Application layer is responsible for coordinating work but does not implement infrastructure concerns.

---

## Domain

The Domain layer represents the core business concepts of Asteria.

Examples include:

* Workflow definitions
* Workspace
* Project
* Engineering events
* Business rules

The Domain layer must remain independent of infrastructure.

---

## Infrastructure

The Infrastructure layer integrates with external systems.

Responsibilities:

* AI provider communication
* Database access
* Filesystem operations
* Sandbox execution
* Preview runtime
* Persistent storage

Infrastructure components implement capabilities required by the Application layer.

---

## Shared

The Shared layer contains reusable building blocks.

Examples include:

* Shared types
* Result objects
* Error definitions
* Utility functions
* Constants

Shared code should remain generic and independent of specific business logic.

---

# Backend Component Overview

```text
HTTP Request

↓

Interfaces

↓

Workflow Engine

↓

Workflow Registry

↓

Workflow Executor

↓

Workflow Stages

↓

Infrastructure

↓

Engineering Events

↓

Streaming Response
```

---

# Workflow Engine

Responsibilities:

* Receive execution requests
* Resolve workflows
* Initialize execution context
* Start execution
* Track workflow lifecycle

The Workflow Engine does not execute stages directly.

---

# Workflow Registry

Responsibilities:

* Register workflows
* Resolve workflows
* Support future extensibility

New workflows should be introduced through the registry without modifying the Workflow Engine.

---

# Workflow Executor

Responsibilities:

* Execute workflow stages
* Manage execution state
* Handle failures
* Execute retries
* Emit lifecycle events

The Workflow Executor is responsible for runtime execution.

---

# Execution Context

The Execution Context contains all information required during workflow execution.

Examples include:

* User request
* Workspace
* Conversation history
* Project metadata
* Generated artifacts
* Current stage
* Workflow configuration

The Execution Context is shared across all workflow stages.

---

# Workflow Stages

Stages perform focused engineering activities.

Examples include:

* Requirements Analysis
* Planning
* Code Generation
* Validation
* File Updates
* Preview Startup

Stages communicate by updating the Execution Context and emitting engineering events.

---

# Engineering Events

Every significant operation produces engineering events.

These events drive:

* Streaming updates
* Engineering timeline
* Progress indicators
* Future analytics

The backend publishes events without knowledge of how they are ultimately presented.

---

# Dependency Rules

Dependencies should always move inward.

```text
Interfaces

↓

Application

↓

Domain

↓

Infrastructure
```

The Domain layer must never depend on Infrastructure.

Application logic should remain independent of implementation details whenever practical.

---

# Design Principles

The backend follows these principles:

* One responsibility per module
* Workflow-centric execution
* Event-driven communication
* Provider independence
* Clear dependency boundaries
* Explicit execution flow

---

# Future Evolution

As Asteria grows, infrastructure components may evolve into independent services.

Potential future services include:

* Workflow Service
* Preview Service
* AI Gateway
* Workspace Service
* Notification Service

The internal architecture should support this evolution without requiring major redesign.

---

# Summary

The backend architecture is centered around workflow execution.

The Workflow Engine coordinates execution.

The Workflow Executor manages runtime behavior.

Workflow stages perform focused engineering activities.

Infrastructure provides external capabilities.

Engineering events connect all major backend components while maintaining loose coupling.
