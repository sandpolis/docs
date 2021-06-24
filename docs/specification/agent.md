# Agent Instance
At the highest level, agents are responsible for carrying out tasks for remote
users. They can connect over the network to any other type of instance. At minimum,
agents must be associated with one server.

## Agent Configuration
The agent's configuration is represented in standard Java properties format and
is named `agent.properties`. The configuration may be embedded in the agent's executable
or configured by the user at runtime.

| Property   | Description |
|------------|-------------|
| `instance.version` | The instance's version string |
| `build.platform` | The build platform's name |
| `build.timestamp` | UTC epoch timestamp |
| `server.address` | A CSV of IP addresses or domain names including port information |
| `server.timeout` | The server connection timeout in milliseconds |
| `server.strict_certs` | The agent will refuse to connect to a server that presents an invalid certificate |

## Agent Types

### Independent Agent
### Subagent
Subagents are devices that do not have an independent agent installed, but are
instead managed via a third-party protocol such as SSH, HTTP, or SNMP. The gateway
for a subagent may be an independent agent or a server.

#### Communicators
##### SSH
##### HTTP
##### SNMP

## Upgrades
There are two ways to upgrade the agent:
- automatically by sending the update command to the server,
- manually by generating a new installer and executing it on the agent  

### Manual Upgrade
A manual upgrade is triggered when an installer is executed on the agent and the
relevant base directory is already populated with an installation. If the agent
is not running, the installer will overwrite the base directory and install itself.
Any data that the agent has cached but not sent to the server will be lost!

Advantages
- This is the only way to upgrade if the agent can no longer connect to the server

Disadvantages
- Manual intervention required
- Cached data may be lost

### Automated Upgrade
If the agent is connected to a server, it can be upgraded remotely. This will cause
the server to fetch the agent configuration, generate a new installer, and transfer
it to the agent. The agent then executes the new installer and terminates.
