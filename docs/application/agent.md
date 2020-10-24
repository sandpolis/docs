## 1 Agent
Agent installations are entirely contained in a single directory called the base directory. This base directory may not coincide with the base directory of a server or client installation.

###### 1.1 Filesystem Structure
- `/base/agent.jar` The agent executable, named according to the configuration.
- `/base/agent.db` The agent's only database, named according to the executable.
- `/base/lib` A directory for extracted agent-libraries. For simplicity, all libraries, native and multiplatform, are located in the root of this directory.
- `/base/tmp` A secondary temporary directory.

###### 1.2 Additional Changes
The agent-installer makes additional platform specific changes upon installation:

###### 1.2.1 Windows
###### 1.2.2 Linux
###### 1.2.3 Mac OS

###### 1.3 Upgrading
There are two ways to upgrade the agent:
- automatically by sending the update command to the server,
- manually by generating a new installer and executing it on the agent  

###### 1.3.1 Manual Upgrade
A manual upgrade is triggered when an installer is executed on the agent and the relevant base directory is already populated with an installation. If the agent is not running, the installer will overwrite the base directory and install itself. Any data that the agent has cached but not sent to the server will be lost!

Advantages
- This is the only way to upgrade if the agent can no longer connect to the server

Disadvantages
- Manual intervention required
- Cached data may be lost

###### 1.3.2 Automated Upgrade
If the agent is connected to a server, simply issue the update/upgrade command from a viewer instance. This will cause the server to fetch the agent configuration, generate a new installer, and transfer it to the agent. The agent then executes the new installer and terminates.
