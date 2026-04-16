# Rust Instructions

## Purpose

These instructions define stable, cross-role expectations for Rust work that uses this repository.

## Formatting and lint expectations

- keep the tree ready for the selected evidence profile, from `cargo fmt --check` through workspace-wide variants when applicable
- keep the tree ready for the selected Clippy profile, up to `cargo clippy --workspace --all-targets --all-features -- -D warnings` when the repository shape requires it
- prefer straightforward code over macro-heavy or overly abstract patterns unless the crate already uses them consistently

## `unsafe` policy

- avoid `unsafe` unless it is clearly necessary
- isolate `unsafe` to the smallest possible block
- explain the invariant that makes the block sound at the point of use; undocumented `unsafe` is incomplete work
- prefer safe wrappers around unsafe internals rather than leaking unsafe requirements into callers

## Error handling conventions

- return structured errors or clear messages that help operators and maintainers act
- do not use `unwrap` or `expect` in recoverable production paths
- preserve causal context when translating lower-level errors

## Crate and dependency hygiene expectations

- prefer existing dependencies and standard-library facilities before adding new crates
- justify new dependencies in terms of maintenance cost, security surface, and portability
- keep public APIs stable unless the task explicitly authorizes breaking changes
- evaluate public API changes against Rust API Guidelines and note likely semver impact when a public surface changes

## Testing expectations

- add or update tests when behavior changes
- start from the smallest failing behavior or verification target
- cover concurrency, parsing, boundary conditions, and error paths when they are materially affected
- for concurrent code, document ordering, cancellation, and shared-state assumptions in tests or adjacent notes when those assumptions affect correctness

## Documentation expectations

- update examples or docs when public behavior, CLI flags, or configuration surfaces change
- record notable assumptions, invariants, and limitations close to the code or in adjacent documentation
- record bootstrap blockers explicitly when a required tool such as `cargo audit` or `cargo deny` is not yet available in the consumer repository
