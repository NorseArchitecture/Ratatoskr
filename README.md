# Ratatoskr

> *The sly squirrel that races up and down Yggdrasil, carrying slander and secrets between the eagle at the crown and Níðhöggr at the roots — the original message broker.*

![Ratatoskr — the sly squirrel who races the length of Yggdrasil, carrying messages between the eagle at the crown and Níðhöggr gnawing at the roots](https://github.com/user-attachments/assets/e8657b0f-5176-43ec-bb87-a11d2b80cf43 "Ratatoskr — the original message broker")

*Image credit: [@norsemythologyclips](https://www.instagram.com/norsemythologyclips/) — go follow them.*

NServiceBus endpoint configuration, saga infrastructure, message conventions, and transport wiring for the Norse Architecture. Asgard declares the messaging surface; Ratatoskr carries it. The squirrel runs up and down Yggdrasil so the Æsir never need to know how messages travel.

## What this is

`Norse.Messaging.*` — the platform's messaging realm, scoped to all message-broker and transport activity, not just NServiceBus:

- `Norse.Messaging.NServiceBus` is today's live vendor family — endpoint configuration, saga infrastructure, message conventions, and transport wiring — carved from Midgard for the same reason Urðarbrunnr was.
- NServiceBus has strong opinions (sagas, message conventions, endpoint configuration) that `Norse.Infrastructure` should not be coupled to, and it has its own versioning and licensing lifecycle independent of the core abstractions.
- A different broker or messaging library lands here as its own sibling under `Norse.Messaging.*` (`Norse.Messaging.MassTransit`, `Norse.Messaging.Rebus`, …) the same way Heimdall took on FluentUI — not every Midgardian implementation will use NServiceBus.

Asgard (`Norse.Abstractions`) declares the messaging surface — `IPublishEvent<T>`, `ISendCommand<T>`, `IHandleMessage<T>`, and the like — without caring how messages travel. Ratatoskr is the carrier.

## What this is not

A replacement for the messaging contracts in Asgard. Those stay put — the Æsir declare the law; Ratatoskr just runs it.

## Status

This repo is a bare shell. No specs have converged here yet. The design process starts in [Glitnir](https://github.com/NorseArchitecture/Glitnir) — brainstorm → spec → plan → code, in that order, never reversed. The full messaging decision (NServiceBus 10.2, `ReceiveOnly` transport transaction mode, source-generated handler registration, two endpoint flavors per context) is in `Glitnir/docs/Platform/specs/2026-06-03-messaging-foundation-design.md`.

## Soundtrack: Ratatöskr
[![Soundtrack: Ratatöskr](https://img.youtube.com/vi/GvnP7TThMyE/maxresdefault.jpg)](https://www.youtube.com/watch?v=GvnP7TThMyE)
