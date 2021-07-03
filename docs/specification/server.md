# Server Instance
Every Sandpolis network must include one server instance at minimum. Servers are
responsible for coordinating interactions among instances and persisting data.

## Listening port
The Sandpolis server listens on TCP port **8768** by default, but can be configured
to listen on a different port or multiple ports concurrently.

## Geolocation Services
Sandpolis is able to get its location information from several sources. To select
a location service, the following configuration options are recognized:

| Property   | Default | Description |
|------------|---------|---|
| `server.geolocation.service` | *ip-api.com* | The name of the geolocation service to use. Valid values are found in the table below. |
| `server.geolocation.key` | *null* | The service API key |
| `server.geolocation.expiration` | *240* | The cache timeout in hours |

The following public geolocation services are supported:

| Service    | Identifier |
|------------|------------|
| <a href="https://ip-api.com" target="_blank">ip-api.com</a> | `ip-api.com` |
| <a href="https://tools.keycdn.com/geo" target="_blank">tools.keycdn.com</a> | `keycdn.com` |

## Permissions
All user accounts are subject to a set of permissions controlling what server
operations are authorized. The inital admin user has complete and irrevocable
permissions. By default, additional user accounts are created without permissions
and consequently are allowed to do almost nothing.

### Permissions list

| Permission | Description |
|------------|-------------|
| `server.generate` | Rights to use the generator |
| `server.fs.read` | Read access to the server's filesystem |
| `server.fs.write` | Write access to the server's filesystem |
| `server.users.view` | Right to view usernames and permissions of all other users |
| `server.users.create` | Right to create new users (of lesser or equal permissions) |
| `server.state.stop` | Right to stop the server |
| `server.state.shutdown` | Right to shutdown the server |
| `server.state.restart` | Right to restart the server |
| `server.net.view` | Right to open the network control panel |
| `server.net.create_listener` | Right to create a new listener on the server |
| `server.auth.create_group` | Right to create a new authentication group on the server |
| `agent.fs.read` | Read access to the agent's filesystem |
| `agent.fs.write` | Write access to the agent's filesystem |
| `agent.state.shutdown` | Right to shutdown the agent |
| `agent.state.restart` | Right to restart the agent |

## Authentication Groups
Authentication groups are sets of agents that share a common authentication scheme.
Every group has exactly one owner and zero or more client members.

### Password Authentication
### Certificate Authentication

## Generators
Sandpolis is compatible with many different platforms and therefore needs to have a flexible approach to client installation. A `Generator` is a routine which produces some installation artifact according to a supplied configuration (`GenConfig`). This installation artifact is then used to install the Sandpolis client on a remote system.

### Installation Artifacts
At minimum, installation artifacts contain configuration and settings for the client. Usually, installation artifacts will also contain the actual client code and be runnable on the remote system.

#### Installers
An installer contains the full client codebase and is runnable on the remote system. Upon execution, the installer sets up the base directory according to its configuration and executes the client. If the target directory already contains an installation, the old installation is overwritten.  In an automated upgrade scenario, this operation poses no risk to data stored in the old client's database because this data would have been already flushed to the server. A manual upgrade could destroy data cached in the client database and is therefore not recommended.

##### Advantages
- Simple
- Does not require Internet access during installation

##### Disadvantages
- File size is large
- File transfer may be inconvenient

##### Examples
- Runnable Jar files (.jar, .war, .ear)
- Windows portable executables (.exe, .msi)
- Scripts (.sh, .rb, .py, .bat, ...)

#### Downloaders
Downloaders are similar to installers except dependencies must be downloaded upon execution. This can drastically reduce the size of the resulting installation artifact. Remote dependencies must be located in a Maven repository and not downloaded from the Sandpolis server.

##### Advantages
- Smaller file size

##### Disadvantages
- Requires Internet access during installation
- File transfer may be inconvenient

##### Examples
- Runnable Jar files (.jar, .war, .ear)
- Windows portable executables (.exe, .msi)
- Scripts (.sh, .rb, .py, .bat, ...)
	
#### Tokens
A token is an artifact which only contains the client configuration and cannot be executed by itself. When provided to a generic installer, the token allows the client to be installed on the remote system.

##### Advantages
- No files are transferred

##### Disadvantages
- More user interaction is required

##### Examples
- Barcodes for use on Android, IOS, etc...

### Generators
All installation artifacts are first generated on the server using a generator and then transferred to the requesting client (or client in the case of an automated upgrade). 

##### Generator Queue
Since performing a generation is an infrequent task, the server maintains a simple queue of requests (generation configs) and fufills them serially. If the queue becomes full, incoming requests are dropped.

##### Generator Configs
A `GenConfig` specifies what type of generator should process it, any necessary options for that generator, and where to direct the resulting installation artifact. `GenConfigs` are implicitly created on the client from the graphical interface.

## 2 Server
Server installations are entirely contained in a single directory called the base directory. This base directory may not coincide with the base directory of an agent or client installation.

###### 2.1 Filesystem Structure
- `/base/server.jar` The server executable.
- `/base/server.db` The server's only database.
- `/base/lib` A directory for extracted libraries, regardless of instance prerequisites.
	- `jar` Contains platform-independent Java libraries.
	- `win` Contains Windows-specific native libraries.
	- `lin` Contains Linux-specific native libraries.
	- `osx` Contains OSX-specific native libraries.
	- `bsd` Contains BSD-specific native libraries.
	- `sol` Contains Solaris-specific native libraries.
- `/base/tmp` A secondary temporary directory.

###### 2.2 Additional Changes
The server-installer makes additional platform specific changes upon installation:

###### 2.2.1 Windows
TODO: Research services
###### 2.2.2 Linux
###### 2.2.2.1 Systemd
Management via systemd is supported.

###### 2.2.3 Mac OS
