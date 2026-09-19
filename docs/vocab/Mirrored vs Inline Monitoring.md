A network detector can observe traffic using two main physical arrangements:

1. **Mirrored or SPAN monitoring** -> the detector receives a copy of the traffic
2. **Inline monitoring** -> the original traffic must pass through the detector

## Mirrored or SPAN monitoring

A managed network switch can copy selected traffic to a monitoring port.

**SPAN** commonly means **Switched Port Analyzer**. It is also called **port mirroring**.

```
Sender ─────> Switch ─────> Destination
                 │
                 └────────> Detector receives a copy
```

The original traffic continues toward its destination. The detector analyzes a separate copy.

Advantages:
- The detector does not add delay to the original traffic path
- Detector failure does not normally stop the original communication
- Safer for early development and demonstrations
- Useful for passive intrusion detection

Limitations:
- The detector normally cannot directly block the original packet
- The mirror port can lose packets if copied traffic exceeds its capacity
- The detector only sees traffic selected by the switch configuration
- Packet timing may differ slightly from the original path

## Inline monitoring

An inline system is placed directly between the sender and destination.

```
Sender ─────> Detector ─────> Destination
```

Every original packet must pass through the detector.

Advantages:
- Can block, modify, rate-limit, or redirect traffic
- Observes the traffic actually passing through the protected link
- Can act as an intrusion-prevention system rather than only a detector

Risks and requirements:
- Must forward legitimate traffic correctly
- Must sustain the required line rate
- Adds some latency
- Packet loss or system failure can interrupt communication
- Requires careful handling of malformed packets, congestion, resets, and crashes

## Detection versus prevention

A passive mirrored system is commonly used for **detection**:
```
Observe suspicious behavior -> generate alert
```

An inline system can perform **prevention**:
```
Observe suspicious behavior -> block or limit traffic
```

Detection and prevention are separate capabilities. A system can detect an attack without being able to stop it.

## Fail-open and fail-closed

These describe what an inline system does when it fails.

**Fail-open:**
```
Detector fails -> traffic continues
```

This favors availability but may allow attacks through.

**Fail-closed:**
```
Detector fails -> traffic is blocked
```

This favors protection but can cause an outage.

A true hardware fail-open path may require additional circuitry or bypass hardware.

## Why mirroring does not guarantee perfect capture

Suppose two one-gigabit links are mirrored onto one one-gigabit monitoring port. If the combined copied traffic exceeds the monitoring port's capacity, some copied packets may be dropped even though the original traffic continues normally.

The team should measure packet loss at the detector rather than assuming every packet was copied successfully.

## Recommendation for our project

The project's intended final architecture is **inline monitoring without materially bottlenecking the link**:
```
Network side A -> Icicle Kit -> Network side B
```

The Icicle Kit has two Gigabit Ethernet ports, so it can physically sit between two network segments. However, the team must demonstrate throughput, latency, and packet-loss performance rather than assuming the FPGA automatically guarantees line-rate forwarding.

A useful architecture separates two logical paths:

**Fast forwarding path**
```
Receive packet -> forward legitimate traffic
```

**Sideband analysis path**
```
Observe packet metadata -> update features -> FPGA inference -> alert or policy decision
```

The forwarding path should not wait for full AI inference on every packet. The detector can classify a flow or time window and then apply a rule to later packets from that flow.

Development should still be staged:
1. Verify that both Ethernet interfaces work
2. Build a transparent software bridge and establish baseline throughput, latency, and loss
3. Observe forwarded traffic without changing forwarding decisions
4. Add FPGA feature processing and inference in the sideband path
5. Apply blocking or rate-limiting only after classification is reliable
6. Compare performance before and after each feature is added

Mirrored/SPAN monitoring remains a useful debugging and model-validation mode, but it is not the intended final architecture.

The phrase **without bottlenecking** must become measurable acceptance criteria, such as sustained throughput, added latency, and packet loss under normal and worst-case traffic.

## Main idea

> Mirrored monitoring analyzes a copy without controlling the original path; inline monitoring processes the original traffic and can block it, but introduces forwarding and reliability requirements.

## Check yourself

1. Why can a mirrored detector fail without stopping normal traffic?
2. Why can an inline detector block an attack while a mirrored detector normally cannot?
3. What is the difference between fail-open and fail-closed?
4. Why might a mirror port drop copied packets?
5. Which arrangement is safer for our first prototype, and why?
