## 3 Client
Client installations are entirely contained in a single directory called the base directory. This base directory may not coincide with the base directory of an agent or server installation.

###### 3.1 Filesystem Structure
- `/base/client.jar` The client executable.
- `/base/client.ico` An icon for the client
- `/base/db` A directory for client databases. Each server that the client connects to will have a corresponding database located here.
- `/base/lib` A directory for extracted client-libraries. For simplicity, all libraries, native and multiplatform, are located in the root of this directory.
- `/base/tmp` A secondary temporary directory.

###### 3.2 Additional Changes
The client-installer makes additional platform specific changes upon installation:

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