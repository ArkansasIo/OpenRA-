# Repository Maintenance Guide

This guide documents the practical checks to run when maintaining the OpenRA source tree in this repository.

## Project profile

OpenRA is a libre real-time strategy game engine implemented primarily in C#/.NET. This repository contains the engine, game/mod projects, launcher, server, utility tools, tests, and GitHub Actions workflows.

This project is a native game application, not a static website. GitHub Pages is therefore not a deployment target for the game itself. Documentation or a separate website can be published independently, but a working game build requires the supported .NET and platform dependencies.

## Repository areas

- `OpenRA.Game/` — shared game/runtime code.
- `OpenRA.Mods.Common/`, `OpenRA.Mods.Cnc/`, and `OpenRA.Mods.D2k/` — common traits and game/mod-specific content.
- `OpenRA.Launcher/` and `OpenRA.WindowsLauncher/` — launcher applications.
- `OpenRA.Server/` — multiplayer server.
- `OpenRA.Utility/` — developer and content utilities.
- `OpenRA.Test/` — automated tests.
- `.github/workflows/` — continuous integration, documentation, packaging, and publishing workflows.

Refer to `INSTALL.md` for the supported prerequisites and platform-specific setup.

## Recommended validation

Run these checks in an environment with the .NET SDK required by the current source tree and the native dependencies documented by `INSTALL.md`.

1. Inspect pending changes before building: `git status --short`.
2. Restore and build using the repository's documented build entry points. For CI parity, inspect `.github/workflows/ci.yml` and the `Makefile` first rather than guessing a framework or SDK version.
3. Run the repository's test target or the documented test command from `INSTALL.md`.
4. When changing YAML rules, maps, or mod content, also run the content validation tools used by the project.
5. For release changes, inspect `.github/workflows/packaging.yml` and confirm each targeted platform's packaging job succeeds.

## GitHub Actions health

The latest workflow state should always be checked on the Actions page; a successful historical run does not guarantee a later commit is healthy.

- [Continuous Integration](https://github.com/ArkansasIo/OpenRA-/actions/workflows/ci.yml)
- [Packaging](https://github.com/ArkansasIo/OpenRA-/actions/workflows/packaging.yml)
- [Documentation](https://github.com/ArkansasIo/OpenRA-/actions/workflows/documentation.yml)

## Change safety

- Keep upstream OpenRA licensing and attribution intact; review `COPYING` before redistributing modified builds.
- Avoid replacing upstream game systems wholesale for cosmetic or experimental features.
- Implement custom factions, units, missions, and rules as a mod where possible; use the Mod SDK and official modding documentation as the starting point.
- Do not commit generated build outputs, local settings, credentials, signing keys, or private service tokens.
- Prefer small, reviewable commits and run the relevant automated checks before merging.

## Useful upstream documentation

- [Installation and development setup](https://github.com/ArkansasIo/OpenRA-/blob/bleed/INSTALL.md)
- [Contributing guidelines](https://github.com/ArkansasIo/OpenRA-/blob/bleed/CONTRIBUTING.md)
- [OpenRA documentation](https://docs.openra.net/)
- [OpenRA modding guide](https://github.com/OpenRA/OpenRA/wiki/Modding-Guide)
