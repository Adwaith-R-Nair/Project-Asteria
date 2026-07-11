# Event System

> **Title:** Event System
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
> * `docs/architecture/frontend.md`
> * `docs/architecture/system-flows.md`

---

# Purpose

This document defines the event-driven communication model used throughout Project Asteria.

The Event System enables loose coupling between components while providing real-time visibility into software engineering workflows.

Every meaningful engineering activity produces an event.

These events become the foundation for workflow visualization, streaming, timeline generation, and future analytics.

---

# Event Driven Philosophy

Components should communicate through events whenever practical.

Instead of directly invoking other components, publishers emit events describing completed actions.

Subscribers react independently.

This architecture promotes modularity, extensibility, and transparency.

---

# Event System Overview

```text
Workflow Engine

↓

Workflow Executor

↓

Workflow Stage

↓

Engineering Event

↓

Event Bus

↓

Event Stream

↓

Frontend
```

The Event System acts as the communication layer connecting backend execution with frontend visualization.

---

# Event Lifecycle

Every engineering event follows the same lifecycle.

```text
Action Performed

↓

Event Created

↓

Published

↓

Delivered

↓

Processed

↓

Visualized
```

Events are immutable records of completed actions.

---

# Event Categories

## Workflow Events

Represent workflow lifecycle changes.

Examples:

* WorkflowStarted
* WorkflowCompleted
* WorkflowFailed

---

## Stage Events

Represent execution of workflow stages.

Examples:

* StageStarted
* StageCompleted
* StageFailed

---

## File Events

Represent project filesystem changes.

Examples:

* FileCreated
* FileUpdated
* FileDeleted
* DirectoryCreated

---

## Preview Events

Represent preview lifecycle changes.

Examples:

* PreviewStarted
* PreviewReady
* PreviewRestarted
* PreviewFailed

---

## Workspace Events

Represent workspace lifecycle changes.

Examples:

* WorkspaceCreated
* WorkspaceLoaded
* WorkspaceSaved

---

## System Events

Represent internal platform events.

Examples:

* ProviderConnected
* ProviderUnavailable
* DependencyInstalled
* ErrorOccurred

---

# Event Structure

Every engineering event contains a consistent set of metadata.

Conceptually, an event includes:

* Event identifier
* Event type
* Workflow identifier
* Timestamp
* Payload

A consistent structure simplifies processing throughout the platform.

---

# Publishers

Publishers produce engineering events.

Examples include:

* Workflow Executor
* Workflow Stages
* Filesystem Module
* Preview Module
* Workspace Module

Publishers should not know which components consume their events.

---

# Event Bus

The Event Bus is responsible for:

* Receiving events
* Distributing events
* Preserving ordering
* Supporting multiple subscribers

The MVP implementation will use an in-process Event Bus.

Future versions may evolve to distributed messaging infrastructure if required.

---

# Subscribers

Subscribers react to published events.

Examples include:

* Streaming Layer
* Engineering Timeline
* Logging
* Analytics
* Notifications

Subscribers remain independent of publishers.

---

# Event Stream

The Event Stream delivers engineering events to connected frontend clients.

The frontend receives a continuous stream of events rather than polling for updates.

This enables real-time workflow visualization.

---

# Commands and Events

Commands represent requested actions.

Examples:

* GenerateProject
* ExplainProject
* FixBug

Events represent completed actions.

Examples:

* WorkflowStarted
* StageCompleted
* PreviewReady

Commands request work.

Events describe facts.

---

# Design Principles

The Event System follows these principles:

* Events are immutable.
* Publishers are unaware of subscribers.
* Subscribers react independently.
* Events describe completed actions.
* Communication remains loosely coupled.
* Every meaningful engineering action should be observable.

---

# Future Evolution

The Event System should support future capabilities including:

* Event replay
* Workflow playback
* Analytics
* Monitoring
* Distributed event processing
* Plugin subscribers
* Workflow metrics

These capabilities should build upon the existing event model.

---

# Summary

The Event System forms the communication backbone of Project Asteria.

By modeling software engineering as a stream of immutable events, Asteria provides transparency, modularity, and extensibility while keeping the user informed throughout every workflow execution.
