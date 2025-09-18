# Wireshark Lab – DNS Tunneling Traffic Analysis  

## 🎯 Objective  
Simulate and detect suspicious DNS traffic in a controlled lab environment using Wireshark.  

## ⚙️ Lab Setup  
- **OS**: Kali Linux VM  
- **Tools**: Wireshark, nslookup  
- **Traffic Generated**: Normal and suspicious DNS queries  

## 🔍 Analysis Steps  
1. Captured live traffic with Wireshark.  
2. Applied filters (`dns`, `udp.port == 53`).  
3. Observed abnormally long TXT DNS records (potential tunneling).  
4. Followed UDP stream to analyze data exfiltration attempts.  

## 📊 Findings  
- Multiple long TXT DNS records detected.  
- Potential data exfiltration pattern (simulated).  
- Normal DNS queries had short, clean responses.  

## 🛡️ Mitigation  
- Block suspicious domains at DNS resolver.  
- Implement DNS logging/monitoring in SIEM.  
- Escalate to Tier 2 if repeated anomalies observed.  

## 📸 Screenshots  
![DNS Traffic](images/dns-capture.png)  
![Suspicious TXT Record](images/txt-record.png)  
