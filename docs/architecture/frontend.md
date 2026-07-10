# Frontend Architecture

> **Title:** Frontend Architecture
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
> * `docs/architecture/backend.md`
> * `docs/architecture/system-flows.md`

---

# Purpose

This document defines the architecture of the Asteria frontend.

The frontend is responsible for presenting workflow execution, visualizing engineering progress, enabling user interaction, and maintaining a responsive software engineering experience.

The frontend is not responsible for business logic.

Instead, it reflects the current state of the backend through streamed engineering events.

---

# Architectural Goals

The frontend architecture is designed to achieve the following goals:

* Workflow-centric user experience
* Real-time updates
* Clear engineering visibility
* Responsive interaction
* Modular component organization
* Minimal business logic
* Extensible user interface

---

# Frontend Philosophy

The frontend is a projection of the backend.

The backend owns system state.

The frontend visualizes that state.

Users should never wonder what the platform is doing.

Every meaningful engineering action should be visible.

---

# Primary User Interface Regions

The frontend is organized into five primary regions.

## Workflow Panel

The Workflow Panel is the central element of the interface.

Responsibilities:

* Display active workflow
* Display current stage
* Display workflow progress
* Display workflow status
* Display failures and recovery

---

## Workspace

The Workspace provides the development environment.

Responsibilities:

* File explorer
* Code editor
* Open files
* Search
* Project navigation

---

## Live Preview

The Live Preview displays the running application.

Responsibilities:

* Display application output
* Refresh after updates
* Display build failures
* Display runtime errors

---

## Conversation Panel

The Conversation Panel enables interaction with Asteria.

Responsibilities:

* Prompt input
* Conversation history
* Workflow requests
* Follow-up questions

The Conversation Panel is an interface for initiating workflows rather than the primary focus of the application.

---

## Engineering Timeline

The Engineering Timeline displays engineering progress.

Responsibilities:

* Display engineering events
* Display workflow history
* Display stage completion
* Display project evolution

The timeline represents one of Asteria's core differentiators by making software engineering transparent.

---

# Context Panel

The Context Panel provides educational context throughout workflow execution.

Responsibilities:

* Explain workflow stages
* Explain engineering decisions
* Explain generated files
* Explain architectural choices

The Context Panel reinforces Asteria's mission of helping developers understand what they build.

---

# Frontend State

The frontend maintains presentation state only.

Examples include:

* Open files
* Selected tabs
* Active panel
* UI preferences

Business state remains on the backend.

---

# Event Driven User Interface

The frontend reacts to engineering events.

Examples include:

```text
WorkflowStarted

↓

Workflow Panel Updated
```

```text
FileCreated

↓

Workspace Updated
```

```text
PreviewReady

↓

Preview Refreshed
```

```text
StageCompleted

↓

Timeline Updated
```

The frontend should not poll for updates.

It reacts to streamed events.

---

# Page Structure

The application consists of three primary pages.

* Workspace
* Projects
* Settings

Most engineering activity occurs within the Workspace page.

---

# Component Principles

Frontend components should follow these principles:

* One responsibility per component
* Composition over inheritance
* Reusable building blocks
* Event-driven updates
* Minimal internal state

---

# Future Evolution

Future capabilities may include:

* Collaborative editing
* Multi-user workflows
* Plugin panels
* Custom layouts
* Mobile companion experience
* Workflow analytics
* Session replay

The architecture should support these capabilities without significant redesign.

---

# Summary

The Asteria frontend is designed around workflow visibility rather than chat interactions.

It presents software engineering as an observable process by reacting to engineering events and visualizing workflow execution in real time.

This approach aligns the user experience with Asteria's core philosophy of transparency, understanding, and workflow-centric software engineering.
