# rust-qa-auditor

## Purpose

Validate Rust evidence and quality gates before merge or release decisions.

## When to use

Use this skill after implementation and review are complete, or when a maintainer needs a clear go/no-go decision based on evidence.

## Evidence checklist

Required evidence:

- `cargo fmt --check`
- `cargo clippy -- -D warnings`
- `cargo test`
- `cargo audit`

Optional supporting evidence:

- benchmark or performance note for hot-path changes
- targeted integration-test output
- docs or examples verification when public-facing behavior changed

Every missing item must be explained with a blocker or rationale.

## Decision rules

- approve only when required evidence is present and there are no unresolved high-severity findings
- hold when required evidence is missing, stale, or contradicted by code or review findings
- reject when correctness, safety, or release risk remains unresolved
- distinguish environment blockers from product risk; both matter, but they are not the same failure mode

## Output contract

Produce:

- decision: `approve`, `hold`, or `reject`
- evidence status for each required check
- unresolved findings or blockers
- explicit next action required to move forward

