# 🧪 Wireshark Lab – DNS Tunneling Traffic Analysis

## 🎯 Objective
Simulate and detect suspicious DNS traffic (DNS TXT tunneling) in a controlled Windows lab environment using Wireshark.

---

## ⚙️ Lab Setup
- **Host OS:** Windows 10/11  
- **Tools:** Wireshark (with Npcap), nslookup / PowerShell Resolve-DnsName  
- **Traffic Generated:**  
  - Normal DNS queries (`google.com`, `microsoft.com`)  
  - Simulated suspicious TXT queries with abnormally long labels (`attacker-example.test`)  

---

## 🔍 Steps Performed
1. Installed Wireshark + Npcap on Windows.  
2. Captured traffic on the Wi-Fi adapter while running DNS queries.  
3. Generated baseline traffic:  
   ```powershell
   nslookup google.com
   
## Simulated tunneling traffic:
Powershell Code:
nslookup -type=txt "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa.attacker-example.test" 8.8.8.8
(also tested PowerShell loops for repeated queries)

## Applied Wireshark filters:

1. dns
2. dns && dns.qry.type == 16 (TXT queries only)
3. udp.port == 53 (standard DNS over UDP)

Inspected suspicious packets in Packet Details.

Followed UDP stream to observe payloads of repeated TXT queries.

## 📸 Screenshots
**DNS traffic overview with filter applied**
![DNS Traffic](https://github.com/antwoinecollins/Wireshark-Lab-DNS-Tunneling-Traffic-Analysis/blob/main/UDP-Follow.Sanitized2025-09-17%20235125.png)

**Suspicious TXT query expanded in Packet Details**
![Suspicious TXT](https://github.com/antwoinecollins/Wireshark-Lab-DNS-Tunneling-Traffic-Analysis/blob/main/TXT-Record_Sanitized2025-09-17%20234933.png)


## 📊 Findings
- Normal DNS: Short A/AAAA queries with clean responses.
- Suspicious DNS: TXT queries containing very long labels (e.g., aaaaaaaa...attacker-example.test).
- Indicators: Long subdomain labels + repeated TXT queries = typical DNS tunneling / exfiltration pattern.

## 🛡️ Mitigation
- Enable DNS query logging and forward to SIEM.
- Alert on anomalous TXT record lengths and repeated subdomain patterns.
- Block or sinkhole suspicious domains at the resolver.
- Escalate anomalies to Tier 2 SOC for deeper investigation.


## ✅ Notes
- attacker-example.test was used as a safe placeholder domain.
- This lab demonstrates the detection workflow, not a live attack.
