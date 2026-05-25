# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

C++/CLI DLL implementing Modbus TCP (function code 16 — Write Multiple Registers) for Yaskawa MP2300S motion controllers. Two source files: `MP2300SController.h/.cpp` (library) and `Main.cpp` (interactive console test harness).

## Build

Windows-only. Requires Visual Studio 2017+ with the **C++/CLI support** component, **Desktop development with C++**, and **.NET desktop development** workloads. .NET Framework 4.0+.

```bash
msbuild ModbusTCPMaster.sln /p:Configuration=Debug /p:Platform=Win32
msbuild ModbusTCPMaster.sln /p:Configuration=Release /p:Platform=x64
```

No automated test suite. Manual testing against a Modbus TCP simulator on port 502.

## Conventions

- Use the type aliases (`BYTE`, `WORD`, `INT`, `DINT`) defined in `MP2300SController.h` — not raw C++ types.
- Managed allocations use `gcnew`; do not mix with native `new` for managed types.
- Protocol and frame logic stays in `MP2300SController.cpp`; `Main.cpp` is only the test harness.
- Error conditions throw `System::Exception` subclasses with messages including the Modbus error code in both decimal and hex.
- Conventional commits with `feat/`, `fix/`, `chore/` branch prefixes. See the [Development Guide](https://github.com/rios0rios0/guide/wiki).
