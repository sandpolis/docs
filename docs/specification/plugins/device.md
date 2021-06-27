# Device Plugin
The device plugin extends management functionality out to agent-less devices.

## Subagents
Subagents are devices that do not have a Sandpolis agent software installed, but are
instead managed via a third-party protocol such as SSH, HTTP, or SNMP from an instance
called the _gateway_. The gateway instance for a subagent may be an independent
agent or a server.

### Communicators
A subagent communicates to its gateway instance over one of the following well-known
protocols. Since subagents must accept incoming connections, the gateway instance
usually must reside on the same network segment.

#### SSH
| Property   | Description |
|------------|-------------|
| `ssh.username` | The SSH username |

#### HTTP
#### SNMP
| Property   | Description |
|------------|-------------|
| `snmp.version` | The SNMP version |
