# rust-reviewer

## Purpose

Perform findings-first Rust review with emphasis on correctness, safety, and contract stability.

## When to use

Use this skill when reviewing Rust changes before merge, before release, or before handing work back to an implementer.

## Review priorities

- correctness and behavioral regressions
- memory and safety issues, including `unsafe` invariants
- concurrency hazards such as races, deadlocks, missed cancellation, or ordering assumptions
- API and contract stability
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

## Required evidence

- patch or code context reviewed
- test and lint evidence, or explicit blocker
- note on whether public API or behavior changed
- note on whether concurrency or `unsafe` paths were touched

## Non-goals

- restating the patch without identifying risk
- giving summary-first feedback that hides actionable issues
- requesting speculative refactors unrelated to correctness, maintainability, or evidence quality

