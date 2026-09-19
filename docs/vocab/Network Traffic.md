[[Network Traffic]] means all the [[packet|packets]] moving through a network during some period of time

A [[packet]] is one individual piece of data, while [[network traffic]] is the larger stream formed by many [[Packet|packets]].

```
Packet → Packet → Packet → Packet → Packet
└─────────────────────────────────────────┘
              Network traffic
```

**Traffic direction**
Inbound traffic -> [[Packet|packets]] entering a network
Outbound traffic -> [[Packet|packets]] exiting a network

**Traffic rate**
Measures how quickly data or packets are moving
- Packets per second -> how many individual packets are arriving each second
- Bits per second -> total amount of data transferred each second

**Malicious traffic** is traffic created or manipulated to cause harm
- ***This is what we must distinguish in our project***

**Traffic pattern** describes how packets behave over time

**Traffic burst** is a short period of unusually high activity
- is not automatically an attack, could be from large downloads or joining calls

**Traffic flow** is a smaller conversion within the larger body of network of traffic
