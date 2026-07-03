# CLAUDE.md — Ratatoskr (`Norse.NServiceBus`)

## 0. Wrong Root — Halt

If you are reading this because **Ratatoskr itself is the Claude Code session root** — someone ran `claude` from inside this directory instead of `../Bifrost` — stop here. Do not read further, do not propose changes, do not run anything.

Tell the user: every Norse Architecture session starts from **Bifrost**. Org-wide settings (the `superpowers` plugin, permission rules) only apply when Bifrost is the actual session root — Claude Code never merges a submodule's own `.claude/settings.json` into a parent-launched session. Exit, `cd ../Bifrost`, and run `claude` there instead.

This repo's own `.claude/settings.json` carries a `SessionStart` hook that should already have blocked this session before this file was ever read. If you're reading this anyway, hooks were bypassed, disabled, or failed — halt regardless; this rule does not depend on the hook to hold.

---

> **Do not commit, push, or rewrite git history.** Stage edits (`git add`), show the diff, and stop — the human reviews and commits.

> **Use US English spelling** in code, identifiers, comments, docs, and commit/PR copy.

## 1. What This Repository Is

Ratatoskr is **the squirrel** — `Norse.NServiceBus`: NServiceBus endpoint configuration, saga infrastructure, message conventions, and transport wiring. It is the NServiceBus-specific implementation layer carved from Midgard for the same reason Urdarbrunnr was: NServiceBus has strong opinions (sagas, message conventions, endpoint configuration, licensing) that should not seep into `Norse.Infrastructure`, it has its own versioning and licensing lifecycle independent of the core abstractions, and not every Midgardian implementation will use it — some may use MassTransit, Rebus, Azure Service Bus SDK directly, or something else entirely.

Asgard (`Norse.Abstractions`) declares the messaging surface — `IPublishEvent<T>`, `ISendCommand<T>`, `IHandleMessage<T>`, and the like — without caring how the squirrel carries them. Ratatoskr is the carrier; the Æsir never need to know it exists.

In the dependency chain: Ratatoskr sits above Asgard and Svartalfheim (it depends on their contracts and primitives), alongside Midgard (neither depends on the other), and below Yggdrasil (the hosting chassis wires it in).

This repo is currently a bare shell (LICENSE + README only) — no specs have converged here yet. Before writing any code: brainstorm → spec → plan, recorded in `../Glitnir/docs/Ratatoskr/`, per the org's spec-first discipline. Do not scaffold a project structure ahead of a converged spec. When that plan is written, its REQUIRED SUB-SKILL line names `superpowers:subagent-driven-development` as the default (not a recommendation among equals — `executing-plans` is the narrow fallback for separate-session review checkpoints) paired with `superpowers:test-driven-development` — implementation here is subagent-orchestrated and test-driven, never one without the other (`../Glitnir/CLAUDE.md` §2.8).

See `../Bifrost/CLAUDE.md` (§2 The Naming Model) and `../Glitnir/CLAUDE.md` (§3 Bounded Context Map, §4 Messaging) for the full realm table, the messaging decision (NServiceBus 10.2, `ReceiveOnly`, source-generated handler registration), and how Ratatoskr fits the rest of the cosmos.
