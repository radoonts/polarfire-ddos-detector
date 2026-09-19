**PCAP** commonly refers to a packet-capture file containing recorded network packets and associated capture metadata.

A [[Packet Capture|packet-capture]] tool such as Wireshark or `tcpdump` can save observed packets into a PCAP file for later analysis.

## What a PCAP can contain

For each recorded packet, a capture file can store information such as:
- Arrival timestamp
- Number of bytes captured
- Original packet length
- Raw packet bytes, including protocol headers

Whether the full [[Payload|payload]] is present depends on how the capture was configured.

## Recording versus replaying

**Recording** writes observed packets into a PCAP file:
```
Live traffic -> capture tool -> traffic.pcap
```

**Analysis** reads the file without transmitting its packets:
```
traffic.pcap -> Wireshark or analysis program
```

**Replay** sends recorded packet data back through a test network using a suitable replay tool:
```
traffic.pcap -> replay tool -> test network
```

Opening a PCAP for analysis is not the same as replaying it.

## Why PCAP is useful for testing

A saved capture provides repeatable input.

The team can use the same traffic to test:
- Software feature extraction
- The quantized reference model
- FPGA inference
- Later design revisions

This makes comparisons fair because each version processes the same recorded traffic.

Example workflow:
```
Known PCAP
    ↓
Extract features
    ↓
Software prediction
    ↓
FPGA prediction
    ↓
Compare outputs and timing
```

## Ground truth

A PCAP contains packets, but it does not automatically contain trustworthy attack labels.

For model evaluation, the team also needs **ground truth** describing what the traffic actually represents, such as:
- Benign traffic
- SYN flood
- UDP flood
- Port scan

The labels may come from a controlled experiment, dataset documentation, or a separate label file.

## Limitations

A PCAP may be incomplete because:
- Packets were dropped during capture
- Only part of each packet was saved
- Traffic was filtered
- The capture point could not observe all directions
- Encryption hides application payload contents

The team must document how each capture was created.

## PCAP and PCAPNG

**PCAPNG** is a newer capture format that can store richer metadata and information from multiple interfaces. Wireshark commonly supports both PCAP and PCAPNG.

For the project, either can work if the software tools support the chosen format and the format is documented.

## Privacy and safety

A capture file may contain sensitive network data. Only record or replay traffic in an authorized test environment, and remove or anonymize sensitive information before publishing files.

## Main idea

> A PCAP is a saved recording of observed network packets that allows the same traffic to be analyzed and tested repeatedly.

## Check yourself

1. What is the difference between capturing, analyzing, and replaying packets?
2. Why does using the same PCAP improve experiment repeatability?
3. Does a PCAP automatically provide correct attack labels?
4. Why might a PCAP be incomplete?
