# ADR-003: Adopt Event-Driven Communication

## Status

Accepted

## Decision Date

July 11, 2026

## Decision Makers

Project Asteria Team

## Context

The Workflow Engine, frontend, preview runtime, engineering timeline, and future analytics features all require visibility into workflow execution.

Direct component-to-component communication would create tight coupling.

## Decision

Adopt an event-driven communication model.

Meaningful engineering actions publish immutable events that are consumed by independent subscribers.

## Options Considered

### Direct service communication

Simple but tightly coupled.

### Event-driven communication (Selected)

Advantages:

* Loose coupling
* Better extensibility
* Streaming support
* Timeline generation
* Analytics support

## Consequences

Positive:

* Modular communication
* Real-time updates
* Transparent workflow execution

Trade-offs:

* Requires event infrastructure
* Additional runtime complexity

## Related ADRs

* ADR-001
* ADR-002
