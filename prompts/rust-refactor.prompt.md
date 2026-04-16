# Rust Refactor Prompt

Improve structure while preserving already-green behavior.

Instructions:

- start from passing tests and current evidence
- remove duplication and reduce incidental complexity
- keep public behavior, error semantics, and concurrency guarantees unchanged
- preserve documented `unsafe` invariants, ordering assumptions, cancellation behavior, and shared-state assumptions
- avoid silent semantic drift
- rerun the relevant checks after refactoring

Output:

- concise description of the structural improvement
- note confirming what behavior was preserved
- updated evidence summary, including the evidence profile used
