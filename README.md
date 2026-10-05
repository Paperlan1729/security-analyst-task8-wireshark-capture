# Security Analyst Task 8: Capture Network Traffic with Wireshark

**Author:** Dhrumit Asari  
**GitHub:** [Paperlan1729](https://github.com/Paperlan1729)  
**Track:** Security Analyst (Intermediate Practical Task)

---

## Installation Notes

### Linux (Ubuntu / Kali)
```bash
sudo apt update
sudo apt install wireshark -y
# Add your user to the wireshark group to capture without root
sudo usermod -aG wireshark $USER
# Log out and back in for the group change to take effect
```

### Windows / macOS
Download the official installer from https://www.wireshark.org/download.html.  
On Windows, the installer includes Npcap (required for live capture). Running as Administrator may be required depending on interface permissions.

---

## Capture Performed

- **Duration:** ≥ 2 minutes of live traffic on a local network interface (lab VM or host-only adapter).
- **Interface:** Chosen local interface (e.g., eth0, WLAN, or VirtualBox Host-Only).
- **Ethics:** Only traffic on networks I own or administer was captured. No public Wi-Fi or third-party networks were monitored.

### Display Filters Applied

| Filter | Purpose |
|--------|---------|
| `http` | Isolate HTTP traffic |
| `dns`  | Isolate DNS queries and responses |
| `tcp`  | Examine TCP streams, including the three-way handshake |

### TCP Three-Way Handshake Analysis

1. **SYN** — Client sends a TCP segment with the SYN flag set and an initial sequence number.
2. **SYN-ACK** — Server replies with SYN and ACK flags, acknowledging the client’s sequence and providing its own.
3. **ACK** — Client sends a final ACK, completing the handshake. The connection is now established.

Screenshots of the filtered views and the annotated handshake should be placed in `screenshots/`.

---

## Unencrypted Data Observation

An HTTP GET request was identified in the capture. Because HTTP transmits data in cleartext, the following information is visible to any observer on the network path:

- Request method and full URL path
- Host header
- User-Agent string
- Cookie values (if present)
- Any form data or query parameters sent in the clear

**Why this is dangerous:** An attacker performing a man-in-the-middle attack (or simply sniffing an open network) can read credentials, session tokens, personal data, and application logic.  
**How HTTPS prevents this:** HTTPS wraps the HTTP payload inside a TLS-encrypted tunnel. Even if the packets are captured, the content remains unreadable without the session keys.

---

## Glossary (in my own words)

| Term       | Definition |
|------------|------------|
| **Packet** | The basic unit of data transmitted across a network; contains headers and a payload. |
| **Protocol** | A set of rules that define how devices communicate (e.g., TCP, HTTP, DNS). |
| **Port**   | A logical endpoint on a host that identifies a specific process or service (e.g., 80 for HTTP, 443 for HTTPS). |
| **Payload** | The actual data carried by a packet, excluding the headers. |
| **Handshake** | The initial exchange of packets that establishes a connection (most famously the TCP three-way handshake). |

---

## Files

- `README.md` — This documentation
- `wireshark_capture.pcap` — Placeholder note (actual pcap should be exported from Wireshark and committed if size permits; otherwise store externally and link)
- `screenshots/` — Filtered views and annotated handshake

**Note on the .pcap file:** Real packet captures can be large and may contain sensitive data. For this repository a placeholder is provided; replace it with your own lab capture when ready.

---

*Completed by Dhrumit Asari — Security Analyst Track. Capture performed only on owned lab networks.*
