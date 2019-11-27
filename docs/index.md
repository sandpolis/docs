# Sandpolis Official Documentation

This documentation explains how to **install**, **configure**, and **maintain** Sandpolis. It's still a work in progress; feel free to <a href="https://github.com/Subterranean-Security/docs/issues" target="_blank">drop us an issue</a>.

## The Basics
You may already be familiar with other remote-control utilities that allow you to monitor/manage many different computers from a single GUI. To use these tools, you typically install a *stub* or *agent* on the computers you wish to monitor and direct that stub to connect back to the main application running on your computer. While relatively simple, there are some disadvantages to this approach:

- Your computer may not always be online to accept connections
- Your computer may not have a stable IP address
- This architecture does not scale as the number of client computers increases

To address these problems, Sandpolis uses a client-server-viewer (CSV) architecture. Rather than connecting clients directly to an application on your computer, a central server mediates all interactions between you and your client systems.

With CSV, clients and viewers can come and go without affecting the rest of the network. This means that:

- background or scheduled tasks can continue after a user logs out
- users are not restricted to a particular user interface
- messages between clients and viewers are routed through the server first. (For high-volume messages like remote desktop streams or file transfer streams, the server automatically coordinates a direct connection between the two nodes if possible).
- users don't have to adjust their firewalls or port-forwarding rules