A **time window** is a chosen period during which a detector collects [[Network Traffic|network-traffic]] measurements before calculating features or making a prediction.

Instead of judging every [[Packet|packet]] independently, the system summarizes what happened during an interval such as 100 milliseconds, one second, or five seconds.

Example one-second window:
```
12:00:00.000 ───────────────── 12:00:01.000
       Collect packets and update counters
                         ↓
              Calculate features
                         ↓
                Run classification
```

## Measurements collected in a window

The detector might calculate:
- Total packet count
- Total byte count
- TCP and UDP packet counts
- SYN and ACK counts
- Number of unique source IP addresses
- Number of destination ports contacted
- Average packet size
- Average time between packets

These values can form a feature vector for the model.

## Fixed or tumbling window

A **fixed window**, also called a **tumbling window**, divides time into separate non-overlapping intervals.

Example using one-second windows:
```
Window 1: 0–1 second
Window 2: 1–2 seconds
Window 3: 2–3 seconds
```

At the end of each window, the detector calculates features and begins the next window.

Advantages:
- Simple to implement
- Easy to understand
- Each packet belongs to one window

Disadvantage:
- An event split across a window boundary may appear weaker in both windows

## Sliding window

A **sliding window** overlaps earlier observations.

Example using a two-second window evaluated every half-second:
```
Window 1: 0.0–2.0 seconds
Window 2: 0.5–2.5 seconds
Window 3: 1.0–3.0 seconds
```

Advantages:
- Produces more frequent updates
- Reduces sensitivity to fixed boundaries

Disadvantages:
- Requires more storage or bookkeeping
- Reuses packets in multiple evaluations
- Can require more computation

## Short versus long windows

A **short window** can detect changes quickly but may contain too little information and react strongly to harmless bursts.

A **long window** provides more stable statistics but increases detection delay and may hide brief attacks inside a larger average.

The team must choose a window based on:
- Required detection speed
- Normal traffic behavior
- Attack duration
- Amount of memory available
- Feature-extraction and inference speed

## Global windows versus per-flow windows

A detector can measure:
- All traffic observed during a window
- Each [[Network Flow|network flow]] separately during a window
- Each source or destination separately during a window

These answer different questions.

Examples:
- Global window -> Is the entire link experiencing a flood?
- Per-flow window -> Is one conversation behaving abnormally?
- Per-destination window -> Is one server being attacked by many sources?

## Why this matters to our project

The time window controls both detection quality and response speed.

Example:
```
Normal rate: 1,000 packets per second
Observed in current window: 40,000 packets per second
```

The detector can combine this with protocol, port, IP-address, and TCP-flag measurements before classifying the behavior.

The proposal should state the initial window design rather than merely saying the system operates in "real time."

## Main idea

> A time window is the period of traffic summarized into one set of measurements for analysis or classification.

## Check yourself

1. Why might one packet be insufficient for detecting an attack?
2. What is the difference between a fixed window and a sliding window?
3. What is the tradeoff between a short and long window?
4. How does a global window answer a different question from a per-flow window?
