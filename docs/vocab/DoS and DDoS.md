**DoS** means **Denial of Service**. A DoS attack attempts to make a system or service unavailable to legitimate users by exhausting a limited resource.

**DDoS** means **Distributed Denial of Service**. It has the same goal, but the attack traffic comes from many systems or sources rather than one primary source.

## Resources an attack may exhaust

A denial-of-service attack may target:
- Network bandwidth
- Packets-per-second processing capacity
- CPU time
- Memory
- Connection tables
- Application request capacity

High byte volume is therefore not the only form of exhaustion. A large number of small packets can overwhelm packet-processing or connection-tracking capacity without filling the entire link bandwidth.

## DoS versus DDoS

```
DoS:
One main source ------> Target

DDoS:
Source A ----┐
Source B ----┼--------> Target
Source C ----┤
Many more ---┘
```

Distributed attacks are harder to filter using one source address because malicious traffic may appear to come from many systems.

## Detection signals

Possible indicators include:
- Sudden increase in packet or byte rate
- Many unique source [[IP address|IP addresses]] targeting one destination
- Large number of new [[Network Flow|flows]]
- Strong imbalance between requests and successful responses
- Exhaustion of connection or application resources
- Unusual protocol, port, or packet-size distribution

No single indicator proves an attack. A popular event, software update, or legitimate traffic burst may produce similar behavior.

## Why this matters to our project

The detector can summarize traffic by destination and [[Time Window|time window]] to identify coordinated behavior across many flows.

Useful features may include:
- Packets per second
- Bytes per second
- Number of unique sources
- Number of new flows
- TCP/UDP/ICMP ratios
- SYN-to-ACK ratio
- Inbound-to-outbound traffic ratio

## Main idea

> A denial-of-service attack attempts to exhaust a resource so legitimate users cannot receive normal service; DDoS distributes that activity across many sources.

## Check yourself

1. What is the difference between DoS and DDoS?
2. Why can many small packets be harmful even without consuming all bandwidth?
3. Why does a high traffic rate not automatically prove an attack?
4. Why might per-destination windows help detect DDoS behavior?
