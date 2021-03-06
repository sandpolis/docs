# Server Instance
Every Sandpolis network must include one server instance at minimum. Servers are
responsible for coordinating interactions among instances and persisting data.

## Listening port
The Sandpolis server listens on TCP port **8768** by default, but can be configured
to listen on a different port or multiple ports concurrently.

## Geolocation Services
Sandpolis is able to get its location information from several sources. To select
a location service, the following configuration options are recognized:

| Property                        | Default      | Description                                                                            |
|---------------------------------|--------------|----------------------------------------------------------------------------------------|
| `server.geolocation.service`    | *ip-api.com* | The name of the geolocation service to use. Valid values are found in the table below. |
| `server.geolocation.key`        | *null*       | The service API key                                                                    |
| `server.geolocation.expiration` | *240*        | The cache timeout in hours                                                             |

The following public geolocation services are supported:

| Service    | Identifier |
|------------|------------|
| <a href="https://ip-api.com" target="_blank">ip-api.com</a> | `ip-api.com` |
| <a href="https://tools.keycdn.com/geo" target="_blank">tools.keycdn.com</a> | `keycdn.com` |

## Database

| Property                        | Default      | Description                                                                            |
|---------------------------------|--------------|----------------------------------------------------------------------------------------|
| `s7s.storage.provider`          | *ephemeral*  | The database storage provider                                                          |
| `s7s.storage.mongodb.host`      |              | The address of the mongodb host                                                        |
| `s7s.storage.mongodb.username`  |              | The mongodb user's username                                                            |
| `s7s.storage.mongodb.password`  |              | The mongodb user's password                                                            |

## First Start
If the server starts with ephemeral storage or an empty database, the server enters
"first start" mode. This mode has the following implications:

### Default admin password
The admin password will be randomized and printed in the server log. All clients
are required to force users to change the admin password and setup multi-factor
authentication before proceeding after the first login.

## Connection Blocking
The server will refuse connections from IP addresses on a configurable blocklist
or those that trigger the global rate-limiting policy.

IP address on a configurable whitelist are exempt from rate-limiting.

## Permissions
All user accounts are subject to a set of permissions controlling what server
operations are authorized. The inital admin user has complete and irrevocable
permissions. By default, additional user accounts are created without permissions
and consequently are allowed to do almost nothing.

### Permissions list

| Permission                   | Description                                                                                              |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| `server.generate`            | Rights to use the generator                                                                              |
| `server.users.list`          | Right to view usernames and permissions of all other users                                               |
| `server.users.create`        | Right to create new users (of lesser or equal permissions)                                               |
| `server.net.view`            | Right to open the network control panel                                                                  |
| `server.listener.create`     | Right to create a new listener on the server                                                             |
| `server.listener.list`       | Right to view all listeners on the server                                                                |
| `server.group.create`        | Right to create a new authentication group on the server                                                 |
| `server.group.list`          | Right to view all authentication groups on the server                                                    |
| `agent.system.power`         | Right to shutdown, reboot, etc the agent                                                                 |

## Agent Groups
Agent groups are sets of agents that share one or more authentication schemes.
Every group has exactly one owner and zero or more (user) members.

### Password Authentication Scheme
After establishing a connection, agents may present an unsalted SHA512 hash of
a password entered by the user to the server. The server compares the password
to each agent group until it finds a match. If a match is found, the agent is
becomes authenticated to the matching agent group. Otherwise, the connection is
closed if more than 5 attempts were made on that connection.

Since a user must type the password manually, the server will attempt to configure
the certificate authentication scheme for all subsequent connections.

### Token Authentication Scheme
The agent may provide an 8 character alphanumeric time-based token periodically
generated by the server from an agent group's secret key. Since a user must type
the token in manually, the server will attempt to configure the certificate authentication
scheme for all subsequent connections.

### Certificate Authentication Scheme
The agent may provide an X509 "client" certificate signed by an agent group's secret
key during the initial connection attempt. If the agent certificate was found to
be valid, the connection is automatically authenticated without any additional
message exchanges.

#### Agent Certificate Expiration
The default lifetime for an agent certificate is six months. The following section
implies an agent must connect to a server at least once every 1.5 months otherwise
it loses its ability to authenticate.

#### Agent Certificate Renewal
Once 75% of the lifetime of an agent certificate elapses, the server attempts to
issue a new certificate and installs it on the agent.

## Agent Generators
A `Generator` is a routine which produces some installation artifact according
to the parameters set out in an authentication group. The installation artifact
can then be used to install an agent on a remote system.

- Standard agent (com.sandpolis.agent.vanilla)
- Native agent (com.sandpolis.agent.micro)
- Minimal agent (com.sandpolis.agent.nano)

### Installers
On execution, installers set up the agent base directory according to its configuration
and executes the agent. If the target directory already contains an installation,
the old installation is entirely overwritten.

#### Installer Configuration
Installers have an embedded configuration file called `install.properties` that
describes how the installation process should proceed.

| Property                     | Description                                                                                              |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| `agent.type`                 | The agent type (vanilla, micro, or nano)                                                                 |
| `agent.path`                 | The filesystem path                                                                                      |
| `agent.auth.scheme`          | The name of the authentication scheme to use (password or certificate)                                   |
| `install.recover`            | Whether the installation should attempt to continue if errors occur                                      |

### Packager
A packager is responsible for creating an agent installer binary according to the
parameters set out in an authentication group.

### Deployer
A deployer is responsible for deploying generated agent installers to remote
systems automatically.

#### SSH Deployer
The SSH deployer first determines the remote system type and invokes an appropriate
packager to generate an installer. The installer is then transferred to the remote
host and executed.
