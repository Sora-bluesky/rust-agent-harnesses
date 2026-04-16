# Usage Examples

## Human builder, human reviewer

1. Define the failing behavior with `prompts/rust-red.prompt.md`.
2. Implement with `skills/rust-builder/SKILL.md`.
3. Run the required evidence commands.
4. Review with `skills/rust-reviewer/SKILL.md`.
5. Hold merge until findings are resolved and evidence is current.

## Agent builder, human reviewer

1. Give the builder agent the target behavior, affected files, and `rust-builder` skill.
2. Require command evidence and a concise change note.
3. Have a human reviewer use `rust-reviewer` for findings-first validation.
4. Use `rust-qa-auditor` before merge if the change affects releases or shared libraries.

## Team adoption

1. Vendor this pack into the repository.
2. Adapt command examples to the workspace if needed.
3. Keep role separation even when one person fills multiple roles; the output contract still matters.

