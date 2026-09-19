A **network port** is a number that identifies a particular application or service on a device.

An [[IP address]] identifies the device, while a port identifies which program or service on that device should receive the data.

A useful analogy is:
- **IP address** -> the address of an apartment building
- **Port** -> a particular apartment inside the building

## Source and destination ports

A TCP or UDP [[Packet|packet]] normally contains:
- **Source port** -> identifies the sending application's temporary communication endpoint
- **Destination port** -> identifies the service the packet is trying to reach

Example:
```
Source IP:         192.168.1.25
Source port:       52143
Destination IP:    142.250.72.14
Destination port:  443
Protocol:          TCP
```

This means an application using port `52143` on `192.168.1.25` is communicating with a service using port `443` on `142.250.72.14`.

## Port-number range

A port number is 16 bits wide, so valid port numbers range from:
```
0 through 65535
```

TCP and UDP maintain separate port spaces. TCP port 53 and UDP port 53 are different communication endpoints even though they use the same number.

## Common service ports

Some commonly used destination ports are:
- `22` -> SSH remote access
- `53` -> DNS name lookup
- `80` -> HTTP web traffic
- `443` -> HTTPS encrypted web traffic

These are conventions rather than an absolute guarantee. An application can sometimes use a nonstandard port, and malicious traffic can deliberately use a familiar port.

## Temporary or ephemeral ports

A client application usually selects a temporary **ephemeral port** for its side of a connection.

Example:
```
Laptop:52143 <----> Website:443
```

The website listens on the familiar service port `443`, while the laptop uses temporary port `52143` to distinguish this connection from its other connections.

## Port versus physical port

A **network port number** is a logical number stored in packet data.

A **physical Ethernet port** is the connector where an Ethernet cable is plugged in.

They are unrelated concepts that happen to use the same word.

## Why ports matter to our project

Our detector can examine port behavior to calculate features such as:
- Destination ports contacted by one source
- Number of distinct ports contacted during a time window
- Repeated traffic aimed at one service
- Unexpected services receiving traffic
- Sudden changes in normal port usage

## Port scanning

A **port scan** occurs when a device tests many destination ports to discover which services are available.

Example:
```
Source 192.168.1.50 contacts:
10.0.0.8:20
10.0.0.8:21
10.0.0.8:22
10.0.0.8:23
...
10.0.0.8:500
```

Contacting many ports quickly can be suspicious, although legitimate administrative and security tools can also perform scans.

## Main idea

> An IP address identifies a device or network interface, while a network port identifies an application or service on that device.

## Check yourself

1. What is the difference between an IP address and a port?
2. Why does a client usually use a temporary source port?
3. What is the difference between network port `443` and a physical Ethernet port?
4. Why might contacting hundreds of destination ports be suspicious?
