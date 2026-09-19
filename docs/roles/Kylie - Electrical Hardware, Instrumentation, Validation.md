This role is in charge of building a reliable physical test environment and collecting trustworthy measurements of power, temperature, connectivity, and hardware performance.

This role's rough overview would be:
- Physical system and test-environment setup
- Icicle Kit hardware bring-up
- Power and current measurements
- Thermal testing
- Ethernet connection and reliability testing
- Failure and recovery testing
- Optional alert hardware, such as LEDs or a display
- Possible bypass or support-PCB investigation as a stretch goal

**Electrical Hardware**

We want a defined test environment showing how all the hardware is connected. The setup should first support recorded [[PCAP|PCAP testing]] and later prepare for [[Mirrored vs Inline Monitoring|mirrored or inline live traffic]], depending on the final architecture. [[Chace -  Network Detection, AI, Software|Chace]] defines the traffic source and software test procedure, while Kylie provides the matching physical topology and verifies that the intended traffic actually reaches the board.

Maintain a hardware inventory and a physical topology diagram showing power, Ethernet, USB/UART, traffic-source, and traffic-destination connections. The Icicle Kit hardware bring-up should confirm that the board boots reliably, both Ethernet links work, and the debug connection is available. Kylie also coordinates with [[Collin - FPGA Acceleration, System Integration|Collin]] to ensure the correct FPGA build is programmed and the required hardware connections match his interface design.

A custom PCB is not required for the first version. It should only be considered later if it meaningfully improves measurements, indicators, protected connections, or demonstration reliability. A Gigabit Ethernet bypass is an especially difficult stretch goal and should not delay the detector.

**Instrumentation**

Instrumentation means measuring the physical system rather than simply checking whether it turns on. Useful measurements include:
- Input voltage and current
- Total power consumption
- Board temperature
- Ethernet [[Bandwidth|throughput]] and packet loss
- Results for idle, Chace's CPU-only detector, and Collin's FPGA-accelerated detector

These measurements connect the software and FPGA results to the real hardware and help show whether acceleration provides a genuine performance or efficiency benefit.

**Validation**

Confirm that the board and physical setup work reliably and repeatedly. Test normal startup, power cycling, Ethernet disconnection and reconnection, sustained traffic, and recovery from failures. Record the expected result, observed result, pass/fail status, and the relevant Chace software version and Collin FPGA build.

Kylie should identify whether link loss, packet loss, unstable power, overheating, or another physical problem affects the detector results before the team assumes the fault is in Chace's software or Collin's FPGA logic. Clear documentation can be reused in the final report and should allow another teammate to reproduce the complete setup.
