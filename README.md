# Wireshark Self Study

This repository is part of my 3-hour self-study sessions, where I take one topic and study it for 3 hours.

## Notes on Wireshark (Theory - Questions I'm trying to answer/understand):

### 1. What is Wireshark?
It is an open-source tool that captures and analyzes network traffic in real-time. It's a powerful network protocol analyzer used for network troubleshooting, analysis, and software development.

### 2. What is a packet?
A packet is the unit of data transferred at the Network Layer (Layer 3) of the OSI model. It is a small unit of data that contains a payload (the actual data) and addressing information, like the source and destination IP addresses.

### 3. What is a Frame?
A frame is the data unit used by the Data-Link layer (Layer 2). It encapsulates a packet and includes the physical MAC addresses of the source and destination devices. It also contains a checksum for error detection.

### 4. What are protocols?
Protocols are a set of rules that define how data is formatted, transmitted, and received in a network.
*Examples: HTTP, TCP, UDP, IP, SMTP, SNMP, etc.*

### 5. What are TCP and UDP, and what are the differences between them?
*   **TCP (Transmission Control Protocol)** establishes a connection before sending data, making it reliable. It's used for services where data integrity is crucial (e.g., HTTP, SMTP).
*   **UDP (User Datagram Protocol)** is connectionless and does not guarantee delivery, which makes it faster. It's useful for speed-sensitive applications (e.g., streaming, online gaming, DNS).

### 6. What are capture filters vs. display filters in Wireshark, and how do they differ in purpose?
*   **Capture Filters:** Used *before* starting a packet capture to limit the amount of data captured. This is more efficient as it reduces the size of the capture file.
    *   *Example:* `host 192.168.1.1`
*   **Display Filters:** Used *after* packets have been captured to hide or show specific packets from the captured data. They do not remove packets from the capture file.
    *   *Example:* `ip.addr == 192.168.1.1`

### 7. How can you quickly identify the source and destination IPs and ports in a captured TCP conversation?
*   Use a display filter like `ip.src == 192.168.1.1 and ip.dst == 8.8.8.8`.
*   Use the **Follow TCP Stream** feature (Shortcut: `Ctrl+Alt+Shift+T`).
*   Go to **Statistics > Conversations**, select the TCP tab, choose the desired conversation, and click "Apply as filter."

### 8. What does the “Follow TCP Stream” feature do, and when would you use it?
This feature reconstructs and displays the data from a single TCP connection in a human-readable format. It helps in understanding the application layer (Layer 7) data being exchanged and visualizing the flow of a conversation.

### 9. How can you detect a potential network attack (e.g., ARP spoofing or a SYN flood) using Wireshark?
*   **ARP Spoofing:** Filter for ARP traffic with `arp`. Look for duplicate IP address announcements with different MAC addresses. A filter like `arp.duplicate-address-detected` can also highlight this.
*   **SYN Flood:** Filter for SYN packets that haven't been acknowledged using `tcp.flags.syn == 1 and tcp.flags.ack == 0`. A large number of these packets from one or multiple sources to a single target without a corresponding `[SYN, ACK]` suggests a SYN flood attack.

### 10. What are the key packets in the TCP three-way handshake, and how can you verify it in a capture?
The three-way handshake establishes a TCP connection and consists of three steps:
1.  The client sends a `[SYN]` packet to the server.
2.  The server replies with a `[SYN, ACK]` packet.
3.  The client sends an `[ACK]` packet back to the server.

You can filter for `tcp.flags.syn == 1` to easily locate the start of these handshakes in a capture.

### 11. How can you filter packets to only show HTTP traffic or DNS queries?
*   **HTTP:** Use the display filter `http` or `tcp.port == 80`.
*   **DNS:** Use the display filter `dns` or `udp.port == 53`.

### 12. How can you use Wireshark to identify packet loss, retransmissions, or latency issues?
Use the built-in expert analysis filters:
*   **Packet Loss/Retransmissions:** `tcp.analysis.retransmission` or `tcp.analysis.duplicate_ack`.
*   **Latency:** Analyze the `tcp.time_delta` field, which shows the time between packets in a conversation. High deltas can indicate latency issues.

---
*For practice, I used PCAP files from malware-traffic-analysis.net.*

Feel free to correct or add your own notes.
