# Ripple

**A local intelligence layer for understanding system dependencies and coordinating changes across them.**

> **Status: early development — concept and documentation only.**
> No system mapper, dependency graph, or agent coordination runtime is implemented yet.
> Workflows and milestones below describe proposed direction, not available features.

## Vision and problem

Ripple aims to map code, databases, services, and their dependencies, then
coordinate agents to safely propagate changes across the system.

A change rarely stops at one file. A modified data shape, interface, or service
contract can affect callers, persistence, tests, and downstream services.
The goal is to make those consequences visible and coordinate related work
before components drift out of sync.

## Intended workflow

1. Select a local workspace and define the system boundaries.
2. Map supported code, database definitions, services, and dependencies.
3. Describe a proposed change and inspect its potential impact.
4. Prepare a reviewable change plan covering affected components.
5. Coordinate agents to make approved edits within that scope.
6. Run relevant validation and present the diff and unresolved risks.

**Illustrative use case:** changing a field in a service contract could require
updates to callers, database mappings, and tests. Ripple would aim to identify
those dependencies and coordinate the related edits. This is a target workflow,
not functionality available today.

## Proposed building blocks

- **Workspace mapping:** discover supported components and their relationships.
- **Dependency representation:** retain a navigable view of those relationships.
- **Impact analysis:** identify components potentially affected by a proposed change.
- **Agent coordination:** divide related edits into scoped, ordered tasks.
- **Validation and review:** expose diffs, check results, and unresolved dependencies.

These are conceptual responsibilities, not existing modules. The implementation
architecture and technology stack remain open.

## Current repository

The repository currently contains only this README. There is no application
entry point, dependency manifest, configuration schema, test suite, or CI workflow.

## Local development and validation

There is nothing to install or run yet. Development currently starts with
defining the first supported workspace and a small, testable change scenario.

When the first implementation lands, this section should include supported
languages and runtime versions, installation and startup commands, workspace
configuration, validation commands, and a reproducible example with expected
output. No setup commands or configuration variables are specified before they exist.

## Proposed milestones

1. **Define the first scenario:** select one language and a small local fixture
   with a change that crosses component boundaries.
2. **Build a read-only map:** discover a limited set of dependencies and make
   unsupported relationships explicit.
3. **Explain change impact:** produce an inspectable list of affected components
   with evidence for each dependency.
4. **Coordinate reviewed edits:** introduce scoped agent tasks and a reviewable
   diff without applying changes to live systems.
5. **Validate the scenario:** run the fixture's checks and report failures,
   incomplete work, and remaining uncertainty.

## Open design decisions

- Which language, database definitions, and service contracts should be mapped first?
- How should dependencies be discovered, represented, and kept up to date?
- What evidence is needed before treating a relationship as a dependency?
- How should agents handle ordering, conflicting edits, and partial failure?
- What approval, validation, and recovery mechanisms are required before edits?
- What stays local, and could an external model provider receive workspace data?

## Safety and scope

Start with read-only analysis of disposable local fixtures. Proposed editing
capabilities should require explicit scope, reviewable changes, and validation.
Production database migrations, deployment, and unreviewed system-wide changes
are outside the initial proposed scope.

"Local" describes the project's intended direction; no runtime or data-flow
guarantees exist yet. Do not assume complete dependency discovery or safe
automatic propagation before those properties are implemented and tested.

## Contributing and keeping this README current

Ground each capability in a reproducible fixture and document what the mapper
can and cannot discover. As implementation lands, update this README with actual
setup commands, supported integrations, agent permissions, validation steps, and
known limitations. Keep planned behavior distinct from working features.

Do not commit credentials, private workspace contents, or generated dependency
maps containing sensitive information.
