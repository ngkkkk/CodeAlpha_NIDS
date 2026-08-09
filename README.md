# Python Network Intrusion Detection System (NIDS)

This project is a Python-based Network Intrusion Detection System (NIDS) built with Scapy.

## Network Sniffer vs. NIDS

It is important to understand the distinction between a simple network sniffer and an IDS:

- **Network Sniffer**: Captures raw network traffic and displays it. It does not perform stateful analysis or generate security warnings.
- **NIDS (Network Intrusion Detection System)**: Captures traffic, analyzes the state and context of the traffic against predefined rules, and generates actionable security alerts when suspicious patterns are recognized. It also preserves evidence (like logs and PCAPs) for further investigation.

This project goes beyond sniffing by actively analyzing the packet stream to detect common network attacks.

## Core Detections

- 🔴 **Port Scan Detection**: Identifies when a single host attempts to connect to many distinct ports in a short timeframe.
- 🔴 **SYN Flood Detection**: Identifies a high volume of TCP SYN packets from a single source without corresponding ACKs.
- 🔴 **ICMP Flood Detection**: Identifies a high volume of ICMP Echo Requests (pings) from a single source.
- 🟡 **Rate Anomaly / Repeated Connections**: Detects overall suspicious packet rate spikes from a single source.

## Features

- **Configurable Thresholds**: Easily adjust detection sensitivity via `config.py`.
- **Alert Cooldowns**: Prevents console spam by ignoring repeated alerts for the same source and attack type within a time window.
- **Rich Dashboard**: A clean, real-time terminal UI showing traffic statistics and high-priority alerts.
- **Logging**: Alerts are timestamped and saved to `nids_alerts.log`.
- **PCAP Export**: Suspicious traffic is optionally saved to a `.pcap` file for Wireshark analysis.

## Screenshots

### NIDS Dashboard

![NIDS Dashboard](screenshots/nids_dashboard.png)

### Port Scan Detection

![Port Scan Detection](screenshots/port_scan_detection.png)

### Alert Log

![Alert Log](screenshots/alert_log.png)

### PCAP Analysis

![PCAP Analysis](screenshots/pcap_analysis.png)

## Setup

1. Install requirements:
   ```bash
   pip install -r requirements.txt
   ```
2. (Windows Only) Ensure you have Npcap installed (comes with Wireshark).

## Usage

Run the NIDS (Requires Administrator/root privileges):

```bash
python main.py
```

Or specify a specific interface:

```bash
python main.py -i "Wi-Fi"
```

## Testing / Simulation

You can use the provided simulation script to generate controlled local traffic and trigger the detection rules.

```bash
python simulate_attacks.py --all
```

_Note: Depending on your OS, sending Scapy packets to `127.0.0.1` might bypass the standard interface capture. If alerts don't trigger locally, try targeting your machine's LAN IP (e.g., 192.168.1.50) using `python simulate_attacks.py -t 192.168.1.50`._
