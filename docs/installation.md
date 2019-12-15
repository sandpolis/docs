## 1 Client
Client installations are entirely contained in a single directory called the base directory. This base directory may not coincide with the base directory of a server or viewer installation.

###### 1.1 Filesystem Structure
- `/base/client.jar` The client executable, named according to the configuration.
- `/base/client.db` The client's only database, named according to the executable.
- `/base/lib` A directory for extracted client-libraries. For simplicity, all libraries, native and multiplatform, are located in the root of this directory.
- `/base/tmp` A secondary temporary directory.

###### 1.2 Additional Changes
The client-installer makes additional platform specific changes upon installation:

###### 1.2.1 Windows
###### 1.2.2 Linux
###### 1.2.3 Mac OS

###### 1.3 Upgrading
There are two ways to upgrade the client:
- automatically by sending the update command to the server,
- manually by generating a new installer and executing it on the client  

###### 1.3.1 Manual Upgrade
A manual upgrade is triggered when an installer is executed on the client and the relevant base directory is already populated with an installation. If the client is not running, the installer will overwrite the base directory and install itself. Any data that the client has cached but not sent to the server will be lost!

Advantages
- This is the only way to upgrade if the client can no longer connect to the server

Disadvantages
- Manual intervention required
- Cached data may be lost

###### 1.3.2 Automated Upgrade
If the client is connected to a server, simply issue the update/upgrade command from a viewer instance. This will cause the server to fetch the client configuration, generate a new installer, and transfer it to the client. The client then executes the new installer and terminates.

## 2 Server
Server installations are entirely contained in a single directory called the base directory. This base directory may not coincide with the base directory of a client or viewer installation.

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

## 3 Viewer
Viewer installations are entirely contained in a single directory called the base directory. This base directory may not coincide with the base directory of a client or server installation.

###### 3.1 Filesystem Structure
- `/base/viewer.jar` The viewer executable.
- `/base/viewer.ico` An icon for the viewer
- `/base/db` A directory for viewer databases. Each server that the viewer connects to will have a corresponding database located here.
- `/base/lib` A directory for extracted viewer-libraries. For simplicity, all libraries, native and multiplatform, are located in the root of this directory.
- `/base/tmp` A secondary temporary directory.

###### 3.2 Additional Changes
The viewer-installer makes additional platform specific changes upon installation:

###### 3.2.1 Windows
###### 3.2.2 Linux
###### 3.2.3 Mac OS

## Installer Flags

| Property | Default | Description |
|----------|---------|-------------|
| path     | user.home + /.sandpolis | The base installation path |
| components | null  | The components to install |
| version  | latest  | The version to install |
| ext.linux.desktop | /usr/share/applications; user.home + /.local/share/applications | The Linux desktop entry location |
| ext.windows.start | C:/ProgramData/Microsoft/Windows/Start Menu/Programs; user.home + /AppData/Microsoft/Windows/Start Menu/Programs | The Windows start menu location |
| ext.windows.desktop | user.home + /Desktop | The Windows desktop shortcut location |