A **network flow** is a group of related [[Packet|packets]] treated as one communication stream or conversation.

Instead of analyzing every packet as completely unrelated, a monitoring system groups packets that share identifying information.

## Five-tuple

A flow is commonly identified using five values called the **five-tuple**:

1. Source [[IP address]]
2. Destination [[IP address]]
3. Source [[Port|port]]
4. Destination [[Port|port]]
5. [[Protocol]] such as TCP or UDP

Example:
```
Source IP:         192.168.1.25
Destination IP:    142.250.72.14
Source port:       52143
Destination port:  443
Protocol:          TCP
```

Packets with this same five-tuple can be grouped into one flow.

## Direction

A one-directional flow treats each direction separately:
```
Laptop:52143 -> Website:443
Website:443  -> Laptop:52143
```

A bidirectional flow record combines both directions into one conversation.

The team must define which interpretation is used because it changes the calculated features.

## Flow record

The detector does not need to store every complete packet forever. It can maintain a compact **flow record** containing measurements such as:
- Packet count
- Total bytes
- Start time
- Most recent packet time
- Flow duration
- Inbound and outbound packet counts
- Average packet size
- TCP flag counts

Example:
```
Flow:             192.168.1.25:52143 <-> 142.250.72.14:443 TCP
Packets sent:     35
Packets received: 42
Total bytes:      51,200
Duration:         2.4 seconds
SYN count:        1
ACK count:        68
```

## Flow ending and timeouts

TCP has connection-ending signals such as FIN and RST, but a monitoring system still needs timeout rules. UDP does not establish or close a connection in the TCP sense.

A flow may be considered finished when:
- A TCP connection closes
- No matching packets arrive for a chosen timeout
- A fixed observation window ends

## Flow versus TCP connection

A **TCP connection** is a connection maintained by TCP endpoints.

A **flow** is how a monitoring or analysis system groups related packets. UDP traffic can form a flow even though UDP does not establish a connection.

## Why flows matter to our project

An individual packet may not provide enough evidence to identify an attack. A flow summarizes behavior over several packets.

Useful flow features include:
- Packets per flow
- Bytes per flow
- Packets or bytes per second
- Flow duration
- Average, minimum, and maximum packet size
- Average time between packets
- Inbound-to-outbound traffic ratio
- SYN-to-ACK ratio
- Number of destination ports contacted by one source

Examples:

**Possible normal TCP flow**
```
One SYN followed by responses, acknowledgements, and application data
```

**Possible SYN-flood behavior**
```
Many SYN attempts with very few completed connections or responses
```

## Main idea

> A network flow groups packets that belong to the same communication so the detector can measure their combined behavior over time.

## Check yourself

1. What five values commonly identify a flow?
2. Why can a flow provide more information than one packet?
3. Can UDP traffic form a flow even though UDP does not establish a connection?
4. Why must the team define whether flows are one-directional or bidirectional?
