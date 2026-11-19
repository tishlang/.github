# tishlang/.github

The [`tishlang`](https://github.com/tishlang) organization profile and org-wide community health defaults.

- **[`profile/README.md`](profile/README.md)**: the page shown at github.com/tishlang.
- **`.github/ISSUE_TEMPLATE/`**: applies to every repo in the org that doesn't provide its own.

## Issue templates

- **🐞 Bug report**: structured for Tish. It asks for the fields that make a bug fixable fast: **which
  target/backend** is affected and **which are correct** (most codegen bugs are backend-specific,
  e.g. the `rust` native backend mis-compiles while VM/JS are correct), the exact `tish -V` and install
  method, OS/arch, a **minimal runnable repro** (or a note that it only reproduces in a full
  program), and the **full output / exit code** (137 = SIGKILL, etc.), plus whether a hang spins or blocks.
- **💡 Feature request**: problem, proposal, area, alternatives.

A repo can override these by adding its own `.github/ISSUE_TEMPLATE/`.
