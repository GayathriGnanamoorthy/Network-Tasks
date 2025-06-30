#  Network Traffic Using Wireshark

## 1. Install Wireshark
- **Version:** 4.4.7
- ![image](https://github.com/user-attachments/assets/6d461745-b6f1-4c0c-baa4-664bd578102f)


## 2. Start Capturing on Active Network Interface
- **Interface Used:** Wi-Fi

## 3. Generate Traffic
- **Action:** Browsed the following website:  
  [https://github.security.telekom.com/2022/04/honeypot-tpot-22.04-released.html#download-iso-image](https://github.security.telekom.com/2022/04/honeypot-tpot-22.04-released.html#download-iso-image)
![image](https://github.com/user-attachments/assets/fbadfea9-5cc3-4a2d-9e56-815b79058897)

## 4. Stop Capture
- **Capture Duration:** Approximately 1 minute

## 5. Apply Protocol Filters
- Filtered protocols for inspection: `http`, `dns`, `tcp`, etc.
![image](https://github.com/user-attachments/assets/9932827f-ad59-4eed-87f8-bdad3a5f61f3)
![image](https://github.com/user-attachments/assets/b0b27abd-d16d-45c9-b7d8-5606bd6f6b91)
![image](https://github.com/user-attachments/assets/4b923ed6-0b59-430a-8495-422c220a09a1)

## 6. Identified Protocols in Capture
1. **TCP** – Transmission Control Protocol  
2. **ARP** – Address Resolution Protocol  
3. **mDNS** – Multicast Domain Name System  
4. **ICMPv6** – Internet Control Message Protocol version 6  
5. **HTTP** – HyperText Transfer Protocol  
6. **SSDP** – Simple Service Discovery Protocol

## 7. Export Capture
- **Exported File:** `task5.pcapng`

## 8. Summary of Findings and Packet Details

1. The DNS response in Frame 3036 was a standard query reply from IP `172.17.10.8` to `10.11.137.76` using UDP port 53.  
2. The DNS query was successfully processed with no errors (`0x8180`), but it returned no answer records.  
3. The transaction had one question and zero answers, authority, or additional records.  
4. The round-trip time for the DNS response was approximately 2.6 milliseconds.  
5. In Frame 11097, an HTTP GET request was sent from `10.11.137.76` to `23.15.147.118` on TCP port 80.  
6. The request was for a certificate revocation list (CRL) file: `/DigiCertGlobalRootG2.crl`.  
7. It included headers for cache control, host identification (`crl3.digicert.com`), and conditional fetch via `If-Modified-Since`.  
8. The user-agent indicates the request came from Microsoft's CryptoAPI, typically used for certificate validation.  
9. Frame 11108 shows the server responded with HTTP status code `304 Not Modified`.  
10. This indicates the CRL file had not changed, and the client could continue using its cached version.

---
