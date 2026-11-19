# Tish

**A TypeScript- and JavaScript-compatible language, implemented in Rust.** The same source runs on an
interpreter or a bytecode VM, or compiles to standalone native binaries, WASM/WASI or JavaScript.
I/O is opt-in, `undefined` doesn't exist, and type annotations turn into real machine types on the
native backend.

**[tishlang.com](https://tishlang.com)** ·
**[Docs](https://tishlang.com/docs)** ·
**[Language spec](https://github.com/tishlang/tish/blob/main/docs/LANGUAGE.md)** ·
**[Playground](https://github.com/tishlang/tish-playground)** ·
**[npm](https://www.npmjs.com/package/@tishlang/tish)** ·
**[crates.io](https://crates.io/crates/tishlang)**

## Install

```sh
brew tap tishlang/tish https://github.com/tishlang/tish && brew install tish
# or
npm install @tishlang/tish
```

Start a project with `npx @tishlang/create-tish-app my-app`.

## Run it, then ship it

```tish
// path.tish
type Point = { x: number, y: number }

fn dist(a: Point, b: Point): number {
  let dx = a.x - b.x
  let dy = a.y - b.y
  return Math.sqrt(dx * dx + dy * dy)
}

let path: Point[] = [{ x: 0, y: 0 }, { x: 3, y: 4 }, { x: 6, y: 8 }]
let total = 0
for (let i = 1; i < path.length; i++) { total += dist(path[i - 1], path[i]) }
console.log(`path length: ${total}`)
```

```sh
tish run path.tish                       # interpret: path length: 10
tish build path.tish -o path             # standalone native binary, no runtime needed
tish build path.tish --target js -o path.js
tish build path.tish --target wasi -o path.wasm
```

On the native backend, `Point` becomes a Rust struct and `Point[]` a `Vec`, so typed hot loops run
unboxed. Anything the compiler can't prove falls back to the dynamic path. Network, filesystem and
process APIs are compiled in only with `--feature http|fs|process`.

## Toolchain

| Tool | What it does |
| --- | --- |
| `tish` | `run`, `repl`, `build` (native via Rust, Cranelift or LLVM; `wasm`, `wasi`, `js`, `bytecode`) |
| `tish-fmt` · `tish-lint` | Formatter and linter (`--format sarif` for code scanning) |
| `tish-lsp` | Language server, with gradual type checking as you type |
| [tish-vscode](https://github.com/tishlang/tish-vscode) | VS Code grammar, snippets, LSP client and tasks |

## Repositories

| Layer | Repository | What's in it |
| --- | --- | --- |
| Language | **[tish](https://github.com/tishlang/tish)** | Compiler, interpreter, VM, CLI, LSP, formatter, linter and spec |
| | **[tish-vscode](https://github.com/tishlang/tish-vscode)** | Editor support for VS Code |
| | **[tish-syntax-highlight](https://github.com/tishlang/tish-syntax-highlight)** | Pure-Tish syntax highlighter that emits `hljs`-style spans |
| | **[tishdoc-parse](https://github.com/tishlang/tishdoc-parse)** · **[tishdoc-render-html](https://github.com/tishlang/tishdoc-render-html)** | Markdown/tishdoc parsing (mdx, yaml or json frontmatter) and HTML rendering |
| | **[sem](https://github.com/tishlang/sem)** | Semver, conventional commits and a GitHub Action, with no dependencies |
| UI | **[lattish](https://github.com/tishlang/lattish)** | JSX and a React-like micro framework for Tish |
| | **[tish-tailwind](https://github.com/tishlang/tish-tailwind)** | Tailwind-style CSS preprocessor for web and native Tish apps |
| | **[tish-desktop](https://github.com/tishlang/tish-desktop)** | A native reactive desktop webview driven only by Tish |
| | **[tish-apple](https://github.com/tishlang/tish-apple)** · **[tish-ms](https://github.com/tishlang/tish-ms)** | Native hosts: macOS/iOS crates, and Win32/Direct2D with Windows services |
| Web | **[orbit](https://github.com/tishlang/orbit)** | Markdown-first web framework: static, server or incremental per route |
| | **[tish-browser-server](https://github.com/tishlang/tish-browser-server)** | `http`, `fs` and `process` in the browser (Service Worker, IndexedDB), in pure Tish |
| | **[tish-playground](https://github.com/tishlang/tish-playground)** | Tish in the browser via WASM |
| Learn | **[learn](https://github.com/tishlang/learn)** | Learn to code with Tish |
| | **[tishlang.com](https://github.com/tishlang/tishlang.com)** · **[lattish.com](https://github.com/tishlang/lattish.com)** | The sites and docs |

## Built with Tish

- **[Orbit](https://github.com/tishlang/orbit)**: the web framework, written in Tish, that runs [space.la](https://space.la).
- **[Moo](https://github.com/moomoi)**: a keyboard launcher for macOS and Windows. It's one native
  process with no webview, and its plugins are written in Tish.

## Contributing

Build and test instructions are in
[CONTRIBUTING.md](https://github.com/tishlang/tish/blob/main/CONTRIBUTING.md). Bug reports go fastest
with the **target or backend** that fails and the ones that work (`rust`, `cranelift`, VM or `js`),
the output of `tish -V`, and a minimal repro. The [issue form](https://github.com/tishlang/tish/issues/new/choose)
asks for each of these. MIT licensed.
