# Architecture

## Runtime

P2PDiag targets .NET 10 and runs as a console executable that can be packaged and installed as a dotnet tool.

The application starts through Program.cs, which creates and starts the .NET Generic Host.

## Single-project DDD structure

The project source root is intentionally constrained to four architectural folders plus Program.cs:

    Program.cs
    Application/
    Domain/
    Infrastructure/
    Presentation/

Each architectural layer is organized by feature aggregate.

### Domain

Contains concepts that describe diagnostic behavior independently of operating-system APIs.

Examples include diagnostic status, evidence, endpoints, protocol concepts, test results and session concepts.

Domain must not depend on Infrastructure or Presentation.

### Application

Contains use cases and application contracts.

Examples include diagnostic commands, queries, handlers, orchestration and DTOs.

Application depends on domain abstractions and must not directly bind to concrete sockets, ADB processes, firewall APIs or terminal libraries.

### Infrastructure

Contains implementations for external concerns.

Examples include:

- System.Net.NetworkInformation and System.Net.Sockets integrations.
- Windows networking and firewall inspection.
- ADB process execution.
- pktmon/netsh trace integration.
- Optional Wireshark/tshark integration.
- File and report persistence.

Platform-specific behavior belongs here.

### Presentation

Contains the interactive CLI.

Examples include:

- commands;
- menus;
- forms;
- selectors;
- tables and panels;
- progress rendering;
- localized resource access.

Presentation calls application contracts rather than infrastructure implementations.

## Dependency injection

The Generic Host owns service registration and lifecycle.

Long-running operations are represented as asynchronous tasks. A command awaits the task and propagates CancellationToken rather than maintaining a manual polling loop.

## Feature aggregates

A feature aggregate may have corresponding code in each layer while retaining a common feature-oriented name.

For example:

    Application/Diagnostics/
    Domain/Diagnostics/
    Infrastructure/Diagnostics/
    Presentation/Diagnostics/

The same pattern applies to network, discovery, monitoring, Android, reporting and session features.

## UI architecture

The console UI is a presentation concern. It must support interactive menus/forms, keyboard navigation, selectable options, structured output, ANSI rendering and concurrent dynamic progress.

Dynamic rendering must avoid allowing monitor implementations to write directly to the terminal in an uncontrolled way. A coordinated presentation service should own terminal rendering.

## Packaging

The executable is intended to be packaged as a dotnet tool. Tool packaging configuration belongs to the project file and must not introduce another source-layer directory.
