A **protocol** is an agreed set of rules that devices or programs follow when communicating.

A protocol defines things such as:
- How a message is formatted
- What each field means
- When a message may be sent
- How the receiver should respond
- How errors or missing information are handled

A useful analogy is a spoken language. Two people may both be capable of making sounds, but they cannot exchange useful information unless they understand the same language and its rules.

## Why protocols are necessary

Sending electrical or radio signals is not enough. Both sides must agree on how to interpret those signals.

For example, a protocol may define:
```
First field: source address
Second field: destination address
Third field: message type
Remaining bytes: data
```

If the sender and receiver disagree about that format, the receiver will interpret the message incorrectly.

## Protocols used together

Network communication normally uses several protocols in layers rather than one protocol doing everything.

A simplified stack is:
```
Application:  HTTP, HTTPS, DNS
Transport:    TCP or UDP
Network:      IP
Local link:   Ethernet or Wi-Fi
Physical:     Electrical, optical, or radio signals
```

Each layer has a different responsibility:
- **Ethernet/Wi-Fi** -> moves data across the local network
- **IP** -> provides source and destination network addresses
- **TCP** -> provides reliable, ordered communication
- **UDP** -> provides lightweight, best-effort datagrams
- **HTTP** -> defines web requests and responses
- **DNS** -> translates names such as `example.com` into IP addresses

## Encapsulation

When an application sends data, each network layer adds its own control information.

Example:
```
Ethernet frame
└── IP packet
    └── TCP segment
        └── HTTP data
```

The receiving device removes and interprets those layers in the opposite order.

## Protocol identification

The [[Header|header]] contains information that tells the receiver which protocol should interpret the next section.

For example, an IPv4 header contains a protocol-number field. Common values include:
- `6` -> TCP
- `17` -> UDP
- `1` -> ICMP

This allows the receiver to send TCP data to its TCP implementation and UDP data to its UDP implementation.

## Protocol versus port

A [[Port|port]] identifies an application communication endpoint within TCP or UDP.

A protocol defines the communication rules.

For example:
```
Protocol: TCP
Destination port: 443
```

This means the packet uses TCP's rules and is being directed to a service using TCP port `443`.

## Why protocols matter to our project

The detector must identify protocols because different protocols produce different normal behavior and attack patterns.

Examples:
- A SYN flood abuses TCP connection establishment
- A UDP flood produces unusually high UDP traffic
- An ICMP flood may contain many ping-related messages
- A DNS attack may target UDP or TCP port 53

Useful model features may include:
- Number of TCP packets
- Number of UDP packets
- Number of ICMP packets
- TCP-to-UDP ratio
- Traffic rate for each protocol
- Unexpected or uncommon protocols

A protocol by itself is not malicious. The detector must examine how it is being used.

## Main idea

> A protocol is a shared set of formatting and behavior rules that allows two systems to interpret and respond to each other's messages correctly.

## Check yourself

1. Why are physical signals alone not enough for communication?
2. What is the difference between a protocol and a port?
3. Why does one network transmission use several protocols at once?
4. Which responsibilities belong to IP, TCP, and HTTP?
