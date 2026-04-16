# Usage Examples

## Human builder, human reviewer

1. Define the failing behavior with `prompts/rust-red.prompt.md`.
2. Implement with `skills/rust-builder/SKILL.md`.
3. Choose an evidence profile:
   - minimal baseline for a single crate
   - workspace baseline for a workspace or broad feature coverage
   - strict profile when the repository adds tools such as `cargo deny`
4. Run the required evidence commands for that profile.
5. Review with `skills/rust-reviewer/SKILL.md`, cross-checking language, API, and evidence concerns against the linked primary sources.
6. Hold merge until findings are resolved and evidence is current.

## Agent builder, human reviewer

1. Give the builder agent the target behavior, affected files, and `rust-builder` skill.
2. Require command evidence, the selected evidence profile, and a concise change note.
3. Have a human reviewer use `rust-reviewer` for findings-first validation against the linked primary sources.
4. Use `rust-qa-auditor` before merge if the change affects releases, workspaces, or shared libraries.

## Team adoption

1. Vendor this pack into the repository.
2. Pick a default evidence profile for the repository and document any stricter local additions.
3. Treat missing `cargo audit` as a bootstrap blocker until the tool is installed or an explicit exception is recorded.
4. Keep role separation even when one person fills multiple roles; the output contract still matters.
