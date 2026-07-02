# Core Domain

> **Title:** Core Domain
>
> **Version:** 1.0
>
> **Status:** Approved
>
> **Owner:** Project Asteria Team
>
> **Last Updated:** July 2, 2026
>
> **Related Documents:**
>
> * `docs/product/vision.md`
> * `docs/product/prd.md`
> * `docs/architecture/principles.md`
> * `docs/architecture/hld.md`

---

# Purpose

This document defines the Core Domain of Project Asteria.

It explains the unique engineering capability that differentiates Asteria from traditional AI coding assistants and serves as the foundation for every architectural and implementation decision.

Every major feature should strengthen the Core Domain.

If a feature does not contribute to the Core Domain, its value should be carefully evaluated before implementation.

---

# The Core Problem

Modern AI tools are exceptional at generating code.

However, software engineering is much more than code generation.

A software engineer performs many activities before, during, and after writing code.

These include:

* Understanding requirements
* Clarifying ambiguity
* Planning implementation
* Designing architecture
* Generating code
* Validating changes
* Running applications
* Testing
* Debugging
* Refactoring
* Explaining decisions
* Iterating with feedback

Current AI tools often compress these activities into a single interaction.

The engineering process becomes invisible.

Developers receive the result, but rarely understand the journey.

---

# Our Core Domain

Project Asteria is **not** fundamentally a code generation platform.

Its Core Domain is:

> **Workflow Execution for Software Engineering**

Asteria specializes in executing software engineering workflows while making every meaningful stage transparent, observable, and understandable.

Artificial Intelligence is one capability used within these workflows.

It is not the product itself.

---

# Why Workflow Execution?

Every engineering task follows a process.

Examples include:

Generate an application.

Refactor an existing project.

Add authentication.

Fix a bug.

Generate tests.

Explain an architecture.

Improve accessibility.

Deploy an application.

Although the goals differ, they all follow structured workflows.

Instead of treating these as unrelated features, Asteria models each capability as an independent workflow executed by a common engine.

---

# The Workflow Engine

The Workflow Engine is the heart of Asteria.

Its responsibilities are to:

* Select the appropriate workflow.
* Initialize execution context.
* Execute workflow stages.
* Coordinate progress.
* Emit engineering events.
* Handle failures.
* Report completion.

The Workflow Engine does **not** generate software directly.

Instead, it coordinates the execution of specialized workflows.

---

# Workflows

A workflow represents a complete software engineering process.

Examples include:

* Generate Application
* Edit Application
* Explain Project
* Refactor Project
* Generate Tests
* Fix Bug
* Dockerize Project
* Configure CI/CD
* Deploy Application

Each workflow is independent.

New workflows can be introduced without modifying the Workflow Engine itself.

This design follows the Open/Closed Principle by allowing extension without requiring modification of the execution engine.

---

# Workflow Stages

Every workflow is composed of ordered stages.

A stage performs one specific responsibility before handing execution to the next stage.

Example:

```text
Generate Application

↓

Requirements Analysis

↓

Planning

↓

Code Generation

↓

Validation

↓

File Updates

↓

Preview

↓

Completion
```

Stages should remain small, focused, and independently testable.

Future workflows may reuse existing stages where appropriate.

---

# Engineering Events

Every meaningful stage emits events.

Events provide transparency throughout the engineering process.

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

These events drive the user interface, engineering timeline, progress indicators, and future analytics capabilities.

---

# Relationship Between Components

The Workflow Engine coordinates workflows.

Workflows execute stages.

Stages emit events.

Events update the platform.

```text
Workflow Engine

↓

Workflow

↓

Stage

↓

Engineering Event

↓

Platform Update
```

This layered approach minimizes coupling while maximizing extensibility.

---

# Why This Matters

This architecture allows Asteria to grow naturally.

Adding a new capability should typically require:

1. Creating a new workflow.
2. Defining its stages.
3. Emitting appropriate events.

The existing engine remains unchanged.

As a result, the platform becomes easier to extend, maintain, and test over time.

---

# Design Principles

The Core Domain follows several key principles:

* Everything is a workflow.
* Every workflow is composed of stages.
* Every stage has one responsibility.
* Every meaningful action emits an event.
* Every event improves transparency.
* AI participates in workflows rather than defining them.

---

# Future Evolution

The Workflow Engine should evolve into a platform capable of orchestrating increasingly sophisticated software engineering workflows.

Future workflows may include:

* Security Review
* Performance Optimization
* Dependency Upgrades
* Documentation Generation
* Database Migration
* Infrastructure Provisioning
* Kubernetes Deployment
* Production Monitoring

The engine should support these capabilities without fundamental architectural changes.

---

# Summary

The Core Domain of Project Asteria is **Workflow Execution for Software Engineering**.

Rather than focusing solely on AI-assisted code generation, Asteria models software engineering as a collection of transparent, observable workflows.

This approach aligns with the project's vision of helping developers build software while understanding every major engineering decision.

Every architectural decision, implementation detail, and future capability should reinforce this Core Domain.
