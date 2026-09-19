# AGENTS.md

## Repository

This repository contains P2PDiag, a .NET 10 interactive console diagnostic tool distributed as a dotnet tool.

## Source of truth

The complete feature scope is tracked by GitHub issue #1, [FEATURE] P2P Diagnosis Tool. Implementation work is divided into the five phase task issues #2 through #6.

Before implementing a feature or changing architecture, read the relevant issue and the documentation under docs/.

## Documentation

Project documentation is located exclusively under:

- docs/

Documentation must be written in en-US.

At minimum, keep architecture, feature scope, usage, localization and diagnostic-behavior documentation synchronized with the implementation.

## Architecture rules

Use a DDD single-project architecture.

The project source root must contain only:

- Program.cs
- Application/
- Domain/
- Infrastructure/
- Presentation/

Do not add additional top-level source folders.

Inside Application, Domain, Infrastructure and Presentation, organize source code by feature aggregate.

Keep boundaries explicit:

- Domain contains domain concepts, value objects, domain rules and domain abstractions.
- Application contains use cases, commands, queries, handlers, DTOs and application abstractions.
- Infrastructure contains operating-system, networking, ADB, firewall, packet-capture, process and report integrations.
- Presentation contains CLI commands, interactive forms, menus, rendering, localization and user-facing presentation concerns.

Infrastructure details must not leak into Domain.

## Generic Host and dependency injection

The CLI must create and start a .NET Generic Host from Program.cs.

Use dependency injection for application services, infrastructure services, presentation services and long-running monitors.

A dynamic command must await its operation rather than implementing a polling loop whose sole purpose is to wait for completion.

Use CancellationToken consistently.

The host remains alive while the active operation is running and shuts down after completion or cancellation.

## Dynamic operations

All long-running operations must distinguish:

- graceful stop;
- cancellation.

Graceful stop must allow the operation to finish its shutdown path, dispose resources and report final status.

Cancellation must interrupt the operation promptly and must not be presented as a normal successful completion.

Do not leak sockets, streams, processes, timers or other disposable resources.

## CLI and UI

Use .NET 10-compatible console UI libraries to provide a fancy interactive CLI.

The CLI should support:

- menus;
- forms;
- keyboard navigation;
- selectable/clickable options where supported;
- tables and panels;
- ANSI rendering;
- progress indicators;
- concurrent dynamic monitors.

Keep presentation code independent from diagnostic implementation details.

## Localization

Every user-visible string must come from resource files.

Required resource files:

- Resources/Localization/Strings.resx
- Resources/Localization/Strings.pt-BR.resx
- Resources/Localization/Strings.en-US.resx

This includes menu labels, prompts, validation messages, errors, exception messages presented to users, statuses, logs and diagnostic summaries.

Do not hard-code user-facing text in C# presentation code.

## Diagnostics

Diagnostics must collect evidence rather than collapse the result into a single score or opaque verdict.

Preserve:

- endpoint;
- direction;
- protocol;
- address;
- port;
- timestamps;
- packet counts;
- sequence information;
- latency;
- loss;
- observed errors;
- environmental context;
- diagnostic status.

Differentiate ICMP, TCP, UDP unicast, UDP broadcast, directed broadcast, multicast, discovery and handshake behavior.

Do not infer that ICMP failure proves UDP failure.

## Safety

The diagnostic tool is primarily read-only.

Do not silently change:

- firewall rules;
- routes;
- network configuration;
- adapter configuration;
- system security settings.

External tools such as ADB, pktmon, netsh trace, Wireshark or tshark are optional integrations and must fail gracefully when unavailable.

Never embed machine-specific paths.

## .NET and C# conventions

Target .NET 10.

Prefer:

- async/await;
- CancellationToken;
- modern C# collection expressions where appropriate;
- primary constructors where they improve clarity;
- using/await using for disposable resources;
- nullable reference types;
- implicit usings;
- XML documentation for public APIs.

Avoid unnecessary abstraction and overengineering. Introduce interfaces where they protect architecture boundaries, enable platform isolation, or represent meaningful application contracts.

## Testing and repository operations

Do not create tests unless the current task explicitly requires them.

Do not create commits or push changes unless explicitly requested.

Keep each implementation phase buildable and coherent.

## Completion checklist

Before considering an implementation complete:

1. Read the relevant issue and docs.
2. Verify the DDD single-project folder constraints.
3. Verify all user-facing text is localized.
4. Verify cancellation and disposal behavior.
5. Verify platform-specific code remains in Infrastructure.
6. Build the solution.
7. Update relevant documentation under docs/.
8. Report any unsupported platform capability explicitly instead of simulating success.
