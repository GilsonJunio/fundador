# AGENTS.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.
## Current repository state
- This repository is an Astro project (`astro@^6.4.7`) with a single page implementation.
- Runtime requirement is Node `>=22.12.0` (`package.json` engines).
- The current page is narrative-driven and implemented in `src/pages/index.astro`.
- Build commands are established (`npm run dev`, `npm run build`, `npm run preview`), but no lint/test commands are configured yet.

## Commands
- Git status:
  - `git --no-pager status --short --branch`
- List repository files:
  - `ls -la`
- Install dependencies:
  - `npm ci`
- Run development server:
  - `npm run dev -- --host 0.0.0.0 --port 4321`
- Build production output:
  - `npm run build`
- Preview production build:
  - `npm run preview -- --host 0.0.0.0 --port 4321`
- Astro CLI:
  - `npm run astro -- --help`

### Container-first workflow (preferred in this repository)
- The repository uses Podman-based development to avoid host-level package installation.
- Install dependencies into dedicated container volume:
  - `podman run --rm --userns=keep-id -v "$PWD":/workspace:Z -v fundador_node_modules:/workspace/node_modules -w /workspace docker.io/library/node:22 bash -lc "npm ci"`
- Start dev server in background (host network, stable local access on 4321):
  - `podman run -d --name fundador-dev --userns=keep-id --network host -v "$PWD":/workspace:Z -v fundador_node_modules:/workspace/node_modules -w /workspace docker.io/library/node:22 bash -lc "npm run dev -- --host 0.0.0.0 --port 4321"`
- Stop and remove dev container:
  - `podman rm -f fundador-dev`

## Testing and quality checks
- There is no test suite configured yet (no unit/integration test scripts in `package.json`).
- Single-test execution is not available yet for this repository.
- Canonical validation today is a production build:
  - `npm run build`

## Architecture
- App type: static Astro site (output generated to `dist/` by `astro build`).
- Entry point and routing:
  - `src/pages/index.astro` defines the main `/` route.
- Styling approach:
  - CSS is currently inlined in `src/pages/index.astro` inside a `<style>` block (no external CSS pipeline configured yet).
- Static assets:
  - Public assets are served from `public/` (for example, profile image and favicons).
- Configuration:
  - `astro.config.mjs` currently uses default `defineConfig({})`.
- Build/runtime flow:
  - Development uses Astro dev server (`npm run dev`).
  - Production output is generated into `dist/` by `npm run build`.

## Existing assistant-rule files
- No `WARP.md`, `CLAUDE.md`, `.cursorrules`, `.cursor/rules/`, or `.github/copilot-instructions.md` files were found.
- If any of these files are added later, sync their important repository-specific instructions into this document.
