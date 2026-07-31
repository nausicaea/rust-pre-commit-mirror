# Rust Pre-Commit Hooks

This repository provides `pre-commit` hooks for maintaining Rust projects. The
hooks automatically format code, detect compilation errors, run tests, identify
lint issues, measure test effectiveness, check dependencies for known
vulnerabilities, and report code coverage.

## Motivation

Running these checks automatically helps catch problems before code is pushed
or reviewed. The goal is to:

- Keep Rust code consistently formatted.
- Detect compilation errors early.
- Ensure tests pass before changes are shared.
- Identify common code-quality issues with Clippy.
- Detect insufficient tests through mutation testing.
- Find publicly reported vulnerabilities in dependencies.
- Track code coverage over time.
- Apply safe formatting and compiler-supported fixes during development.

The hooks are split between `pre-commit` and `pre-push` to keep regular commits
fast while reserving broader validation for pushes.

## Available Hooks

### Pre-commit

These hooks can modify the working tree to fix issues:

- `cargo-fmt`: Formats Rust files with `cargo fmt`.
- `clippy-fix`: Runs Clippy and applies suggested fixes with `--allow-dirty`.
- `cargo-fix`: Checks the crate and applies compiler-supported fixes to staged files.

### Pre-push

These hooks validate the project before it is pushed:

- `cargo-fmt-check`: Verifies that files are correctly formatted.
- `cargo-check`: Checks the crate for compilation errors.
- `cargo-test`: Runs the complete test suite.
- `clippy`: Runs `cargo clippy`.
- `mutants`: Runs mutation testing with `cargo-mutants`.
- `audit`: Audits dependencies with `cargo-audit`.
- `tarpaulin`: Measures code coverage with `cargo-tarpaulin`.

The `nextest-run` hook is currently disabled because `cargo nextest` requires
the `--locked` option in this configuration.

## Usage

Install the `pre-commit` framework by following the official instructions at
[pre-commit.com](https://pre-commit.com/). Then install the Git hooks from the
repository root:

```bash
pre-commit install --hook-type pre-commit
pre-commit install --hook-type pre-push
```

Hooks will now run automatically during commits and pushes.

To run all hooks manually against the repository:

```bash
pre-commit run --all-files
```

To run a specific hook:

```bash
pre-commit run cargo-fmt
pre-commit run clippy-fix
```

Because the validation hooks use the pre-push stage, run them explicitly when
needed:

```bash
pre-commit run --hook-stage pre-push --all-files
```

The first execution may take longer while pre-commit creates environments and
installs declared command-line dependencies.

## Requirements

The project must be compatible with the tools invoked by these hooks, including
cargo-mutants, cargo-audit, and cargo-tarpaulin.

Run `pre-commit autoupdate` periodically to update hook revisions and
dependencies when appropriate.
