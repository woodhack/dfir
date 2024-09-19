# OSI model

**Layer 7 — Application:**

The application layer provides services directly to end-user applications, enabling them to transmit data over a network. It facilitates functions like file transfers, email, and web browsing, and passes data to the presentation layer.

**Layer 6 — Presentation:**

This layer ensures data from the application layer is in a standardized format for the receiving system. It handles tasks like data translation, encryption, and compression, converting the data into a usable form for the session layer.

**Layer 5 — Session:**

The session layer establishes, manages, and terminates connections between devices. It synchronizes data exchanges and ensures multiple sessions (e.g., different browser tabs) don't interfere with each other. Once a session is established, it passes data to the transport layer.

**Layer 4 — Transport:**

The transport layer ensures reliable data transfer between devices. It selects TCP (for reliable, connection-based transmission) or UDP (for faster, connectionless communication). It breaks data into smaller pieces—called segments (TCP) or datagrams (UDP)—and ensures error correction and flow control.

**Layer 3 — Network:**

This layer handles routing and forwarding of data using logical IP addresses. It determines the best path for the data to reach its destination and facilitates communication across networks (e.g., the Internet).

**Layer 2 — Data Link:**

The data link layer manages physical addressing using MAC addresses and ensures data is in the correct format for transmission. It adds the MAC address of the receiving device and checks for errors in the data. It bridges the network layer and the physical layer.

**Layer 1 — Physical:**

This layer involves the hardware components that convert binary data into electrical, optical, or radio signals for transmission. It handles the actual transmission of data over physical media like cables or wireless signals.

## Encapsulation:

As data moves down through the OSI model layers, each layer adds its own specific information to the beginning of the transmission. At the network layer, this data is called a packet. When it reaches the data link layer, it becomes a frame, and by the time it's transmitted across the network, the frame is broken into bits. When the receiving computer gets the message, it reverses the process, starting at the physical layer and moving up to the application layer, removing the added information at each step. This process is called **de-encapsulation**.

![image.png](OSI%20model%20b615caa51cce44f09b67de76739b5944/image.png)