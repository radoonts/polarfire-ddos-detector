**Bandwidth** is the maximum amount of data a communication path can theoretically carry per unit of time.

It describes the capacity of a link, similar to how the number of lanes describes the capacity of a road.

Bandwidth is commonly measured in **bits per second**:
- `Kbit/s` -> kilobits per second
- `Mbit/s` or `Mbps` -> megabits per second
- `Gbit/s` or `Gbps` -> gigabits per second

## Bits versus bytes

A lowercase `b` means **bits**. An uppercase `B` means **bytes**.

```
8 bits = 1 byte
```

Therefore, under ideal decimal-unit calculations:
```
1 Gbit/s = 125 MB/s
100 Mbit/s = 12.5 MB/s
```

Protocol overhead and system limitations make real application-transfer rates lower than the theoretical conversion.

## Bandwidth versus throughput

**Bandwidth** is the link's theoretical capacity.

**Throughput** is the data rate actually achieved.

Example:
```
Link bandwidth:       1 Gbit/s
Measured throughput:  930 Mbit/s
```

Throughput may be lower because of protocol headers, processing limits, congestion, packet loss, storage speed, or software overhead.

## Bandwidth versus latency

**Bandwidth** describes how much data can be carried per second.

**Latency** describes how long one piece of data takes to travel or be processed.

A link can have high bandwidth but high latency, or low bandwidth but low latency.

Road analogy:
- Number of lanes -> bandwidth
- Travel time for one car -> latency
- Cars actually arriving each second -> throughput

## Bandwidth versus packet rate

Two traffic streams can use similar bandwidth while containing different numbers of [[Packet|packets]].

```
Stream A: fewer large packets
Stream B: many small packets
```

Stream B may require more packet-processing work because each packet has its own headers and must be examined separately.

For our project, measure both:
- Bits or bytes per second
- Packets per second

## Bandwidth exhaustion

If incoming traffic reaches or exceeds the capacity of a link, legitimate traffic may be delayed or dropped.

```
Link capacity:       1 Gbit/s
Incoming demand:     greater than 1 Gbit/s
Result:              congestion and packet loss
```

A DDoS attack may attempt to consume link bandwidth, but other attacks may instead exhaust packet-processing or connection-tracking capacity.

## Why bandwidth matters to our project

The Icicle Kit's inline detector must forward traffic without materially reducing the target link rate.

The team should compare:
- Link bandwidth
- Measured forwarding throughput
- Packets per second
- Added latency
- Packet loss
- Performance with and without feature extraction and FPGA inference

The phrase "no bottleneck" should be supported by measurements rather than assumed from the advertised port rate.

## Main idea

> Bandwidth is the theoretical data-carrying capacity of a communication path; throughput is the data rate actually achieved.

## Check yourself

1. What is the difference between `Gbps` and `GB/s`?
2. What is the difference between bandwidth and throughput?
3. Can a high-bandwidth link still have high latency?
4. Why must our detector measure packets per second as well as bits per second?
