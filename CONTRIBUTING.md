# Contributing

## Setup

```bash
git clone https://github.com/nishal21/NekoDroid.git
cd NekoDroid
npm install
npm run build:wasm
npm run dev
```

Open http://localhost:5173

## Checks before a PR

```bash
cargo test --lib
npm run build:wasm
npm run build
```

## Layout

Work at the repo root (`src/`, `public/`). Do not publish a nested `browser-droid/` copy.

## What never belongs in a commit

Do **not** `git add .` or `git add -A`. Those pull in local junk.

Never stage:

- `browser-droid/` (local nested working copy)
- `pkg/`, `target/`, `node_modules/`, `dist/`
- `test-images/`, `*.zImage`, `*.img`, `*.cpio.gz`
- `learning-journal.md`, `handoff-devlog.md`, `.cursor/`, `.env*`
- accidental CRLF-only edits to files you did not mean to change

Leave already-tracked demo binaries alone unless you are deliberately changing them:

- `snake.*`, `theremin.*`, `vram_test.*`, `input_test.*`, `program.*`

## Safe staging (APK HLE work)

Stage only these paths (PowerShell-friendly):

```powershell
git add -- `
  .gitignore .gitattributes `
  Cargo.toml Cargo.lock `
  package.json package-lock.json `
  README.md LICENSE CONTRIBUTING.md DEVLOG.md rust-toolchain.toml `
  .github/workflows/ci.yml `
  docs/ examples/hello-apk/ public/_headers `
  src/android/ `
  src/lib.rs src/main.ts src/cp15.rs src/cpu.rs src/cpu/tests.rs `
  src/memory.rs src/memory/tests.rs `
  testdata/
git add -u -- src/counter.ts src/typescript.svg
```

Then `git status` and confirm `browser-droid/`, `pkg/`, journals, and demo binaries are **not** listed.

## Docs

- `docs/SUPPORTED_APKS.md` — which APKs the HLE path can run
- `docs/REFERENCES.md` — DEX/Dalvik specs
- `docs/OPCODE_MVP.md` — opcode coverage
- Update tracked `DEVLOG.md` when you finish a real session of work

## Scope

The APK path is a constrained HLE Dalvik runner, not full Android/ART. Prefer small test APKs without native libs. See `docs/SUPPORTED_APKS.md`.

## Before you start

You need: Rust stable with the `wasm32-unknown-unknown` target, `wasm-pack`, and Node 20 (same as CI).

## Branches

Branch from `main` and name it `fix/<short-name>`, `docs/<short-name>` or `test/<short-name>`. One issue per branch.

## Pull requests

- Link the issue in the description (`Fixes #12`)
- Say what you changed and how you checked it (paste the `cargo test --lib` summary line, or a screenshot for UI changes)
- Keep it small. If it touches more than the issue asks for, split it.
