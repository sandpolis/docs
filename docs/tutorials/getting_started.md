# Getting Started
If you just want to demo Sandpolis, try connecting to the official demo server
(`demo.sandpolis.com`) with the desktop client. You'll be able to look around at
simulated systems, but won't be able to add your own agents.

Otherwise, if you want to run your own Sandpolis network, the first thing you need
is a private server instance.

## Deploying the Server
There are several different ways to install the server. The universal installer
is a user-friendly method that will work on just about every system, but a specialized
distribution package or Docker container is the most convenient option for keeping
the server updated.

### With Docker
The server can be run as a Docker container with the following command:
``` sh
docker run \
	--name sandpolis-server \
	--restart unless-stopped \
	-p 8678:8678 \
	sandpolis/server:latest
```

!!! note
	If your instance isn't starting on boot, ensure the Docker daemon is configured to start automatically:
	``` sh
	sudo systemctl enable docker
	```

The default admin password will be printed in the container's log which can be
viewed with the following command:

```sh
docker logs sandpolis-server
```

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

### With the universal installer GUI
- <a href="https://sandpolis.com/download" target="_blank">Download</a> the universal installer for your operating system.

!!! note
	Although the server runs on any platform, it's extremely convenient to manage the server process with `systemctl` on Linux.

- Select **server** from the available components and choose "install".


## Installing a Client
There are several official client applications that can be used to connect to a
server. Not all of them have the same capabilities, so choose the variant that
meets your needs best.

### Sandpolis Desktop Client

### Sandpolis for iOS
The [Sandpolis iOS application](https://apps.apple.com/us/app/sandpolis/id1478068506) can be installed from the App Store and supports
iPhone and iPad devices running iOS 13.0 or greater.

## Installing the Agent
Once you're logged into a server, the last thing to do is install an agent. As
with clients, there are several choices that are suitable in different environments.

### Standard Agent
### Native Agent
### Minimal Agent
