A **UDP flood** is a denial-of-service attack that sends a large volume of UDP datagrams toward a target in an attempt to consume bandwidth or processing resources.

UDP is connectionless and does not use TCP's three-way handshake.

## Basic behavior

```
Large volume of UDP datagrams ------> Target
```

The traffic may target:
- One UDP port
- Many UDP ports
- An application that uses UDP
- Closed ports that still require the target to inspect and reject traffic

The exact effect depends on the target and network configuration.

## Why UDP can be used for floods

UDP:
- Does not require a connection handshake
- Allows independent datagrams to be sent
- Does not provide built-in sender authentication
- Can use spoofed source IP addresses in some environments

These properties do not make UDP malicious. They mean UDP traffic must be evaluated by its behavior rather than by protocol name alone.

## Possible detection signals

- Sudden increase in UDP packets per second
- Sudden increase in UDP bytes per second
- UDP traffic greatly exceeding its normal baseline
- Many source addresses targeting one destination
- Unusual destination-port distribution
- Repeated packet sizes or timing patterns
- Strong inbound-to-outbound imbalance

## False positives

Legitimate applications can produce high UDP traffic, including live video, voice communication, games, DNS activity, and telemetry. A detector should learn or define normal behavior for the monitored environment.

## Why this matters to our project

Useful features include:
- UDP packet count
- UDP byte count
- UDP packets and bytes per second
- Unique source count
- Unique destination-port count
- Average and variance of packet size
- Average time between datagrams
- Inbound-to-outbound ratio

## Main idea

> A UDP flood attempts to exhaust a target or network by sending an abnormally large volume of UDP datagrams.

## Check yourself

1. Why does a UDP flood not depend on a TCP handshake?
2. What resources can a UDP flood consume?
3. Why is high UDP traffic not automatically malicious?
4. Which measurements could distinguish ordinary UDP traffic from a flood?
