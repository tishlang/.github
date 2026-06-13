# tishlang/.github

Org-wide community health defaults for [`tishlang`](https://github.com/tishlang) repositories.

Files here apply to every repo in the org that doesn't provide its own.

## Issue templates (`.github/ISSUE_TEMPLATE/`)

- **🐞 Bug report** — structured for Tish. The fields that make a bug fixable fast: **which
  target/backend** is affected vs. **which are correct** (most codegen bugs are backend-specific —
  e.g. the `rust` native backend mis-compiles while VM/JS are correct), exact `tish -V` + install
  method, OS/arch, a **minimal runnable repro** (or a note that it only reproduces in a full
  program), and the **full output / exit code** (137 = SIGKILL, etc.) with spin-vs-block for hangs.
- **💡 Feature request** — problem, proposal, area, alternatives.

A repo can override these by adding its own `.github/ISSUE_TEMPLATE/`.
