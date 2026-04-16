# Design Basis

## Purpose

This document explains which public sources anchor the design of `rust-agent-harnesses` and how each role interprets them.

`rust-agent-harnesses` is a workflow pack for Codex-based Rust work. It is not the Rust language specification, the Cargo book, or the RustSec advisory database. Instead, it packages reusable role guidance that points back to those sources.

## Primary Sources

- [The Rust Programming Language](https://doc.rust-lang.org/stable/book/)
- [The Rust Reference](https://doc.rust-lang.org/stable/reference/)
- [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/)
- [cargo fmt](https://doc.rust-lang.org/cargo/commands/cargo-fmt.html)
- [Clippy Documentation](https://doc.rust-lang.org/clippy/)
- [cargo test](https://doc.rust-lang.org/cargo/commands/cargo-test.html)
- [RustSec Advisory Database](https://rustsec.org/)
- [cargo-audit](https://docs.rs/crate/cargo-audit/latest)

## Role Basis

### `rust-builder`

The builder role protects implementation quality while changes are being made.

It is grounded in:

- The Rust Book for ownership, borrowing, errors, testing, and concurrency fundamentals
- The Rust Reference when semantics need to be checked against stable-language behavior
- Rust API Guidelines when public API surfaces, naming, interoperability, or semver-sensitive changes are involved
- Cargo and Clippy command documentation for baseline evidence expectations

The builder role should preserve:

- ownership and borrowing correctness
- explicit error semantics
- `unsafe` invariants, documented at the point of use
- ordering, cancellation, and shared-state assumptions in concurrent code
- semver-aware public API evolution

### `rust-reviewer`

The reviewer role is findings-first and should cross-check claims against primary sources rather than relying on style preference alone.

The reviewer should use:

- The Rust Book to sanity-check idiomatic ownership, error-handling, and concurrency expectations
- The Rust Reference when behavior depends on stable-language semantics or edge-case interpretation
- Rust API Guidelines when reviewing public API naming, interoperability, predictability, and future-proofing
- Clippy and Cargo command documentation when reasoning about missing or weak evidence

The reviewer should explicitly ask which source matters for each concern:

- language behavior: Book or Reference
- public API and semver impact: API Guidelines plus the consumer crate's compatibility expectations
- evidence surface: Cargo and Clippy docs
- dependency risk: RustSec plus `cargo-audit`

### `rust-qa-auditor`

The QA auditor role interprets evidence and makes an approve, hold, or reject decision.

The QA auditor should treat the evidence profiles as:

- minimal baseline: single-crate or bootstrap CI evidence
- workspace baseline: workspace-wide evidence across targets and features
- strict profile: optional extra policy checks such as `cargo deny`, integration tests, doc verification, and benchmark notes

The QA auditor interprets evidence as follows:

- formatter and lint commands show style and static-analysis status, not full behavioral correctness
- `cargo test` shows executed unit, integration, and documentation tests for the chosen profile, but not untested paths
- `cargo audit` shows dependency vulnerability status from RustSec data, but not broader design or runtime quality
- missing required evidence is fail-closed for the selected profile unless the blocker is recorded and explicitly accepted by the consumer

## Evidence Profiles

### Minimal Baseline

- `cargo fmt --check`
- `cargo clippy -- -D warnings`
- `cargo test`
- `cargo audit`

### Workspace Baseline

- `cargo fmt --all -- --check`
- `cargo clippy --workspace --all-targets --all-features -- -D warnings`
- `cargo test --workspace --all-targets --all-features`
- `cargo audit`

### Strict Profile

- `cargo deny check`
- documentation or examples verification
- benchmark note for hot paths
- targeted integration tests

If `cargo audit` is not available yet, record a bootstrap blocker instead of silently weakening the chosen profile.

## Non-Goals

- redefining the Rust language or superseding the Rust Reference
- replacing the consumer repository's own architecture, release, or compatibility policy
- acting as a maintainer-only runbook or approval chain
- claiming that formatter, lint, test, or audit output alone is sufficient engineering judgment

## What This Repo Is

This repository is a reusable workflow pack.

It packages:

- source-backed checklists
- role definitions
- prompts
- example evidence profiles

It does not package:

- compiler semantics beyond what the linked Rust sources define
- hidden repository-specific state
- proprietary internal practices
