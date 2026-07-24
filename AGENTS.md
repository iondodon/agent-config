# Project Agent Guidelines

These instructions apply to the entire repository.

This is an evolving project, not a rigid implementation of a fully known final design. It is being built incrementally, and each task may reveal a better structure, abstraction, style, workflow, or low-level approach.

Treat the current codebase as the best-known design so far, not as something that must remain unchanged.

## Development Lifecycle

Treat each task as an incremental improvement to the project, not merely as an isolated implementation request.

Consider the complete development lifecycle:

- Discovery
- Architectural impact
- Preparation
- Implementation
- Integration
- Migration
- Verification
- Documentation
- Future maintenance

Before proposing or implementing a change:

1. Gather the information needed to understand the request and the current system.
2. Locate and inspect the relevant code, architecture, tests, dependencies, boundaries, configuration, and nearby patterns.
3. Understand the existing behavior before deciding how it should change.
4. Assess the task from the highest relevant architectural level down to the implementation details.
5. Consider its effect on users, existing behavior, integrations, related modules, deployment, maintenance, and future development.
6. Identify any preparation needed for a clean solution, such as:
   - Refactoring existing code
   - Moving behavior to the correct owner
   - Clarifying an interface
   - Replacing an unsuitable approach
   - Introducing missing infrastructure
   - Migrating existing data or behavior

7. Present the proposed solution, important trade-offs, preparatory changes, and decisions that could materially affect the direction.
8. Ask questions when important answers cannot be established from the repository, requirements, or available evidence.

Discuss and refine the direction with the user, and wait for explicit approval before implementation when the task requires a meaningful architectural or product decision.

When the user has already approved the direction and asked to proceed, implement it without unnecessarily repeating the same discussion.

Choose the scope required for a coherent, reliable, and maintainable result, not simply the smallest change suggested by the apparent size of the task.

A substantial refactor may be appropriate even for a small feature when the evidence shows that it is necessary to integrate the change correctly or materially improve future development. Keep such work purposeful, proportionate, and directly connected to the task.

The final user experience and functionality are the primary outcomes. Code, architecture, and process exist to support those outcomes.

Integrate each implementation with the existing system, preserve or improve affected behavior, and verify the result at every relevant layer.

## Simplicity And Efficiency

Always strive for solutions that are simple, clear, and efficient.

Do not overengineer.

Prefer the simplest design that:

- Correctly satisfies the requirements
- Integrates cleanly with the existing system
- Is reliable and testable
- Has clear ownership
- Can be maintained without unnecessary effort
- Does not block known near-term development

Avoid introducing abstractions, layers, frameworks, configuration, indirection, or general-purpose systems without a concrete need.

Do not optimize solely for the fewest changed lines. A slightly larger but clearer solution is preferable to a small patch that creates hidden coupling, duplication, fragile behavior, or future maintenance problems.

At the same time, do not redesign large parts of the project when a focused and well-structured change is sufficient.

Prefer straightforward implementations over clever ones.

Optimize performance only where it matters or where evidence shows a meaningful problem. Avoid speculative optimization, but do not introduce obviously inefficient behavior when an equally simple and efficient alternative exists.

## Engineering Principles

- Put behavior in the layer that owns it.
- Keep domain-specific logic separate from shared infrastructure.
- Design generally useful capabilities so other modules, applications, or products can reuse them without depending on unrelated domain-specific code.
- Prefer existing abstractions and conventions when they fit the task.
- Introduce a new abstraction only when it:
  - Establishes a real ownership boundary
  - Removes meaningful duplication
  - Supports a concrete reusable capability
  - Makes important behavior easier to test or reason about

- Refactor adjacent code when necessary to integrate a change cleanly, improve structure, or restore the correct dependency direction.
- Make the best architectural decision supported by the current task and available evidence.
- Do not preserve an earlier decision only because it already exists.
- Modules, packages, crates, APIs, services, components, styles, schemas, and implementation strategies may be created, split, combined, moved, replaced, or removed when that improves the project.
- Apply this willingness to improve at every relevant level, from overall architecture and product boundaries to naming, control flow, data structures, tests, tooling, and user experience.
- Avoid unrelated refactoring.
- Avoid premature generalization.
- Keep application entry points focused on bootstrap, configuration, and composition rather than feature implementation.
- Keep platform-specific, framework-specific, vendor-specific, and infrastructure-specific details behind clear boundaries when doing so improves portability or testability.
- Make behavior, defaults, state transitions, ownership, data conversions, and error cases explicit and deterministic.
- Avoid hidden side effects, environment-dependent guessing, and implicit fallback paths.
- Fail clearly when an operation cannot satisfy its contract.
- Do not silently substitute behavior, discard information, repair invalid data, or reduce functionality.
- Any necessary fallback must be deliberate, observable, documented, and testable.
- Favor established open standards and interoperable formats for user-facing data, protocols, persistence, and integration boundaries.
- Prefer proven libraries, protocols, platform facilities, and existing solutions when they meet the requirements.
- Create custom alternatives only for a concrete and documented reason.
- Keep custom representations internal when possible.
- Treat every officially supported environment and platform as a primary target when designing shared behavior.

## Reuse And Structure

For each implementation, consider:

1. Is this behavior specific to one feature, module, product, or domain?
2. Could it be useful elsewhere in the project?
3. Does an existing module, component, service, or type already own it?
4. Would placing it locally cause meaningful duplication later?
5. Can reusable infrastructure be separated from domain-specific semantics?
6. Does the proposed abstraction solve a concrete current problem?
7. Does the change leave the code easier to understand, extend, and test?
8. Is the dependency direction clear and appropriate?

Share infrastructure and contracts where useful, but do not force unrelated parts of the project into one universal model.

Different products, modules, and domains may reuse shared services while retaining their own models, rules, and workflows.

Reason at every relevant level, beginning with the highest level affected:

1. Project or system
2. Product or application
3. Domain or subsystem
4. Package, crate, service, or module
5. Component, type, or interface
6. Function or method
7. Implementation detail

Check that local decisions support the broader project direction and that broader abstractions remain grounded in concrete needs.

Existing placeholders, modules, product boundaries, and directory structures provide architectural context, but they are not necessarily a permanent roadmap. They may be added, removed, renamed, split, or combined as the project evolves.

## Implementation

During implementation:

- Follow the approved direction and existing project conventions where appropriate.
- Keep changes focused on the task and necessary supporting work.
- Preserve existing behavior unless the requested change intentionally alters it.
- Keep new behavior explicit and deterministic.
- Handle relevant failure cases.
- Avoid leaving temporary compatibility code, dead code, duplicated paths, or unfinished migrations unless explicitly justified.
- Update all affected call sites, integrations, schemas, configuration, tests, and documentation.
- Remove obsolete code when the new implementation fully replaces it.
- Keep public interfaces as small and clear as reasonably possible.
- Use names that communicate domain meaning and ownership.
- Add comments only where they explain intent, constraints, trade-offs, or behavior that is not clear from the code itself.
- Do not use comments to compensate for unnecessarily confusing code.

When a migration or compatibility period is necessary:

- Define the old and new behavior clearly.
- Make the transition explicit.
- Test both the migration and the final state.
- Document removal conditions for temporary compatibility code.
- Avoid indefinite dual implementations.

## Testing And Verification

Testing is not limited to unit tests.

For every meaningful change, determine which forms of verification provide useful confidence. Use a combination appropriate to the task.

Possible verification methods include:

- Unit tests
- Integration tests
- End-to-end tests
- Regression tests
- Component tests
- Contract tests
- API tests
- Database tests
- Migration tests
- Serialization and deserialization tests
- Property-based tests
- Fuzz tests
- Snapshot tests
- Visual regression tests
- Accessibility tests
- Performance tests
- Load tests
- Concurrency tests
- Security tests
- Cross-platform tests
- Installation and upgrade tests
- Build and packaging tests
- Manual testing

Do not add every type of test mechanically. Select the tests that exercise the real risks introduced or affected by the change.

### Automated Testing

- Add focused regression coverage for behavioral changes and bug fixes.
- Test externally observable behavior rather than only internal implementation details.
- Cover important success paths, failure paths, boundaries, and state transitions.
- Test integrations at the level where failures can realistically occur.
- Verify migrations with representative existing data when applicable.
- Avoid tests that merely repeat the implementation without validating meaningful behavior.
- Keep tests deterministic, isolated where appropriate, and understandable.
- Ensure tests fail for the intended reason when behavior breaks.
- Update obsolete tests when intentional behavior changes.
- Do not weaken assertions simply to make a failing test pass.

### Manual And Real-World Testing

When practical, test the result as a real user would.

This may include:

1. Building and running the actual application.
2. Starting all required services and dependencies.
3. Interacting with the changed feature through the real user interface, command-line interface, API, or workflow.
4. Testing both normal and failure scenarios.
5. Verifying persistence across restarts or reloads.
6. Trying realistic input rather than only synthetic test data.
7. Checking behavior with different window sizes, devices, platforms, permissions, network conditions, or configurations when relevant.
8. Capturing screenshots of important visual states.
9. Reviewing and analyzing those screenshots for:
   - Layout problems
   - Clipping
   - Overflow
   - Incorrect spacing
   - Misalignment
   - Unexpected colors or styles
   - Missing states
   - Inconsistent typography
   - Accessibility problems
   - Incorrect responsive behavior
   - Visual regressions

10. Comparing the result with the expected user experience.
11. Recording any limitations or scenarios that could not be tested.

Use judgment and creativity when deciding how to test a change. The goal is to evaluate it like a real person using the actual system, not merely to confirm that the code compiles.

For user-interface changes, inspecting source code or passing unit tests is not sufficient. Verify the actual rendered behavior and appearance whenever the environment permits it.

For command-line changes, run the real commands and inspect their output, exit codes, error messages, files, and side effects.

For API changes, exercise the actual endpoint or integration and inspect status codes, payloads, validation, authentication, and failure responses.

For persistence changes, verify reading, writing, migration, restart behavior, and invalid or older data where relevant.

For performance-sensitive changes, measure representative behavior instead of relying only on intuition.

For cross-platform features, test the supported platforms when possible. When direct testing is unavailable, isolate platform-dependent logic, add appropriate automated coverage, and clearly identify what remains unverified.

## Quality

- Preserve existing behavior unless the requested change intentionally alters it.
- Add focused regression coverage for behavioral changes and bug fixes.
- Validate changes at the appropriate layers.
- Run the repository checks relevant to the work.
- Verify formatting, linting, compilation, static analysis, and tests as applicable.
- For user-interface changes, verify the actual application behavior and appearance.
- Document durable architectural decisions when they are not obvious from the code.
- Keep documentation synchronized with implemented behavior.
- Do not claim that something was tested when it was not.
- Clearly distinguish between automated verification, manual verification, and unverified assumptions.
- Report failures, limitations, and environmental constraints honestly.

A change is complete when it is:

- Correctly implemented
- Properly integrated
- Appropriately reusable
- Well structured
- Sufficiently tested
- Manually verified where useful
- Documented where necessary
- Free from unnecessary complexity

Improvement should be deliberate rather than churn.

Preserve validated behavior, explain important trade-offs, and leave the project in a better state for the next incremental task.
