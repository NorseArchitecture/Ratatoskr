# CLAUDE.md — Ratatoskr (`Norse.NServiceBus`)

## 0. Wrong Root — Halt

Session root must be **Bifröst**, not this repo directly — org-wide settings (`superpowers`, permission rules) only apply from the actual root, and Claude Code never merges a submodule's own `.claude/settings.json` into a parent-launched session. If `claude` was run from inside **Ratatoskr**, stop: don't read further, don't propose changes, don't run anything — tell the user to `cd ../Bifrost` and start there. (This repo's `.claude/settings.json` carries a `SessionStart` hook meant to block this before you ever see this file; if you're reading this anyway, the hook was bypassed, disabled, or failed — halt regardless.)

> **Do not commit, push, or rewrite git history** — stage (`git add`), show the diff, stop; the human reviews and commits. This applies even when a skill's flow includes a commit step. **US English spelling** everywhere — code, comments, docs, commits.

## 1. What This Repository Is

Ratatoskr is **the squirrel** — `Norse.NServiceBus`: NServiceBus endpoint configuration, saga infrastructure, message conventions, and transport wiring. It is the NServiceBus-specific implementation layer carved from Midgard for the same reason Urðarbrunnr was: NServiceBus has strong opinions (sagas, message conventions, endpoint configuration, licensing) that should not seep into `Norse.Infrastructure`, it has its own versioning and licensing lifecycle independent of the core abstractions, and not every Midgardian implementation will use it — some may use MassTransit, Rebus, Azure Service Bus SDK directly, or something else entirely.

Asgard (`Norse.Abstractions`) declares the messaging surface — `IPublishEvent<T>`, `ISendCommand<T>`, `IHandleMessage<T>`, and the like — without caring how the squirrel carries them. Ratatoskr is the carrier; the Æsir never need to know it exists.

In the dependency chain: Ratatoskr sits above Asgard and Svartálfheim (it depends on their contracts and primitives), alongside Midgard (neither depends on the other), and below Yggdrasil (the hosting chassis wires it in).

This repo is currently a bare shell (LICENSE + README only) — no specs have converged here yet. Before writing any code: brainstorm → spec → plan, recorded in `../Glitnir/docs/Ratatoskr/`, per the org's spec-first discipline. Do not scaffold a project structure ahead of a converged spec. When that plan is written, its REQUIRED SUB-SKILL line names `superpowers:subagent-driven-development` as the default (not a recommendation among equals — `executing-plans` is the narrow fallback for separate-session review checkpoints) paired with `superpowers:test-driven-development` — implementation here is subagent-orchestrated and test-driven, never one without the other (`../Glitnir/CLAUDE.md` §2.8).

See `../Bifrost/CLAUDE.md` (§2 The Naming Model) and `../Glitnir/CLAUDE.md` (§3 Bounded Context Map, §4 Messaging) for the full realm table, the messaging decision (NServiceBus 10.2, `ReceiveOnly`, source-generated handler registration), and how Ratatoskr fits the rest of the cosmos.
