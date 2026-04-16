---
name: rust-builder
description: Guide Rust implementation work with an explicit checklist for correctness, maintainability, and verification evidence. Use when writing, changing, or extending Rust code; implementing a bug fix or feature; or driving a disciplined builder role in a Rust workflow.
---

# rust-builder

## Purpose

Guide Rust implementation work with an explicit checklist that keeps behavior, maintainability, and verification evidence in scope.

## When to use

Use this skill when you are writing, changing, or extending Rust code and need a disciplined implementation path instead of ad hoc edits.

## Inputs expected

- task goal and intended user-visible behavior
- relevant files, modules, or crate boundaries
- current failing test, bug report, or verification target
- constraints such as public API stability, performance limits, or MSRV expectations

## Build/implementation checklist

- define the smallest behavior change to make
- identify the crate, module, and API surface affected
- preserve ownership and borrowing clarity; prefer simple lifetimes over clever indirection, using The Rust Book and the Rust Reference when semantics need confirmation
- make error handling explicit and meaningful; avoid lossy `unwrap` or vague error text in production paths
- check public API stability before renaming types, functions, features, or error variants; review Rust API Guidelines expectations and note semver impact explicitly
- document concurrency assumptions for shared state, async work, or channel boundaries; include ordering, cancellation, and shared-state assumptions when they matter
- minimize `unsafe`; if `unsafe` is necessary, narrow the block and explain the invariant being protected at the point of use
- keep dependencies intentional; prefer standard library or existing crate patterns before adding new crates
- leave the code ready for the selected evidence profile, from minimal baseline through workspace or strict checks
- capture verification evidence before claiming completion, and record bootstrap blockers instead of silently weakening the profile

## Expected outputs

- implementation aligned to the requested behavior
- updated or added tests when behavior changed
- concise note describing what changed, why, and which evidence profile was used
- explicit blockers or residual risks when verification is incomplete

## Required evidence

- selected evidence profile command results:
  - minimal baseline: `cargo fmt --check`, `cargo clippy -- -D warnings`, `cargo test`, `cargo audit`
  - workspace baseline when applicable: `cargo fmt --all -- --check`, `cargo clippy --workspace --all-targets --all-features -- -D warnings`, `cargo test --workspace --all-targets --all-features`, `cargo audit`
- command output or concise summary for any environment blocker
