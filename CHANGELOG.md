## v0.3.0 (2026-11-12)

### Feat

- add Github actions (#3)
- add a readme

### Fix

- pin Github actions (#10)
- add release-cooldowns and fix JSON (#5)
- add release-cooldown to the renovate config and fix an issue with an unclosed list

## v0.2.1 (2026-07-31)

## v0.2.0 (2026-07-16)

### Feat

- add security vulnerability scanning with cargo-audit and code coverage analysis with cargo-tarpaulin
- add a hook for cargo-mutants

## v0.1.0 (2026-07-10)

### Feat

- verify-only hooks only run in pre-push, and modifying ones run in pre-commit
- add additional manual hooks
- enable cargo-check and cargo-clippy
- disable nextest hook, and enable rustfmt
- initial commit

### Refactor

- rename the hooks
