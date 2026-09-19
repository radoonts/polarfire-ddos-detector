A [[packet]] is a small unit of data sent across a network

*Data is divided into many packets*

A packet usually contains:

A [[Header|header]] and a [[Payload|payload]]:

```
┌────────────────────────┬──────────────────────────┐
│ Header                 │ Payload                  │
│ Delivery instructions  │ Information being sent   │
└────────────────────────┴──────────────────────────┘
```

**Why divide data into packets?** -> Packets make networks more managable
- Multiple users can share the network
	- The network can alternate between packets from different devices
- Packets can be routed independently
- Missing information can be resent rather than restarting the entire transfer
- Large data is divided into pieces so that network equipment can process efficiently

## TCP and UDP packets

TCP and UDP are **transport protocols** that describe how applications send data over an IP network.

People commonly say **TCP packet** or **UDP packet**, although the more precise structure is:

```
IP packet
├── IP header
└── TCP segment or UDP datagram
    ├── TCP/UDP header
    └── Application payload
```

A packet's IP header identifies the source and destination devices. The TCP or UDP header identifies the source and destination [[Port|ports]] and provides protocol-specific control information.

### TCP packet

**TCP** stands for **Transmission Control Protocol**. It is designed for reliable, ordered communication.

TCP:
- Establishes a connection before normal data transfer
- Numbers data so it can be placed back in the correct order
- Uses acknowledgements to confirm that data arrived
- Retransmits missing data
- Detects duplicate data
- Controls how quickly data is sent

TCP is commonly used when missing or reordered data would cause a problem, such as webpages, file transfers, and remote login sessions.

A TCP header can contain:
- Source and destination ports
- Sequence number
- Acknowledgement number
- TCP flags such as SYN, ACK, FIN, and RST
- Checksum

TCP behaves somewhat like tracked delivery: the sender expects confirmation and can resend missing information.

### UDP packet

**UDP** stands for **User Datagram Protocol**. It sends data without first establishing a connection and does not guarantee delivery or ordering.

UDP:
- Has a smaller and simpler header
- Does not perform a TCP-style connection handshake
- Does not automatically retransmit missing data
- Does not guarantee that packets arrive in order
- Has less protocol overhead

UDP is useful when low delay matters more than perfect delivery, or when the application provides its own reliability. Examples can include live voice/video, online games, DNS requests, and telemetry.

A UDP header mainly contains:
- Source port
- Destination port
- Length
- Checksum

UDP behaves somewhat like sending ordinary postcards: each message is sent independently, without built-in confirmation that it arrived.

### Main difference

```
TCP -> connection-oriented, reliable, and ordered
UDP -> connectionless, lightweight, and best-effort
```

UDP is not inherently faster in every situation, and TCP does not guarantee that the network itself never loses data. TCP detects and responds to loss so the application receives a reliable ordered byte stream.

### Why this matters to our project

The detector should record whether traffic uses TCP or UDP because attacks can produce different patterns:
- A SYN flood abuses TCP connection establishment
- A UDP flood sends a large volume of UDP datagrams
- TCP flags provide useful detection features
- TCP and UDP traffic using the same port number are still different communication endpoints

Useful features may include:
- Number of TCP packets
- Number of UDP packets
- TCP-to-UDP ratio
- Number of SYN and ACK flags
- Packet rate for each protocol
- Average TCP and UDP packet sizes

## Check yourself

1. What reliability features does TCP provide that UDP does not?
2. Why might live voice or game traffic use UDP?
3. Is a UDP packet automatically malicious?
4. Why should our detector distinguish TCP traffic from UDP traffic?