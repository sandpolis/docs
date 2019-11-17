# Getting Started

This guide will explain the process of installing the Sandpolis.

## Installing the Server
If you already have a server or are using a cloud server, you can skip this step.

### With the universal installer GUI
- [Download](https://sandpolis.com/download) the server installer for your operating system. We recommend running the server on a Linux machine because it's convenient to manage the server process with `systemd`, but it works on Windows and macOS as well.
- Select "server" from the available components and press "Install".

### With a distribution package
#### Pacman (Arch Linux)
Download either the stable or development package:
``` sh
# Stable
wget https://aur.archlinux.org/cgit/aur.git/snapshot/sandpolis.tar.gz

# Development
wget https://aur.archlinux.org/cgit/aur.git/snapshot/sandpolis-git.tar.gz
```

Install with `makepkg`:
``` sh
cd sandpolis
makepkg -sif
```

Start and optionally enable the server's `systemd` unit:
``` sh
sudo systemctl start sandpolisd.service
sudo systemctl enable sandpolisd.service
```

## Installing the Client

### With the universal installer GUI
If you have the Sandpolis mobile app, you can scan the QR code in the installer to automatically associate the client with the correct server.

### Generate a client installer
A customized installer can be generated from the desktop viewer application that can then be used to install the client on any machine.

## Installing the Viewer
There are several official viewer applications that can be used to connect to a server.

### Sandpolis iOS application
The Sandpolis iOS application can be installed from the App Store.

#### Create an account
Your Sandpolis account allows you to save multiple servers.

### Sandpolis Android application
Coming soon...

### Sandpolis Desktop Viewer
Coming soon...