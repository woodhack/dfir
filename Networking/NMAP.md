# NMAP

Nmap (Network Mapper) is a powerful open-source tool for network discovery and security auditing. It helps identify hosts, services, open ports, and vulnerabilities by sending packets to targets and analyzing their responses.

**Nmap Switches**

Nmap offers various command-line switches to customize scans. Key switches include:

- `-sS` for SYN scans (stealthy)
- `sT` for TCP connect scans (full handshake)
- `sU` for UDP scans
- `-p` to specify port ranges
- `-p-` scan all ports
- `-O` for OS detection
- `Pn` to skip host discovery and scan all hosts directly
- `-sV` Attempt to discover versions of services running

These switches allow you to adjust how Nmap interacts with the network.

**Scan Types Overview**

Nmap supports different scan types for various purposes, such as probing protocols, discovering open services, or identifying vulnerabilities. Each scan type serves a specific role in network and security assessments.

**TCP Connect Scans (Full TCP)**

TCP Connect (`-sT`) is a complete handshake scan where Nmap establishes full TCP connections with target ports. It’s reliable but generates more logs since it fully opens and closes connections, making it easy to detect.

**SYN Scans (Half-Open)**

SYN scans (`-sS`) are faster and stealthier. They send SYN packets and wait for SYN-ACKs, identifying open ports without completing the TCP handshake. This makes SYN scans harder to detect by firewalls and intrusion detection systems (IDS).

**UDP Scans**

UDP scans (`-sU`) identify open UDP ports by sending UDP packets and waiting for responses. Since many services don’t reply to probes, open ports may require multiple retries, making UDP scanning slower than TCP scans. This method is essential for services like DNS and SNMP.

**NULL, FIN, and Xmas Scans**

These scans send unusual TCP flag combinations to potentially bypass firewalls:

- **NULL** (`sN`) sends packets with no flags set.
- **FIN** (`sF`) sends a FIN flag to indicate the end of a connection.
- **Xmas** (`sX`) sets multiple flags to create an odd packet.

Closed ports usually respond with RST, while open ones don’t reply, helping to identify unfiltered ports.

**ICMP Network Scanning**

Nmap sends an ICMP packet to each possible IP address for the specified network. When it receives a response, it marks the IP address that responded as being alive. To perform a ping sweep, we use the **`-sn`** switch in conjunction with IP ranges which can be specified with either a hypen (**`-`**) or CIDR notation.

**`nmap -sn 192.168.0.1-254`**

**NSE Scripts Overview**

Nmap’s Scripting Engine (NSE) enhances Nmap by running Lua scripts for specialized tasks. These scripts can discover vulnerabilities, brute-force credentials, and retrieve additional network information.

**Working with NSE**

NSE scripts can be run using the `--script` option, specifying either individual scripts or categories (e.g., `--script vuln` for vulnerability scanning). Multiple scripts can be executed simultaneously for in-depth network analysis.

**Searching for NSE Scripts**

NSE scripts are stored in the `/scripts/` directory, and you can search for them by category or function using the `--script-help` command. This helps users find relevant scripts for specific tasks, such as auditing, discovery, or vulnerability detection.

**Firewall Evasion**

Nmap offers several options to bypass firewalls and intrusion detection systems (IDS):

- **Fragmentation** (`f`) sends small packet fragments to evade detection.
- **`--scan-delay <time>ms`**:- used to add a delay between packets sent.
- **Decoy scans** (`D`) spoof multiple IP addresses to obscure the true source.
- **`--badsum`**:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packe
- **Source port manipulation** (`-source-port`) can bypass filters by sending packets from common ports like 80 (HTTP).
- **Timing adjustments** (`T0` to `T5`) control the speed of scans to reduce the chance of detection.