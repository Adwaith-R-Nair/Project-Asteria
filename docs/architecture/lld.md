# Low Level Design (LLD)

> **Title:** Low Level Design
>
> **Version:** 1.0
>
> **Status:** Draft
>
> **Owner:** Project Asteria Team
>
> **Last Updated:** July 2, 2026
>
> **Related Documents:**
>
> * `docs/architecture/hld.md`
> * `docs/architecture/core-domain.md`
> * `docs/architecture/system-flows.md`

---

# Purpose

This document defines the internal architecture of Project Asteria.

While the High Level Design identifies the major system components, the Low Level Design defines how those components collaborate internally to execute software engineering workflows.

This document intentionally focuses on responsibilities and interactions rather than implementation details.

---

# Internal Architecture

The backend is organized around the execution of software engineering workflows.

Every workflow is executed through a common runtime composed of well-defined architectural components.

```text
Workflow Engine

↓

Workflow Registry

↓

Workflow

↓

Workflow Executor

↓

Execution Context

↓

Workflow Stages

↓

Engineering Events
```

---

# Workflow Engine

## Responsibilities

* Receive workflow execution requests.
* Resolve workflow definitions.
* Create execution context.
* Start workflow execution.
* Monitor workflow lifecycle.
* Return workflow status.

The Workflow Engine is the entry point for all workflow execution.

It does not execute workflow stages directly.

---

# Workflow Registry

## Responsibilities

* Register available workflows.
* Resolve workflows by identifier.
* Support future extensibility.

Example workflows include:

* Generate Application
* Modify Project
* Explain Project
* Fix Bug
* Generate Tests
* Dockerize Project

The registry enables new workflows to be introduced without modifying the Workflow Engine.

---

# Workflow

A workflow defines an engineering process.

A workflow consists of:

* Metadata
* Ordered stages
* Configuration
* Execution policies

A workflow describes *what* should happen.

It does not define *how* execution occurs.

---

# Workflow Executor

The Workflow Executor is responsible for runtime execution.

## Responsibilities

* Execute stages sequentially.
* Manage workflow state.
* Handle failures.
* Perform retries where appropriate.
* Emit workflow lifecycle events.
* Update execution context.

The executor owns workflow progression.

---

# Execution Context

The Execution Context contains all information required during workflow execution.

Examples include:

* User prompt
* Workspace
* Project files
* Conversation history
* Workflow metadata
* Configuration
* Current stage
* Generated artifacts

The Execution Context is shared across workflow stages.

Stages communicate by reading and updating the context rather than interacting directly.

---

# Workflow Stage

A stage represents a single engineering activity.

Examples include:

* Analyze Requirements
* Create Plan
* Generate Source Code
* Validate Output
* Update Files
* Start Preview

Every stage should:

* Have one responsibility.
* Receive an Execution Context.
* Update the Execution Context.
* Emit engineering events.
* Return control to the Workflow Executor.

Stages should remain reusable across workflows whenever practical.

---

# Engineering Events

Every meaningful workflow activity emits events.

Events communicate progress throughout the platform.

Examples include:

* WorkflowStarted
* StageStarted
* StageCompleted
* StageFailed
* FileCreated
* FileUpdated
* PreviewStarted
* PreviewReady
* WorkflowCompleted

Events are consumed by other components without creating direct dependencies between them.

---

# Execution Lifecycle

A workflow execution follows the lifecycle below.

```text
Workflow Requested

↓

Workflow Resolved

↓

Execution Context Created

↓

Workflow Started

↓

Execute Stage

↓

Update Context

↓

Emit Events

↓

Execute Next Stage

↓

Workflow Completed
```

If a failure occurs:

```text
Stage Failed

↓

Recovery Policy

↓

Retry

or

Workflow Failed
```

---

# Separation of Responsibilities

| Component         | Responsibility                    |
| ----------------- | --------------------------------- |
| Workflow Engine   | Starts workflow execution         |
| Workflow Registry | Resolves workflows                |
| Workflow          | Describes engineering process     |
| Workflow Executor | Executes workflow                 |
| Execution Context | Stores execution state            |
| Workflow Stage    | Performs one engineering activity |
| Event Bus         | Publishes engineering events      |

Each architectural component owns one primary responsibility.

---

# Design Principles

The Low Level Design follows these principles:

* Everything is a workflow.
* Every workflow consists of stages.
* Every stage has one responsibility.
* Every workflow executes through a common runtime.
* Context is shared through the Execution Context.
* Components communicate through engineering events.
* New workflows should require minimal architectural changes.

---

# Future Evolution

The architecture supports future capabilities such as:

* Parallel stage execution
* Conditional workflows
* Workflow composition
* Workflow templates
* User-defined workflows
* Distributed workflow execution
* Plugin workflows

These capabilities should build upon the existing execution model rather than replacing it.

---

# Summary

The Low Level Design establishes the execution model of Project Asteria.

The Workflow Engine coordinates execution.

The Workflow Executor manages runtime behavior.

Workflow Stages perform focused engineering activities.

Engineering Events communicate progress.

Together these components create a modular, extensible, and transparent execution platform for software engineering workflows.