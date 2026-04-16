# Rust Instructions

## Purpose

These instructions define stable, cross-role expectations for Rust work that uses this repository.

## Formatting and lint expectations

- keep the tree ready for `cargo fmt --check`
- keep the tree ready for `cargo clippy -- -D warnings`
- prefer straightforward code over macro-heavy or overly abstract patterns unless the crate already uses them consistently

## `unsafe` policy

- avoid `unsafe` unless it is clearly necessary
- isolate `unsafe` to the smallest possible block
- explain the invariant that makes the block sound
- prefer safe wrappers around unsafe internals rather than leaking unsafe requirements into callers

## Error handling conventions

- return structured errors or clear messages that help operators and maintainers act
- do not use `unwrap` or `expect` in recoverable production paths
- preserve causal context when translating lower-level errors

## Crate and dependency hygiene expectations

- prefer existing dependencies and standard-library facilities before adding new crates
- justify new dependencies in terms of maintenance cost, security surface, and portability
- keep public APIs stable unless the task explicitly authorizes breaking changes

## Testing expectations

- add or update tests when behavior changes
- start from the smallest failing behavior or verification target
- cover concurrency, parsing, boundary conditions, and error paths when they are materially affected

## Documentation expectations

- update examples or docs when public behavior, CLI flags, or configuration surfaces change
- record notable assumptions, invariants, and limitations close to the code or in adjacent documentation

