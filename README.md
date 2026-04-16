# rust-agent-harnesses

## Overview

`rust-agent-harnesses` is a public-safe starter pack for Rust implementation, review, and QA workflows that benefit from explicit role separation and evidence-driven quality gates.

This repository is for teams that want reusable guidance for:

- implementation work through a builder role
- findings-first code review through a reviewer role
- release or merge readiness checks through a QA auditor role

The pack is intentionally small. It focuses on durable, reusable guidance and avoids project-specific operations, private infrastructure, or maintainer-only process wording.

## Roles

The repository defines three roles:

- `rust-builder`: implement or change Rust code with an explicit engineering checklist
- `rust-reviewer`: review Rust changes with findings first, prioritizing correctness and risk
- `rust-qa-auditor`: validate evidence and quality gates before merge or release decisions

These roles can be used by humans, AI agents, or mixed human-plus-agent workflows. The important part is clear responsibility boundaries and a shared evidence contract.

## Expected Verification Evidence

The default evidence set is:

- `cargo fmt --check`
- `cargo clippy -- -D warnings`
- `cargo test`
- `cargo audit`
- concise findings summary and notable limitations

Optional evidence may include:

- benchmark notes for performance-sensitive changes
- targeted integration-test output
- documentation verification when public APIs or operator-facing behavior changes

If a command cannot be run in the current environment, record the blocker explicitly instead of silently omitting it.

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
3. Capture formatter, lint, test, and audit evidence.
4. Review the change with `skills/rust-reviewer/SKILL.md`.
5. Validate the evidence package with `skills/rust-qa-auditor/SKILL.md`.
6. Use `prompts/rust-refactor.prompt.md` after tests are green to simplify structure without semantic drift.

See `examples/usage-examples.md` for concrete adoption patterns.

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

