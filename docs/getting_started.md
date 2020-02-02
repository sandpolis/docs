## Installing the Server
There are several different ways to install the server. The universal installer will work on just about every system, but a specialized distribution package may be a more convenient option if your system supports it.

### With the universal installer GUI

- <a href="https://sandpolis.com/download" target="_blank">Download</a> the universal installer for your operating system.

!!! note
	Although the server runs on any platform, it's extremely convenient to manage the server process with `systemctl` on Linux.

- Select **server** from the available components and choose "install".

### With a distribution package
#### Pacman (Arch Linux)
Download either the stable or development package from the AUR:
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

Start and optionally enable the server's `systemd` service unit:
``` sh
# Start the server process
sudo systemctl start sandpolisd.service

# Configure the server to start on boot
sudo systemctl enable sandpolisd.service
```

### With Docker
The server can also be run as a Docker container with the following command:
``` sh
sudo docker run --restart unless-stopped sandpolis/sandpolis-server:latest
```

If your container isn't starting on boot, ensure the Docker daemon is configured to start automatically:
``` sh
sudo systemctl enable docker
```

## Installing the Viewer
There are several official viewer applications that can be used to connect to a server. Not all of them have the same capabilities, so choose the variant that meets your needs.

### Sandpolis for iOS
The Sandpolis iOS application can be installed from the App Store and supports iPhone and iPad devices running iOS 13.0 or greater.

!!! warning
	The iOS app optionally uses Google's [Firebase platform](https://firebase.google.com) for user authentication. If you avoid Google products, just login to your servers manually without creating an account.

#### Create an account
Your account allows you to save multiple servers for easy access and enables several features not possible with other viewer applications.

### Sandpolis Android application
Coming soon...

### Sandpolis Desktop Viewer
Coming soon...

## Installing the Client

### With the universal installer GUI
If you have the mobile application, you can scan the QR code in the universal installer to automatically associate the client with the correct server.

### Generate a client installer
The desktop viewer can generate customized installers that can be used to install the client on any machine.
