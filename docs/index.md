# Sandpolis Official Documentation

This documentation explains how to **install**, **configure**, and **maintain** Sandpolis. It's still a work in progress; feel free to <a href="https://github.com/Subterranean-Security/docs/issues" target="_blank">drop us an issue</a>.

## The Basics
You may be familiar with other remote control tools which allow you to keep track of many different computers from a single application. To use these tools, you typically install a "stub" application on the computer you wish to monitor and direct that stub to connect back to the main application running on your computer. While relatively simple, there are some disadvantages to this approach:

robust, permanent solution.

- Your computer may not always be online to accept connections
- Your computer may not have a stable IP address
- This architecture does not scale as the number of computers increases

To address these problems, Sandpolis uses a client-server-viewer (CSV) architecture. Rather than connecting computers directly to an application on your computer, a mediating server allows clients and viewers to interact.

In this architecture, viewers can come and go without affecting the rest of the network. This means that background or scheduled tasks can continue after a viewer logs out. This also means that users are not locked-in to a particular user interface.  This means that most messages between clients and viewers are routed through the server first. (The only exception is for high-volume messages like remote desktop streams or file transfer streams. In this case, the server automatically coordinates a direct connection between the two nodes if possible).