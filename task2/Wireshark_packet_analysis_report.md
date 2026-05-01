# Wireshark Traffic Analysis and Network Attack Demonstration Report

**Date:** May 01, 2026  
**Analyst:** KARRI NIKHILA


**Objective:** To capture and inspect common network protocols (HTTP, DNS, FTP), observe the risks of plaintext communication, and simulate a TCP SYN Flood Denial-of-Service (DoS) attack for traffic analysis.

---

## 1. Tools Used 🛠️

* **Wireshark:** Network packet analyzer used to capture and study traffic in real time.  
* **hping3:** Packet crafting tool used to simulate network attacks.  
* **Operating System:** Kali Linux (Virtual Machine environment).  

---

## 2. Methodology and Procedures

The practical activity was completed in three separate stages.

### ### Phase 1: Capturing Normal Network Traffic

1. **Start Packet Capture:**  
A live capture session was started in Wireshark on the active network interface (`eth0` or `ens33`).

2. **Generate Traffic:**  

* **DNS & HTTP:** A browser was used to visit a website such as `http://example.com` to generate DNS lookups and HTTP requests.  
* **FTP:** An FTP client connection was made to a public FTP server to generate FTP login and command traffic.  

3. **Apply Filters:**  
After stopping the capture, display filters were used to inspect each protocol separately:

* `dns` – Showed DNS query and response packets.  
* `http` – Displayed HTTP GET requests and server replies.  
* `ftp` – Revealed FTP command channel communication.  

---

### ### Phase 2: FTP Credential Inspection

1. **Objective:**  
To demonstrate the insecurity of unencrypted protocols.

2. **Procedure:**  

* The `ftp` filter was applied to the captured packets.  
* Authentication packets containing `USER` and `PASS` commands were located.  
* Wireshark’s **Follow TCP Stream** feature was used.  

3. **Findings:**  

The entire FTP session was visible in readable text, including the username and password. This confirmed that FTP does not encrypt credentials and is unsafe on modern networks.

---

### ### Phase 3: SYN Flood Attack Simulation

1. **Objective:**  
To simulate a Denial-of-Service attack and identify its packet pattern.

2. **Attack Execution:**  

A new Wireshark capture was started with the following display filter:

```text
tcp.flags.syn == 1 and tcp.flags.ack == 0
```
```text 
sudo hping3 -S --flood -V 10.0.2.15
```


3. **Traffic Analysis**:

The Wireshark capture clearly showed:

1. A very large number of TCP SYN packets.

2. Continuous connection requests to one target IP.

3. Multiple randomized source IP addresses.

4. No completed TCP handshakes.

These characteristics are commonly seen in SYN Flood attacks.

 ## 3 : **Conclusion and Key Takeaways**

This task successfully demonstrated packet analysis techniques and network attack behavior.

1.   **Unencrypted Protocols are Dangerous**:
   
   FTP transmits usernames and passwords in plaintext, making it highly insecure. Secure alternatives such as SFTP or FTPS should be used.

3.  **SYN Flood Attacks Have Clear Signatures**:
   
Large volumes of SYN packets from changing source addresses to one destination are strong indicators of a DoS attack.

5.  **Wireshark is a Powerful Security Tool**:
   
Wireshark helps analysts troubleshoot networks, detect attacks, and inspect suspicious traffic in detail.

7.  **Traffic Monitoring is Essential**:
   
Regular packet inspection can help organizations detect threats before they cause major damage.





























