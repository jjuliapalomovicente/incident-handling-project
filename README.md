# incident-handling-project
Malware Traffic Analysis and Timeline Reconstruction using Wireshark, Plaso, and Timesketch
---
## 1. Project Overview  
This project investigates suspicious network activity using the **2025-12-11 Kongtuke ClickFix Activity dataset** from Malware-Traffic-Analysis. The main objective was to identify Indicators of Compromise (IoCs), analyze attacker behavior, and understand how the infection occurred.

The project simulates a real-world incident response scenario, where network traffic is analyzed to detect malicious activity and support investigation decisions.

---

## 2. Project Relevance  
Incident response is a critical part of cybersecurity. This project demonstrates how analysts detect and investigate threats using network traffic and forensic tools. By analyzing DNS requests, TCP connections, and encrypted communication, it is possible to identify suspicious behavior and respond to potential attacks.

This project also highlights the importance of timeline reconstruction in understanding how an attack develops over time.

---

## 3. Dataset  
- **Dataset Name:** 2025-12-11 Kongtuke ClickFix Activity  
- **Source:** Malware-Traffic-Analysis  
- **Files Used:**
  - PCAP network capture files  
  - HTTPS traffic captures  
  - Indicators of Compromise (IoCs)  
  - Supporting infected host artifacts  

This dataset simulates a realistic malware infection and provides both network and forensic data for analysis.

---

## 4. Tools Used  

| Tool | Purpose | Role in Incident Response |
|------|--------|--------------------------|
| Wireshark | Analyze network traffic and packets | Detection / Investigation |
| Timesketch | Visualize timeline of events | Analysis / Decision-making |
| log2timeline (Plaso) | Extract forensic timeline data | Investigation |
| Docker | Deploy Timesketch environment | Setup |

---

## 5. Methodology  

The investigation followed a structured approach:

1. **Data Collection**  
   The PCAP files from the dataset were collected and prepared for analysis.

2. **Network Traffic Analysis (Wireshark)**  
   The PCAP files were loaded into Wireshark to examine network activity. Filters were applied to focus on DNS traffic, TCP connections, and suspicious communication patterns.

3. **Identification of Suspicious Activity**  
   DNS queries, outbound connections, and repeated traffic patterns were analyzed to detect abnormal behavior.

4. **Extraction of Indicators of Compromise (IoCs)**  
   Key indicators such as IP addresses, domains, and infected hosts were identified.

5. **Timeline Reconstruction (Planned)**  
   The project planned to use log2timeline (Plaso) to extract forensic events and generate a timeline.

6. **Timesketch Deployment**  
   Timesketch was deployed using Docker to visualize and correlate events. However, full access to the interface was not achieved due to compatibility issues.

---

## 6. Results  

### 6.1 Initial Connection  

During the analysis, a DNS query for the domain **lotw.org** was observed. This domain resolved to the external IP address **162.159.134.42**.  

The internal host **10.12.11.101** then initiated communication with this IP, establishing a TCP connection followed by TLS encrypted traffic.

This behavior is suspicious because it indicates that the internal system is communicating with an external server, which could be part of command-and-control (C2) activity or malicious script execution.
 
*Figure 1. DNS resolution and initial encrypted connection observed in Wireshark.*

---

### 6.2 DNS Traffic Analysis  

Further analysis revealed multiple DNS requests to external domains. The traffic included communication with services such as Cloudflare and other external domains, which may indicate webpage loading or automated script activity.

Repeated DNS requests and consistent outbound communication patterns suggest that the system may be running automated processes or maintaining communication with external infrastructure.

*Figure 2. Repeated DNS requests to multiple external domains observed in Wireshark.*

---

## 7. Indicators of Compromise (IoCs)  

| Type | Indicator | Description |
|------|----------|------------|
| Internal Host | 10.12.11.101 | Potential infected machine |
| External IP | 162.159.134.42 | External server contacted |
| Domain | lotw.org | Suspicious queried domain |
| DNS Query | wpad.localdomain | Possible proxy discovery activity |

These indicators suggest that the internal host was compromised and actively communicating with an external system. The repeated DNS queries and encrypted traffic indicate possible automated malicious activity.


*Figure 3. Indicators of Compromise identified through network traffic analysis.*

---

## 8. Timesketch Deployment  

Timesketch was successfully deployed using Docker. The backend services, including PostgreSQL, OpenSearch, and Redis, were running correctly.


*Figure 4. Successful Timesketch deployment using Docker.*

---

## 9. Deployment Challenge  

Although the backend services were running, the Timesketch web interface could not be accessed. The connection to localhost failed, likely due to Docker networking issues or compatibility limitations with macOS.

This highlights a real-world challenge in incident response, where tools may not always function as expected due to environment constraints.

*Figure 5. Timesketch web interface connection failure.*

---

## 10. Limitations  

- Timesketch web interface was not accessible  
- Full timeline reconstruction could not be completed  
- Analysis relied mainly on Wireshark network data  

---

## 11. Conclusion  

This project successfully identified suspicious network activity and key Indicators of Compromise. Through Wireshark analysis, it was possible to detect DNS queries, outbound connections, and encrypted communication that indicate potential malicious behavior.

Although the full timeline reconstruction could not be completed due to technical limitations, the project demonstrates how network traffic analysis can be used to detect threats and support incident response.

Future work would include completing the timeline reconstruction using log2timeline and Timesketch for deeper forensic analysis.

---

## 12. Project Structure  

  
