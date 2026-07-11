# ADR-002: Adopt Workflow Engine Architecture

## Status

Accepted

## Decision Date

July 11, 2026

## Decision Makers

Project Asteria Team

## Context

Asteria executes multiple software engineering capabilities, including application generation, project explanation, refactoring, testing, and deployment.

Implementing these capabilities as unrelated services would duplicate execution logic and reduce extensibility.

## Decision

Introduce a centralized Workflow Engine responsible for coordinating software engineering workflows.

Each capability will be implemented as an independent workflow executed through a common runtime.

## Options Considered

### Direct service execution

Simple initially but difficult to extend as capabilities grow.

### Workflow Engine (Selected)

Provides:

* Common execution model
* Reusable stages
* Shared execution context
* Extensible architecture
* Consistent lifecycle management

## Consequences

Positive:

* Clear separation of concerns
* Easy workflow expansion
* Consistent execution lifecycle

Trade-offs:

* Additional architectural abstraction
* Slightly higher implementation complexity

## Related ADRs

* ADR-001
