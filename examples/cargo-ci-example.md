# Cargo CI Example

## Minimal baseline

```bash
cargo fmt --check
cargo clippy -- -D warnings
cargo test
cargo audit
```

## Workspace baseline

```bash
cargo fmt --all -- --check
cargo clippy --workspace --all-targets --all-features -- -D warnings
cargo test --workspace --all-targets --all-features
cargo audit
```

## Strict profile additions

```bash
cargo deny check
```

Optional strict-profile additions:

- docs or examples verification
- benchmark note for hot paths
- targeted integration tests

If `cargo audit` is not available in CI yet, record that as an explicit bootstrap blocker rather than removing it from the selected evidence profile.
