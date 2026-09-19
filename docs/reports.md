# Sessions and Reports

A diagnostic session groups the tests performed for one investigation.

## Session data

A session should preserve:

- session identifier;
- start/end timestamps;
- local endpoint information;
- remote endpoint information;
- selected interface;
- test configuration;
- individual diagnostic results;
- raw or summarized evidence;
- external tool availability;
- cancellation or stop state.

## Export

The tool supports JSON and text report formats.

JSON is intended for machine-readable evidence and later comparison.

Text is intended for operator review and sharing.

## Endpoint comparison

Two endpoint reports can be compared to expose differences such as:

- interface/address selection;
- route differences;
- firewall state;
- UDP unicast asymmetry;
- broadcast behavior;
- packet loss;
- discovery observations.

Comparison must preserve the underlying evidence rather than reducing the result to a winner or score.
