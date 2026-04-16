# Repo Layout Example

Example consumer layout:

```text
my-rust-project/
├─ .codex/
│  ├─ skills/
│  │  ├─ rust-builder/
│  │  │  └─ SKILL.md
│  │  ├─ rust-reviewer/
│  │  │  └─ SKILL.md
│  │  └─ rust-qa-auditor/
│  │     └─ SKILL.md
│  ├─ instructions/
│  │  └─ rust.instructions.md
│  └─ prompts/
│     ├─ rust-red.prompt.md
│     └─ rust-refactor.prompt.md
├─ docs/
│  └─ engineering-evidence.md
├─ src/
├─ tests/
├─ Cargo.toml
└─ README.md
```

The consuming repository keeps ownership of its own commands, CI policies, semver promises, and release process. This pack only provides reusable role guidance, prompts, and evidence profiles.
