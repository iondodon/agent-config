# Linux Office Agent Guidelines

These instructions apply to the entire repository.

This is an evolving project, not a rigid implementation of a fully known final
design. It is being built incrementally, and each task may reveal a better
structure, abstraction, style, workflow, or low-level approach. Treat the
current code as the best-known design so far, not as something that must remain
unchanged.

## Development Lifecycle

Treat each task as an incremental improvement to the project, not merely as an
isolated implementation request. Consider the complete development lifecycle:
discovery, architectural impact, preparation, implementation, integration,
migration, verification, documentation, and future maintenance.

Before proposing or implementing a change:

1. Gather the information needed to understand the request and the current
   system.
2. Locate and inspect the relevant code, architecture, tests, dependencies,
   product boundaries, and nearby patterns.
3. Assess how the task affects the project from the highest relevant level down
   to implementation details, including user experience, existing behavior,
   other products, and future development.
4. Identify any preparation needed for a clean solution, such as refactoring,
   moving ownership, clarifying an interface, replacing an unsuitable approach,
   or adding missing infrastructure.
5. Present the proposed solution, important trade-offs, preparatory changes,
   and decisions that could materially affect the direction. Ask questions when
   the answer cannot be established from the project or requirements.

Discuss and refine the direction with the user, and wait for explicit approval
before implementation. When the user has already approved the direction and
asked to proceed, implement without repeating that discussion unnecessarily.

Choose the scope required for a coherent, reliable, and maintainable result,
not simply the smallest change suggested by the apparent size of the task. A
substantial refactor is appropriate even for a small feature when the evidence
shows that it is necessary and will materially improve current integration or
future development. Keep such work purposeful and connected to the task.

The final user experience and functionality are the primary outcomes. Code,
architecture, and process serve those outcomes, so change any of them when
needed. Integrate each implementation with the existing system, preserve or
improve the behavior of affected areas, and verify the result at every relevant
layer.

## Engineering Principles

- Put behavior in the layer that owns it.
- Keep product-specific logic separate from shared office-suite
  infrastructure.
- Design generally useful capabilities so future office products can reuse
  them without depending on Writer or another product.
- Prefer existing abstractions and conventions when they fit.
- Introduce a new abstraction only when it establishes a real ownership
  boundary, removes meaningful duplication, or supports a concrete reusable
  capability.
- Refactor adjacent code when necessary to integrate a change cleanly, improve
  structure, or restore the correct dependency direction.
- Make the best architectural decision supported by the current task and
  available evidence. Do not preserve an earlier decision only because it
  already exists.
- Modules, crates, APIs, components, styles, and implementation strategies may
  be created, split, combined, moved, replaced, or removed when that improves
  the project.
- Apply this willingness to improve at every level, from overall architecture
  and product boundaries to naming, control flow, data structures, tests,
  tooling, and user experience.
- Avoid unrelated refactoring and premature generalization.
- Keep application entry points focused on bootstrap and composition rather
  than feature implementation.
- Keep platform-specific and framework-specific details behind clear
  interfaces so shared logic remains portable.
- Make behavior, defaults, state transitions, and data conversions explicit
  and deterministic. Avoid hidden side effects, environment-dependent guessing,
  and implicit fallback paths.
- Fail clearly when an operation cannot satisfy its contract instead of
  silently substituting behavior, discarding information, repairing data, or
  reducing functionality. Any necessary fallback must be deliberate,
  observable, documented, and testable.
- Favor established open standards and interoperable formats for user-facing
  data, protocols, and integration boundaries. Prefer proven libraries,
  protocols, platform facilities, and other existing solutions when they meet
  the requirements. Create custom alternatives only for a concrete,
  documented reason, and keep custom representations internal when possible.
- Treat Linux, Windows, and macOS as primary platforms when designing shared
  behavior. Linux support is native Wayland.

## Reuse And Structure

For each implementation, consider:

1. Is this behavior specific to one product, or useful across the office suite?
2. Does an existing module or component already own it?
3. Would placing it locally cause another product to duplicate it later?
4. Can the reusable part be separated from the product-specific semantics?
5. Does the change leave the code easier to extend and test?

Share infrastructure and contracts, not one universal model for every office
product. Writer, spreadsheets, presentations, notes, and other products may
reuse services while retaining their own domain models and workflows.

Reason at every relevant level, starting with the highest level affected:
office suite, product, subsystem, crate or module, type or function, and
implementation detail. Check that local decisions support the broader product
direction and that broader abstractions remain grounded in concrete needs.

The product placeholders under `apps/` are architectural context, not a fixed
roadmap. Products and boundaries may be added, removed, renamed, split, or
combined as the project evolves.

## Quality

- Preserve existing behavior unless the requested change intentionally alters
  it.
- Add focused regression coverage for behavioral changes and bug fixes.
- Validate changes at the appropriate layer and run the repository checks
  relevant to the work.
- For user-interface changes, verify the actual application behavior and
  appearance.
- Document durable architectural decisions when they are not obvious from the
  code.

A change is complete when it is correctly integrated, appropriately reusable,
well-structured, and verified without introducing unnecessary complexity.
Improvement should be deliberate rather than churn: preserve validated
behavior, explain important trade-offs, and leave the project in a better state
for the next incremental task.
