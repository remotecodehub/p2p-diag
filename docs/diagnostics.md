# Diagnostics

P2PDiag is designed to identify the layer where communication stops.

## Diagnostic model

A test should produce structured evidence with:

- status;
- protocol;
- source endpoint;
- destination endpoint;
- direction;
- address and port;
- timestamps;
- packet/attempt counts;
- received sequence numbers;
- latency where measurable;
- loss where measurable;
- operating-system or tool errors;
- explanatory evidence.

## Statuses

The diagnostic model supports:

- Pending
- Running
- Passed
- Failed
- Warning
- Skipped
- Stopped
- Cancelled
- Error

## Interpretation

### ICMP

ICMP success demonstrates that ICMP echo traffic can pass between endpoints.

ICMP failure does not by itself establish that TCP or UDP communication is impossible.

### TCP

A TCP success establishes that a TCP connection could be made to the tested endpoint and port under the test conditions.

A TCP failure must retain the underlying socket/error evidence.

### UDP unicast

UDP tests should use explicit sequence numbers and response/acknowledgement behavior when a bidirectional result is required.

Record packets sent, received, lost and latency where measurable.

### UDP broadcast

Broadcast must be tested separately from unicast.

A network may allow unicast UDP while suppressing broadcast traffic.

### Multicast

Multicast behavior depends on network and platform configuration and must be reported independently.

### Discovery

Application discovery is a higher layer than raw UDP.

A successful UDP broadcast test does not prove that an application discovery protocol is correctly implemented.

### Handshake

Handshake diagnostics should identify whether packets arrive and whether the application-level response is valid.

## Evidence first

Do not replace individual evidence with a single score or opaque verdict. The tool exists to help an operator understand what happened at each layer.
