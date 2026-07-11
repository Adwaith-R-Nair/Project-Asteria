# ADR-001: Adopt Monorepo Architecture

## Status

Accepted

## Decision Date

July 11, 2026

## Decision Makers

Project Asteria Team

## Context

Project Asteria consists of multiple applications and shared packages, including the web application, backend API, shared libraries, infrastructure configuration, and future developer tooling.

Managing these components across separate repositories would introduce unnecessary overhead, duplicated configuration, and versioning complexity.

## Decision

Adopt a monorepo architecture managed with Turborepo.

The monorepo will contain all applications, shared packages, infrastructure, and project documentation within a single repository.

## Options Considered

### Multiple repositories

Advantages:

* Independent repositories
* Independent release cycles

Disadvantages:

* More maintenance
* Configuration duplication
* Harder cross-project refactoring
* Reduced developer experience

### Monorepo (Selected)

Advantages:

* Shared tooling
* Shared TypeScript configuration
* Easier refactoring
* Consistent dependency management
* Better developer experience

## Consequences

Positive:

* Faster development
* Simplified dependency management
* Easier code sharing
* Unified project history

Trade-offs:

* Larger repository
* Requires build orchestration

## Related ADRs

None.
