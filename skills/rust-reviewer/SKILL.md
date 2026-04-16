---
name: rust-reviewer
description: Perform findings-first Rust review with emphasis on correctness, safety, concurrency risk, and contract stability. Use when reviewing Rust changes before merge or release, validating an implementer's work, or producing actionable review findings instead of a summary-first response.
---

# rust-reviewer

## Purpose

Perform findings-first Rust review with emphasis on correctness, safety, and contract stability.

## When to use

Use this skill when reviewing Rust changes before merge, before release, or before handing work back to an implementer.

## Review priorities

- correctness and behavioral regressions
- memory and safety issues, including `unsafe` invariants
- concurrency hazards such as races, deadlocks, missed cancellation, ordering assumptions, or undocumented shared-state behavior
- API and contract stability, including Rust API Guidelines expectations and likely semver impact
- error semantics and diagnostic quality
- performance hotspots or obvious allocation and locking regressions
- missing tests or weak evidence

## Findings format

Present findings before summary. Each finding should include:

- severity
- affected file or area
- concrete risk
- why the current implementation is insufficient
- what evidence would close the concern

If no findings are present, say so explicitly and note any remaining test or evidence gaps.

## Primary-source cross-checks

- use The Rust Book for ownership, borrowing, error-handling, and concurrency fundamentals
- use The Rust Reference when the risk depends on precise stable-language semantics
- use Rust API Guidelines when public API naming, interoperability, predictability, or future-proofing is in scope
- use Cargo and Clippy command documentation when judging whether evidence is weak, stale, or incomplete
- use RustSec and `cargo-audit` when dependency risk is part of the review surface

## Required evidence

- patch or code context reviewed
- selected evidence profile results, or explicit blocker
- note on whether public API or behavior changed
- note on whether concurrency or `unsafe` paths were touched

## Non-goals

- restating the patch without identifying risk
- giving summary-first feedback that hides actionable issues
- requesting speculative refactors unrelated to correctness, maintainability, or evidence quality
