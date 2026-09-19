Basically, turn the proven software detector calculations into FPGA hardware, prove that the hardware produces correct results, and integrate the team's components into one complete detector (and get that bag).

My role contains:
- Receive the trusted software detector from [[Chace -  Network Detection, AI, Software|Chace]]
- Choose which calculations are worth accelerating
- Define how software communicates with the FPGA
- Implement selected calculations in FPGA hardware
- Compare hardware results with software results
- Measure speed and FPGA resource usage
- Integrate and demonstrate the complete system

**FPGA Acceleration**

Understand the hardware inputs and outputs, decide what belongs in the FPGA, create the software-to-FPGA interface, and build the accelerator. Chace's software will initially turn [[Network Traffic|network traffic]] into an ordered feature vector and provide the trained, quantized model parameters and expected results. My FPGA hardware will accept those features and return a prediction such as benign, [[SYN Flood|SYN flood]], or [[UDP Flood|UDP flood]].

FPGA acceleration does not simply mean assigning fewer tasks to the CPU. It means moving suitable repeated calculations—initially model inference and possibly fast rules—into dedicated parallel or pipelined hardware. Packet capture, [[Network Flow|flow]] tracking, [[Time Window|time-window]] management, and logging can remain in software at first. More work should move into the FPGA only if measurements show that it is useful.

The accelerator should be built gradually:
- Software writes values and reads them back
- FPGA adds two software-provided values
- FPGA processes one model operation or artificial neuron
- FPGA processes one complete layer
- FPGA runs the complete small quantized model

**Verification and Performance**

Use the same known-answer feature vectors in Chace's software model, FPGA simulation, and the physical FPGA. Their results should agree; otherwise, check feature order, numeric scaling, signed values, rounding, model parameters, and communication timing.

Measure inference latency, feature vectors per second, FPGA clock rate, logic/memory/DSP usage, timing results, and CPU utilization. [[Kylie - Electrical Hardware, Instrumentation, Validation|Kylie]] will connect these results to measured power, temperature, Ethernet [[Bandwidth|throughput]], and hardware stability. Together, these measurements show whether FPGA acceleration actually improves the system instead of merely relocating the work.

**System Integration**

Connect all three roles and maintain the interfaces between them. Chace and I must agree on the feature order, numeric formats, model parameters, start/result behavior, prediction encoding, and known-answer tests. Kylie and I must ensure that the programmed FPGA, board connections, power, and physical test setup match the documented design.

I will help keep the FPGA project, software-to-FPGA interface, model version, test vectors, and hardware build synchronized. The final system should accept traffic from recorded [[PCAP|PCAP files]], mirrored capture, or a possible inline path without changing what each feature or prediction means. See [[Mirrored vs Inline Monitoring]].
