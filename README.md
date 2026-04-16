# rust-agent-harnesses

## Overview

`rust-agent-harnesses` is a public-safe Codex starter pack for Rust implementation, review, and QA workflows that benefit from explicit role separation and evidence-driven quality gates.

This repository is for teams that want reusable guidance for:

- implementation work through a builder role
- findings-first code review through a reviewer role
- release or merge readiness checks through a QA auditor role

The pack is intentionally small. It focuses on durable, reusable guidance and avoids project-specific operations, private infrastructure, or maintainer-only process wording.

The repository is meant to be installed into a consuming repository's `.codex/` directory, where Codex can use the bundled skills, instructions, and prompts as workflow assets.

## What This Pack Is Based On

This pack is not a trained model or a Rust framework. It is a hand-authored workflow pack that encodes reusable guidance for Codex-based Rust work.

The skills and prompts are based on:

- Codex skill and `.codex/` layout conventions
- language fundamentals from The Rust Programming Language, especially ownership, borrowing, lifetimes, error handling, testing, and concurrency basics
- language and reference semantics from The Rust Reference when review or QA work must check stable-language behavior rather than rule-of-thumb usage
- API design guidance from the Rust API Guidelines when public API changes, naming, interoperability, predictability, and future-proofing are in scope
- formatter, lint, and test commands from the Cargo Book and Clippy documentation, using the documented `cargo fmt`, `cargo clippy`, and `cargo test` command surfaces as the baseline evidence contract
- dependency vulnerability checks from RustSec and `cargo-audit`, treating advisory data as one evidence source within QA rather than a complete quality signal
- role separation between implementation, review, and QA decision-making

In other words, the repository packages procedural knowledge and review checklists, not model weights or hidden repository-specific state.

It does not rely on:

- private project history
- local operator runbooks
- proprietary infrastructure
- unpublished maintainer-only approval flows

See [docs/design-basis.md](docs/design-basis.md) for the source-to-role mapping that explains how each skill uses these inputs.

## Primary Sources

- [The Rust Programming Language](https://doc.rust-lang.org/stable/book/): provides the language fundamentals that shape builder expectations around ownership, borrowing, errors, testing, and concurrency basics.
- [The Rust Reference](https://doc.rust-lang.org/stable/reference/): provides the stable-language reference used when reviewer or QA guidance needs semantic confirmation rather than convention.
- [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/): informs public API review, naming, interoperability, predictability, and future-proofing checks.
- [cargo fmt](https://doc.rust-lang.org/cargo/commands/cargo-fmt.html): defines the formatter command surface used in the evidence baseline and workspace profiles.
- [Clippy Documentation](https://doc.rust-lang.org/clippy/): defines the lint command surface and explains the lint categories used by the evidence contract.
- [cargo test](https://doc.rust-lang.org/cargo/commands/cargo-test.html): defines the test command surface for unit, integration, and documentation test execution.
- [RustSec Advisory Database](https://rustsec.org/): provides the vulnerability data source that informs dependency-risk checks in QA.
- [cargo-audit](https://docs.rs/crate/cargo-audit/latest): defines the Cargo subcommand used to turn RustSec advisory data into an actionable dependency audit step.

## Roles

The repository defines three roles:

- `rust-builder`: implement or change Rust code with an explicit engineering checklist
- `rust-reviewer`: review Rust changes with findings first, prioritizing correctness and risk
- `rust-qa-auditor`: validate evidence and quality gates before merge or release decisions

These roles can be used by humans, AI agents, or mixed human-plus-agent workflows. The important part is clear responsibility boundaries and a shared evidence contract.

## Expected Verification Evidence

Use one of these profiles and record which profile was chosen for a given change.

### Minimal Baseline

Use this when the consumer repository is a single crate or is still bootstrapping its CI surface.

- `cargo fmt --check`
- `cargo clippy -- -D warnings`
- `cargo test`
- `cargo audit`

### Workspace Baseline

Use this when the consumer repository is a workspace or needs wider target and feature coverage.

- `cargo fmt --all -- --check`
- `cargo clippy --workspace --all-targets --all-features -- -D warnings`
- `cargo test --workspace --all-targets --all-features`
- `cargo audit`

### Strict Profile

Use this when the consumer repository wants stronger release gates or broader supply-chain checks.

- `cargo deny check`
- documentation or examples verification
- benchmark note for hot paths
- targeted integration tests

Every profile should still include:

- concise findings summary and notable limitations
- explicit note when public API, concurrency behavior, or `unsafe` usage changed
- explicit blocker handling when a command could not be run

If `cargo audit` is not available yet, treat that as a bootstrap blocker for the selected profile and record the blocker explicitly instead of silently omitting the command.

## Installation

Copy the files you need into your repository, or vendor this repository as a reference pack.

Suggested layout in a consuming repository:

```text
.codex/
├─ skills/
│  ├─ rust-builder/
│  │  └─ SKILL.md
│  ├─ rust-reviewer/
│  │  └─ SKILL.md
│  └─ rust-qa-auditor/
│     └─ SKILL.md
├─ instructions/
│  └─ rust.instructions.md
└─ prompts/
   ├─ rust-red.prompt.md
   └─ rust-refactor.prompt.md
```

Install in this order:

1. Copy `instructions/rust.instructions.md` as the stable baseline.
2. Add the role skills from `skills/`.
3. Add the prompts from `prompts/`.
4. Adapt the examples in `examples/` to match your repository layout and CI commands.

## Usage Patterns

Common usage patterns:

- Builder only: one contributor uses the builder checklist and captures evidence before review.
- Builder plus reviewer: implementation and review are separated, with the reviewer producing findings-first output.
- Builder plus reviewer plus QA auditor: evidence is normalized and audited before merge or release.
- AI-assisted workflow: human owners keep decision authority while agents follow the same role boundaries and evidence expectations.

Recommended operating rules:

- keep prompts small and task-specific
- keep evidence concrete and reproducible
- separate implementation from review whenever possible
- record blockers and assumptions explicitly

## Example Workflow

1. Use `prompts/rust-red.prompt.md` to define the smallest failing behavior or verification target.
2. Implement with `skills/rust-builder/SKILL.md`.
3. Capture evidence with the minimal baseline, workspace baseline, or strict profile that matches the repository.
4. Review the change with `skills/rust-reviewer/SKILL.md`.
5. Validate the evidence package with `skills/rust-qa-auditor/SKILL.md`.
6. Use `prompts/rust-refactor.prompt.md` after tests are green to simplify structure without semantic drift.

See `examples/usage-examples.md` for concrete adoption patterns.

## Limitations

- This repository is a reusable harness pack, not the Rust language specification itself.
- Final engineering judgment stays with the consuming team or repository owner.
- The command set in this repository is a baseline; consuming repositories may need to adjust it for workspace layout, platform constraints, or additional policy tools.
- `cargo audit` provides a dependency vulnerability view and does not replace code review, testing, API review, or broader QA judgment.

## Non-Goals

This repository does not include:

- private maintainer workflows
- issue or roadmap bookkeeping
- approval chain wording tied to one organization
- machine-specific paths
- live-ops or production-control behavior
- project-specific handoff conventions

## License

This repository is released under the MIT License. See [LICENSE](LICENSE).
