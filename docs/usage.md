# Usage

## Local development

Restore and build the solution with the .NET 10 SDK selected by global.json.

The repository contains a local dotnet-tools manifest. After the project is packaged, the tool can be installed locally through the standard dotnet tool workflow.

## Interactive CLI

The primary interface is interactive.

Users should be able to:

- select a diagnostic category;
- select or enter a network interface;
- enter an endpoint and port;
- choose a protocol test;
- start listeners or send probes;
- start one or more dynamic monitors;
- stop an operation gracefully;
- cancel an operation;
- export a diagnostic session.

Forms must validate input before starting network operations.

## Endpoint testing

For two-endpoint testing, start the appropriate listener on one endpoint and run the corresponding sender/probe on the other.

Always record the direction of the test.

For example:

    Windows -> Android
    Android -> Windows

Do not treat an asymmetric result as a generic connectivity result.

## Cancellation

Long-running operations accept CancellationToken.

A graceful stop is a normal lifecycle action and should produce a final status.

Cancellation is an interruption and must not be reported as normal completion.

## Optional external tools

ADB, pktmon, netsh trace, Wireshark and tshark are optional. The CLI should detect availability and present clear localized diagnostics when an integration cannot be used.

## Tool packaging

The project is intended to be published as a dotnet tool. Installation and package metadata must be kept synchronized with the project file and documented here when finalized.
