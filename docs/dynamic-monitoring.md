# Dynamic Monitoring

Dynamic monitoring is intended for long-running diagnosis.

## Monitor lifecycle

A monitor has a task representing its active operation and accepts CancellationToken.

The caller awaits that task.

Do not implement a loop in the command whose only purpose is repeatedly checking whether the monitor task has finished.

## Graceful stop

A graceful stop requests normal shutdown.

The monitor should:

1. stop accepting new work;
2. finish the defined shutdown path;
3. dispose resources;
4. produce its final status;
5. return control to the host.

## Cancellation

Cancellation requests interruption.

The cancellation token must propagate to asynchronous operations where supported.

Cancellation should not be presented as successful completion.

## Concurrent monitors

Multiple monitors may run simultaneously.

Monitor implementations should publish structured events/results to a coordinated presentation layer rather than writing arbitrary terminal escape sequences themselves.

## Terminal rendering

The presentation layer owns terminal rendering.

The intended UI keeps normal diagnostic/log output above persistent progress/status lines near the bottom of the terminal.

The renderer must support multiple active progress instances and update them without corrupting ordinary output.

## Monitoring targets

Planned monitors include:

- UDP traffic;
- TCP/UDP port state;
- network interfaces;
- endpoint statistics;
- application logs;
- discovery packets/protocol;
- packet capture sessions.
