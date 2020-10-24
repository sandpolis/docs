# Sandpolis Official Documentation

This site explains how to **install**, **configure**, and **maintain** Sandpolis. It also contains a high-level programming reference useful to developers. It's still a work in progress; feel free to <a href="https://github.com/Subterranean-Security/docs/issues" target="_blank">open an issue</a>.

## The Basics
You may already be familiar with other remote-control applications that allow you to monitor/manage many different computers from a single pane of glass. To use these tools, you might install an *agent* on the computers you wish to manage and direct the agent to connect back to the main application running on your computer. While relatively simple, there are some major disadvantages to this approach:

- Your computer may not always be online to accept connections
- Your computer may not have a stable IP address
- This architecture does not scale as the number of agents increases

To address these problems, Sandpolis uses a client-server-agent (CSA) architecture. Rather than connecting agents directly to an application on your computer, a central server mediates most interactions between you and your systems.

### Client <-> Server <-> Agent
With CSA, clients and agents can come and go without affecting the rest of the network. This means that:

- background or scheduled tasks can continue after a user logs out;
- users are not restricted to a particular user interface;
- users don't have to adjust their firewalls or port-forwarding rules.

CSA also comes with a few drawbacks:

###### The server is just another application to maintain
Although it can be easy to deploy with Docker, the server still requires some effort to maintain. In addition to the initial setup, it's important to periodically update the server and harden its security.

###### The server is a high value attack target
While the server is designed to be as resilient and secure as possible, it can't be perfect. If an attacker is able to compromise the server (or a user account with sufficiently high privileges), they effectively have full control over all systems connected to it.

To help mitigate this risk, all Sandpolis user accounts are **required** to use two-factor authentication and password rotation.

###### Messages between clients and agents are usually routed through the server first
Often times the route between a user and their systems will be faster than the client/server route plus the server/agent route. This is especially true if a user is on the same network as their systems. To mitigate this issue, the server can automatically coordinate a direct connection between any two nodes for high-volume messages like remote desktop session or file transfers.
