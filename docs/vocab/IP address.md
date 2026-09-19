*IP stands for Internet Protocol.*

An [[IP address]] is a numerical address that identifies a device or network interface so [[Packet|packets]] can be delivered to the correct place.

Every IP [[Packet|packet]] contains:
- **Source IP address** -> where the packet claims to have come from
- **Destination IP address** -> where the packet should go

Example:
```
Source IP:       192.168.1.25
Destination IP:  142.250.72.14
```

This means a device using `192.168.1.25` is sending a packet toward `142.250.72.14`.

## IPv4

An **IPv4 address** contains four numbers separated by periods:
```
192.168.1.25
```

Each number can range from `0` to `255`. Together, the four numbers represent a 32-bit address.

## IPv6

**IPv6** is a newer addressing system that uses 128-bit addresses, allowing far more possible addresses.

Example:
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

Our first project version can focus on IPv4 and treat IPv6 support as a later improvement.

## Private and public IP addresses

A **private IP address** is used inside a local network and is not normally routed directly across the public internet.

Common private IPv4 ranges include:
```
10.x.x.x
192.168.x.x
172.16.x.x through 172.31.x.x
```

A **public IP address** is used to communicate across the internet. A home router normally has a public IP address, while devices inside the home commonly use private addresses.

Simplified example:
```
Laptop                 Router                    Internet
192.168.1.25 ──────> Public IP address ──────> Website
Private IP
```

## Static and dynamic IP addresses

- **Static IP address** -> intentionally kept constant
- **Dynamic IP address** -> may change over time

Home devices commonly receive dynamic private addresses from the router. Servers and infrastructure may use static addresses so other systems can reliably locate them.

## IP spoofing

**IP spoofing** means placing a false source IP address inside a packet.

Because the source address can sometimes be forged, an IP address does not automatically prove which person or physical device created the traffic.

## Why IP addresses matter to our project

Our detector can use IP addresses to measure [[Network Traffic|traffic]] behavior such as:
- Number of packets sent by each source
- Number of unique source addresses
- Number of destinations contacted by one source
- Many sources sending traffic to one destination
- One source contacting many destinations
- Changes in the distribution of source addresses

Examples:

**Possible single-source flood**
```
One source IP sends 50,000 packets to one destination in one second
```

**Possible distributed flood**
```
Thousands of source IPs send packets to one destination
```

**Possible network scan**
```
One source IP contacts many destinations or services in a short period
```

These patterns may be suspicious, but none proves an attack by itself. The detector must combine IP-address behavior with other information such as timing, packet rate, ports, protocols, and TCP flags.

## Main idea

> An IP address is a numerical network address stored in a packet so the network knows where the packet came from and where it should go.

## Check yourself

1. What is the difference between a source IP and a destination IP?
2. What is the difference between a private and public IP address?
3. Why does a source IP not always prove who sent a packet?
4. How could IP-address patterns help detect a DDoS attack?
