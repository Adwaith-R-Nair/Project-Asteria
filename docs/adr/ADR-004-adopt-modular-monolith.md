# ADR-004: Adopt Modular Monolith Architecture

## Status

Accepted

## Decision Date

July 11, 2026

## Decision Makers

Project Asteria Team

## Context

Project Asteria is expected to grow significantly over time.

While microservices provide strong service isolation, they introduce operational complexity that is unnecessary during the early stages of development.

## Decision

Implement Asteria as a modular monolith.

Business capabilities will remain modular with clear boundaries while executing within a single deployable backend.

## Options Considered

### Microservices

Advantages:

* Independent deployment
* Independent scaling

Disadvantages:

* Operational complexity
* Distributed debugging
* Service coordination
* Infrastructure overhead

### Modular Monolith (Selected)

Advantages:

* Simpler development
* Easier debugging
* Lower operational overhead
* Future migration path

## Consequences

Positive:

* Faster development
* Lower infrastructure complexity
* Easier testing

Trade-offs:

* Single deployment unit
* Future extraction work if services are separated

## Related ADRs

* ADR-001
* ADR-002
* ADR-003
