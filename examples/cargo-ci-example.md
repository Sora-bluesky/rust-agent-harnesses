# Cargo CI Example

Minimal evidence sequence for a Rust repository:

```bash
cargo fmt --check
cargo clippy -- -D warnings
cargo test
cargo audit
```

If `cargo audit` is not available in CI yet, record that as an explicit bootstrap blocker rather than removing it from the expected evidence contract.

