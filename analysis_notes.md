# Wireshark Analysis Notes

**Author:** Dhrumit Asari

## Capture Summary
- Interface: local lab interface
- Duration: > 2 minutes
- Filters used: http, dns, tcp

## Key Observations
1. HTTP traffic visible in cleartext — full request lines and headers readable.
2. DNS queries show domain names being resolved (also typically cleartext unless DoH/DoT is used).
3. TCP three-way handshake successfully identified and annotated in screenshots.
4. No production or third-party traffic was captured.

## Security Takeaway
Any sensitive information sent over HTTP can be read by anyone with access to the network path. Always prefer HTTPS and educate users about the risks of unencrypted protocols.
