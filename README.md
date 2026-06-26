# Ratatoskr

> *The sly squirrel that races up and down Yggdrasil, carrying slander and secrets between the eagle at the crown and Níðhöggr at the roots — the original message broker.*

NServiceBus endpoint configuration, saga infrastructure, message conventions, and transport wiring for the Norse Architecture. Asgard declares the messaging surface; Ratatoskr carries it. The squirrel runs up and down Yggdrasil so the Æsir never need to know how messages travel.

## What this is

`Norse.NServiceBus.*` — the NServiceBus implementation layer, carved from Midgard for the same reason Urdarbrunnr was:

- NServiceBus has strong opinions (sagas, message conventions, endpoint configuration) that `Norse.Infrastructure` should not be coupled to.
- It has its own versioning and licensing lifecycle independent of the core abstractions.
- Not every Midgardian implementation will use it — some may use MassTransit, Rebus, Azure Service Bus SDK directly, or something else entirely.

Asgard (`Norse.Abstractions`) declares the messaging surface — `IPublishEvent<T>`, `ISendCommand<T>`, `IHandleMessage<T>`, and the like — without caring how messages travel. Ratatoskr is the carrier.

## What this is not

A replacement for the messaging contracts in Asgard. Those stay put — the Æsir declare the law; Ratatoskr just runs it.

## Status

This repo is a bare shell. No specs have converged here yet. The design process starts in [Glitnir](https://github.com/NorseArchitecture/Glitnir) — brainstorm → spec → plan → code, in that order, never reversed. The full messaging decision (NServiceBus 10.2, `ReceiveOnly` transport transaction mode, source-generated handler registration, two endpoint flavors per context) is in `Glitnir/docs/Platform/specs/2026-06-03-messaging-foundation-design.md`.
