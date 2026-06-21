# AGENTS.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Current repository state
- This repository currently has no commits and no source files (only `.git` is present).
- There is no established build, lint, or test toolchain yet.

## Commands
- Git status:
  - `git --no-pager status --short --branch`
- List repository files:
  - `ls -la`

Until project files are added, there are no valid project-specific commands for build, lint, test, or single-test execution.

## Architecture
- No application architecture exists yet in this repository.
- After the initial project scaffold is added, update this file with:
  - The main entry points and runtime flow.
  - The module/layer boundaries and ownership.
  - The canonical build/lint/test commands, including single-test execution.

## Existing assistant-rule files
- No `WARP.md`, `CLAUDE.md`, `.cursorrules`, `.cursor/rules/`, or `.github/copilot-instructions.md` files were found.
- If any of these files are added later, sync their important repository-specific instructions into this document.
