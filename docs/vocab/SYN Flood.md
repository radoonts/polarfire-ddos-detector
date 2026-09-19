A **SYN flood** is a denial-of-service attack that abuses TCP connection establishment.

## Normal TCP handshake

TCP normally begins a connection using a three-way handshake:
```
Client                         Server
  | -------- SYN ------------> |
  | <------ SYN-ACK ----------- |
  | -------- ACK ------------> |
  |       Connection ready      |
```

- **SYN** -> client requests a connection
- **SYN-ACK** -> server acknowledges and responds
- **ACK** -> client completes the handshake

## SYN-flood behavior

During a SYN flood, a target receives a large number of SYN requests, while many handshakes are never completed.

```
Many SYN requests --------> Server
Few final ACKs -----------> Server
```

The target may maintain state or spend processing resources on many incomplete connection attempts. If enough resources are consumed, legitimate clients may have difficulty connecting.

Source addresses may also be spoofed, so a large number of apparent source IP addresses does not always mean that many real devices sent the traffic.

## Possible detection signals

- Very high SYN packet rate
- Large number of incomplete TCP handshakes
- SYN count greatly exceeding completed connections
- Strong SYN-to-final-ACK imbalance
- Many short-lived or half-open connection records
- Repeated attempts toward one destination IP and port

## False positives

A traffic spike, popular service launch, failed server, or network problem may also create incomplete connections. The detector should combine multiple measurements rather than label every SYN burst as an attack.

## Why this matters to our project

Useful window or flow features include:
- SYN count
- SYN-ACK count
- Final ACK count
- Completed-handshake count
- Incomplete-handshake count
- SYN rate
- Unique source count
- Destination port
- Average duration of incomplete attempts

## Main idea

> A SYN flood overwhelms TCP connection establishment by creating many connection requests that are not successfully completed.

## Check yourself

1. What are the three messages in a normal TCP handshake?
2. Which part is commonly missing during a SYN flood?
3. Why can incomplete handshakes consume target resources?
4. Why is a high SYN count alone insufficient proof of an attack?
