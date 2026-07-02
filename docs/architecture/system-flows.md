# System Flows

> **Title:** System Flows
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
> * `docs/architecture/core-domain.md`
> * `docs/architecture/hld.md`
> * `docs/architecture/principles.md`

---

# Purpose

This document describes the major software engineering workflows supported by Project Asteria.

Each workflow represents a complete engineering capability executed by the Workflow Engine.

Every workflow consists of ordered stages.

Every stage emits engineering events.

The frontend reflects these events in real time.

---

# System Philosophy

Every user interaction is interpreted as an engineering workflow.

The Workflow Engine is responsible for selecting the correct workflow and coordinating its execution.

The user interacts with the workflow, not with individual backend services.

---

# Standard Workflow Lifecycle

Every workflow follows the same lifecycle.

```text
User Intent

↓

Workflow Selected

↓

Execution Context Created

↓

Workflow Started

↓

Stages Executed

↓

Events Emitted

↓

Workflow Completed
```

If a stage fails:

```text
Stage Failed

↓

Recovery Attempt

↓

Retry or Abort

↓

Workflow Failed Event
```

---

# Flow 1: Generate Application

## Purpose

Create a brand-new software project from a natural language prompt.

### Stages

```text
Receive Prompt

↓

Analyze Requirements

↓

Create Engineering Plan

↓

Generate Project Structure

↓

Generate Source Code

↓

Validate Output

↓

Write Files

↓

Install Dependencies

↓

Start Preview

↓

Complete Workflow
```

### Example Events

* WorkflowStarted
* RequirementsAnalyzed
* PlanningCompleted
* DirectoryCreated
* FileCreated
* FileUpdated
* DependenciesInstalled
* PreviewStarted
* PreviewReady
* WorkflowCompleted

---

# Flow 2: Modify Existing Project

## Purpose

Update an existing project using natural language.

### Stages

```text
Load Project

↓

Analyze Request

↓

Identify Files

↓

Generate Modifications

↓

Validate Changes

↓

Update Files

↓

Restart Preview

↓

Complete Workflow
```

---

# Flow 3: Explain Project

## Purpose

Help developers understand an existing project.

### Stages

```text
Load Project

↓

Analyze Architecture

↓

Analyze Source Files

↓

Generate Explanation

↓

Present Results
```

---

# Flow 4: Fix Bug

## Purpose

Resolve an issue described by the developer.

### Stages

```text
Receive Bug Report

↓

Analyze Project

↓

Locate Cause

↓

Generate Fix

↓

Validate

↓

Update Files

↓

Restart Preview

↓

Complete Workflow
```

---

# Flow 5: Generate Tests

## Purpose

Produce automated tests for an existing project.

### Stages

```text
Analyze Project

↓

Identify Test Targets

↓

Generate Tests

↓

Validate Test Files

↓

Save Tests

↓

Complete Workflow
```

---

# Flow 6: Dockerize Project

## Purpose

Prepare an application for containerized deployment.

### Stages

```text
Analyze Project

↓

Determine Runtime

↓

Generate Dockerfile

↓

Generate Compose Configuration

↓

Validate

↓

Complete Workflow
```

---

# Shared Workflow Stages

Some stages can be reused across multiple workflows.

Examples include:

* Load Project
* Analyze Requirements
* Planning
* Validation
* File Updates
* Preview Restart

Reusable stages reduce duplication and simplify maintenance.

---

# Workflow State Model

Every workflow transitions through defined states.

```text
Pending

↓

Running

↓

Completed
```

If execution cannot continue:

```text
Pending

↓

Running

↓

Failed
```

Optional recovery:

```text
Failed

↓

Retrying

↓

Running
```

---

# Event Flow

Every stage emits events.

```text
Workflow

↓

Stage

↓

Event

↓

Event Bus

↓

Streaming

↓

Frontend

↓

UI Update
```

The frontend never polls for progress.

It reacts to streamed engineering events.

---

# Design Goals

System flows should remain:

* Predictable
* Observable
* Modular
* Recoverable
* Extensible

New workflows should reuse existing stages whenever possible.

---

# Future Workflows

Future capabilities may include:

* Security Audit
* Accessibility Review
* Performance Optimization
* Dependency Upgrade
* Kubernetes Deployment
* Production Monitoring
* Database Migration
* Infrastructure Provisioning

Each should integrate into the Workflow Engine without requiring architectural changes.

---

# Summary

System behavior in Asteria is modeled as workflows.

Every workflow consists of reusable stages that emit engineering events.

This architecture enables transparency, modularity, and extensibility while keeping the user informed throughout every software engineering task.
