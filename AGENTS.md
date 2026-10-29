# AGENTS.md

This file provides guidance to AI coding agents (Claude Code, Codex, Cursor, GitHub Copilot) when working with code in this repository.

## Project

C++/CLI library implementing Modbus TCP (function code 16 — Write Multiple Registers) for Yaskawa MP2300S motion controllers. `MP2300SController.h/.cpp` is the library; `Main.cpp` is an interactive console test harness.

## Build

Windows-only. Requires Visual Studio 2019+ (the project uses platform toolset `v142`) with the **C++/CLI support** component, **Desktop development with C++**, and **.NET desktop development** workloads. .NET Framework 4.0+.

```bash
msbuild ModbusTCPMaster.sln /p:Configuration=Debug /p:Platform=x86
msbuild ModbusTCPMaster.sln /p:Configuration=Release /p:Platform=x64
```

Solution platforms are `x86` and `x64` (`x86` maps to the project's `Win32`); `/p:Platform=Win32` is not a valid solution platform. Only Debug|x86 builds the console harness `Debug\ModbusTCPMaster.exe`; the other three configurations build `ModbusTCPMaster.dll`. x64 output goes to `x64\<Config>\`. `.gitignore` covers `Debug` and `x64` but not `Release` — do not commit `Release\`.

No automated test suite. Manual testing against a Modbus TCP simulator on port 502.

## Conventions

- Use the type aliases (`BYTE`, `WORD`, `INT`, `DINT`) defined in `MP2300SController.h` — not raw C++ types.
- Managed allocations use `gcnew`; do not mix with native `new` for managed types.
- Protocol and frame logic stays in `MP2300SController.cpp`; `Main.cpp` is only the test harness.
- Error conditions throw `System::Exception` subclasses with messages including the Modbus error code in both decimal and hex.
- `MP2300SController.cpp` and `Main.cpp` are Windows-1252 encoded, not UTF-8; keep that encoding when editing them.
- Conventional commits with `feat/`, `fix/`, `chore/` branch prefixes. See the [Development Guide](https://github.com/rios0rios0/guide/wiki).

<!-- chlog:start -->
## Changelog (chlog) — MANDATORY

If the repository you are working in uses chlog (a `.chlog.yaml` or `.chlog.yml`
config file, or a `.changes/` directory, exists at the project root), the
following is binding and ALWAYS applies: whenever you make ANY change, you MUST
create a changelog fragment as part of the same change — automatically, without
being asked, before committing.

- Do NOT edit CHANGELOG.md directly; it is generated from fragments.
- Create the fragment with:
  `chlog new --kind <Kind> --body '<past-tense description>'`
- Write an apostrophe inside the single-quoted body as `'\''`.
- Valid kinds: Added, Changed, Deprecated, Removed, Fixed, Security
- Choose the kind that best matches the change (e.g., new feature → Added,
  bug fix → Fixed, behavior change → Changed, removal → Removed, security fix → Security).
- If the change is backward-INCOMPATIBLE with the public API (a breaking
  change), you MUST add the `--breaking` flag:
  `chlog new --kind <Kind> --breaking --body '<past-tense description>'`.
  This is the ONLY thing that triggers a major version bump — the kind alone
  never does (per SemVer, major = incompatible change). When unsure whether a
  change breaks compatibility, ask the user instead of guessing.
- Fragments are YAML files in `.changes/unreleased/`; stage them with your commit.
- `chlog check` fails the build when a fragment is missing — never skip it.
<!-- chlog:end -->
