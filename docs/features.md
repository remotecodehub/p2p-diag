# Features

## Environment diagnostics

Collect operating system, host, runtime and relevant environment information.

## Network diagnostics

Inspect interfaces, addresses, subnet/prefix information, routing, ARP/neighbours, ICMP and transport reachability.

## TCP diagnostics

Provide control-plane connectivity tests, listening-port checks and process/port inspection.

## UDP diagnostics

Provide listeners, senders, unicast tests and bidirectional probes with sequence numbers, packet counts, loss and latency.

## Broadcast and multicast

Test broadcast and directed broadcast behavior independently from unicast. Multicast diagnostics are available where the platform and network support them.

A successful unicast test must not be interpreted as proof that broadcast discovery will work.

## Android and ADB

Discover connected Android devices through ADB and collect network information where available.

Support directional Android/Windows UDP tests where the endpoint capabilities permit them.

ADB is optional; its absence must be represented as a localized diagnostic condition.

## Dynamic monitoring

Monitor network traffic, ports, interfaces, endpoints, logs and discovery traffic continuously.

Multiple monitors can run concurrently.

## Packet capture

Integrate optional operating-system capture tools such as pktmon and netsh trace. Wireshark/tshark may be supported when installed.

Basic diagnostics must not require these tools.

## Sessions and reports

Capture structured evidence in diagnostic sessions and export JSON/text reports.

Reports can be compared between endpoints to identify asymmetry and transport-layer differences.

## End-to-end diagnostics

Compose lower-level tests into a connectivity matrix covering:

1. local environment;
2. interface/address;
3. route;
4. ICMP;
5. TCP;
6. UDP unicast;
7. UDP broadcast;
8. directed broadcast;
9. multicast;
10. discovery;
11. handshake.

Each step retains its own evidence and status.
