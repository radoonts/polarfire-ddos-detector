**Packet capture** is the process of copying [[Packet|packets]] observed by a network interface so software can inspect, analyze, or save them.

A capture tool receives packets from an interface such as Ethernet or Wi-Fi and records information including:
- Arrival timestamp
- Packet length
- [[Header|Header]] bytes
- [[Payload|Payload]] bytes, if included
- The interface where the packet was observed

## Basic process

```
Network traffic
      ↓
Network interface
      ↓
Capture software
      ├── Display or analyze packets
      └── Save packets to a [[PCAP]] file
```

Common capture and analysis tools include Wireshark, `tcpdump`, and applications built using packet-capture libraries.

## Capture point

A capture only sees traffic available at its observation point.

Examples:
- Capturing on a laptop normally shows traffic available to that laptop
- Capturing on a router may show traffic passing through that router
- Capturing from a switch mirror/SPAN port can show copies of selected switch traffic

A capture is not automatically a complete view of the entire network.

## Promiscuous mode

In **promiscuous mode**, a network interface passes more of the frames it observes to capture software instead of accepting only traffic addressed to itself.

This does not magically reveal all network traffic. The physical network and switch configuration still determine which frames reach the interface.

## Capture filters and display filters

A **capture filter** decides which packets are recorded.

A **display filter** decides which already-recorded packets are shown during analysis.

Filtering can reduce storage and focus analysis, but an overly restrictive capture filter can permanently discard evidence that was not saved.

## Packet loss during capture

Capture software can drop packets if traffic arrives faster than the system can copy or process it.

The team should measure:
- Packets observed
- Packets captured
- Packets dropped
- Capture rate

A detector cannot classify packets it never received.

## Why packet capture matters to our project

Packet capture provides the raw traffic from which the software calculates features.

Initial workflow:
```
Live or replayed traffic
        ↓
Packet capture on Linux
        ↓
Read IPs, ports, protocol, flags, size, and timestamp
        ↓
Group packets into [[Network Flow|flows]] or [[Time Window|time windows]]
        ↓
Calculate model features
```

The first version can capture packets in Linux and send calculated feature vectors to the FPGA. Later versions may move selected parsing or feature calculations into FPGA fabric.

## Privacy and safety

Captures may contain private information, authentication material, addresses, or application data. Only capture networks and devices the team owns or has permission to monitor. Avoid publishing sensitive payloads in the contest repository.

## Main idea

> Packet capture copies packets visible to a network interface so they can be inspected, measured, or saved.

## Check yourself

1. Why does a packet capture not necessarily show the entire network?
2. What is the difference between a capture filter and display filter?
3. Why should the team measure dropped packets?
4. Which packet fields would our feature extractor need?
