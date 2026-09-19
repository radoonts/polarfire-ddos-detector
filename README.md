# PolarFire DDoS Detector

Shared notes and implementation workspace for an FPGA-accelerated network-threat detector targeting the **Microchip PolarFire SoC Icicle Kit**.

## Initial project direction

The detector will examine measurable network-traffic behavior over flows or time windows and combine:

- Fast deterministic detection rules
- A trained, quantized machine-learning classifier
- FPGA-accelerated inference and selected calculations

The initial target classes are benign traffic, SYN floods, and UDP floods. Development begins with repeatable PCAP data, followed by live mirrored traffic and possible inline operation if justified by testing.

## Repository structure

- `FPGA Project/` — project planning and team-role notes
- `Key Terms/` — shared networking, security, and FPGA learning notes
- `code/software/` — packet processing, feature extraction, model training, and host software
- `code/fpga/` — FPGA design sources, testbenches, interfaces, and build instructions
- `hardware/` — physical topology, wiring, measurement, and validation material

## Team roles

- **Chace:** network detection, AI, and software
- **Collin:** FPGA acceleration and system integration
- **Kylie:** electrical hardware, instrumentation, and validation

See `FPGA Project/Roles/` for the current responsibility breakdown.

## Opening the notes in Obsidian

1. Clone this repository.
2. Open Obsidian.
3. Choose **Open folder as vault**.
4. Select the cloned repository folder.

The `.obsidian/` directory is intentionally ignored so each teammate can keep personal Obsidian settings and workspace layout.
