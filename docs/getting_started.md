# Getting Started

## Installing the Server
There are several different ways to install the server. The universal installer will work on just about every system, but a distribution package may be a more convenient option.

### With the universal installer GUI
- <a href="https://sandpolis.com/download" target="_blank">Download</a> the universal installer for your operating system. We recommend running the server on a Linux machine because it's convenient to manage the server process with `systemd`, but it works on Windows and macOS as well.
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
tar xf sandpolis.tar.gz
cd sandpolis
makepkg -sif
```

Start and optionally enable the server's `systemd` unit:
``` sh
sudo systemctl start sandpolisd.service
sudo systemctl enable sandpolisd.service
```

### With Docker
The server can also be run as a Docker container with the following command:
``` sh
sudo docker run --restart unless-stopped sandpolis/sandpolis-server:latest
```

If your container isn't starting on boot, make sure the Docker daemon is configured to start automatically:
```
sudo systemctl enable docker
```

## Installing the Viewer
There are several official viewer applications that can be used to connect to a server. Not all of them have the same capabilities, so choose the most convenient variant that meets your needs.

### Sandpolis iOS application
The Sandpolis iOS application can be installed from the App Store and supports iPhone and iPad devices running iOS 13.0 or greater. **Warning:** the iOS app uses Google's Firebase platform for user authentication. If you avoid Google products, use the desktop application instead.

#### Create an account
Your account allows you to save multiple servers for easy access and enables several features not possible with other viewer applications.

### Sandpolis Android application
Coming soon...

### Sandpolis Desktop Viewer
Coming soon...

## Installing the Client

### With the universal installer GUI
If you have the Sandpolis mobile app, you can scan the QR code in the installer to automatically associate the client with the correct server.

### Generate a client installer
A customized installer can be generated from the desktop viewer application that can then be used to install the client on any machine.
