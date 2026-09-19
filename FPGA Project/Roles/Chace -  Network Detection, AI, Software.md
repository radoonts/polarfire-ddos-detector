Our main goal is to deploy a trained, quantized AI model as an FPGA inference accelerator so that it can classify malicious [[Network Traffic|traffic]] and [[DoS and DDoS|DDoS]] patterns quickly.

Chace's main responsibility is to build the trusted software version of the detector, train and evaluate the model, and provide the features, model parameters, and test cases needed for [[Collin - FPGA Acceleration, System Integration|Collin's FPGA implementation]].

A rough overview would be:
- Define the threat model
- Select and understand a labeled dataset
- Build the [[Packet|packet]], [[Network Flow|flow]], and [[Time Window|time-window]] pipeline
- Choose features
- Build a baseline rule-based detector
- Train and evaluate the AI model
- Quantize and export the trained model
- Convert the working detector into C++/Rust and connect it to the FPGA

**Network Detection**

We want to observe traffic over a short [[Time Window|time window]], measure suspicious behavior, combine fast rules with AI classification, and then produce a response.

The first attack classes will likely be:
- Benign traffic
- [[SYN Flood|SYN flood]]
- [[UDP Flood|UDP flood]]

Development can begin with labeled [[PCAP|PCAP files]], then move to live [[Packet Capture|packet capture]]. The final traffic source could use [[Mirrored vs Inline Monitoring|mirrored or inline monitoring]], depending on which architecture performs best. Chace defines what traffic the software expects, while [[Kylie - Electrical Hardware, Instrumentation, Validation|Kylie]] prepares and verifies the corresponding physical network setup so capture problems are not mistaken for detector errors.

**AI**

The AI model will be trained on labeled examples of benign and malicious traffic. It will probably classify feature vectors containing measurements such as packet rate, byte rate, SYN and ACK counts, UDP count, and unique source count rather than reading raw packet payloads directly.

Training and dataset analysis will most likely happen in Python on a development computer. The FPGA will perform **inference** using the trained model. Chace must provide Collin with the exact feature order and ranges, quantized weights and scaling rules, known-answer feature vectors, expected classifications, and software accuracy results so the FPGA can reproduce the same detector.

The response may include an alert, threat score, rate limit, or block rule. A mirrored detector can generate alerts but cannot directly block the original packet; direct blocking requires an inline forwarding path or a separate enforcement device.

**Software**

The deployed software will most likely be programmed in either C++ or Rust. Both provide native performance and low-level access needed for packet parsing, flow tracking, live capture, and communication with the FPGA.

Chace and Collin must agree on how features are sent, how the FPGA is started, how result validity is reported, and how predictions and errors are encoded. Chace also supplies CPU-only accuracy and performance baselines; Collin compares these with FPGA results, while Kylie checks whether power, temperature, link stability, or packet loss affects the comparison.

The software should remain modular so the same detection pipeline can accept recorded PCAP traffic, mirrored live traffic, or inline traffic without rebuilding the entire detector.
