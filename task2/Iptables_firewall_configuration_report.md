# Report: Firewall Security Configuration using iptables

**Date:** May 01, 2026  
**Analyst:** KARRI NIKHILA

**Objective:** To implement a secure firewall using `iptables`, apply a default block policy, allow trusted services, and automatically detect repeated scan attempts.

---

## 1. Tools Used 🛠️

* **iptables:** Linux firewall tool used to manage packet filtering rules.
* **nmap:** Used to test firewall behavior through scanning.
* **netcat:** Used for connectivity and port checks.

---

## 2. Methodology and Procedures

The firewall setup was completed in several phases.

### ### Phase 1: Applying a Default Secure Policy

Initially, the system accepted all incoming traffic. To improve security, the firewall was configured to deny traffic unless explicitly permitted.

1. **Set Default Policy to DROP:**  
All unsolicited incoming traffic was blocked by default.

2.  **Allow Established  Connections**:
Packets related to active sessions were allowed.
'
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT'


4. **Allow Loopback Traffic**:
Internal communication on localhost was permitted.
sudo iptables -A INPUT -i lo -j ACCEPT

5. **Allow SSH Access**:
Port 22 was opened for secure remote access.
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

This established a secure base firewall configuration.

### ### ### Phase 2: Port Scan Detection and Blocking

To defend against scanning activity, dynamic rules were created using the recent module.

1.**Flush Existing Rules**:
Old rules were removed before applying the new ruleset.
sudo iptables -F
sudo iptables -X
2.**Create Custom Chain**:
sudo iptables -N SCAN_BLOCK
3.**Redirect New TCP Requests**:
sudo iptables -A INPUT -p tcp --syn -j SCAN_BLOCK
4.**Detect Frequent Requests**:
If an IP sent more than 6 requests in 30 seconds, it was blocked.
sudo iptables -A SCAN_BLOCK -m recent --name ATTACKER --update --seconds 30 --hitcount 6 -j DROP
5.**Track New IP Addresses**:
sudo iptables -A SCAN_BLOCK -m recent --name ATTACKER --set -j ACCEPT

This allowed automatic blocking of suspicious scanning attempts.

### ### Phase 3: Verification using nmap

Firewall rules were tested by scanning the local machine.

Command Used:
nmap -sS 127.0.0.1
Observed Result:
At first, the scan detected some ports normally. After repeated probes, packets were dropped and ports began showing as filtered, confirming successful detection.


### ### Phase 4: Cleanup and Restore Defaults

After testing, the firewall was reset to avoid network disruption.

sudo iptables -F
sudo iptables -X
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT

## 3. Conclusion and Key Takeaways

This exercise successfully demonstrated the implementation of an effective firewall policy using `iptables`.

1. **Default Deny Improves Security:**  
A default-deny approach is one of the safest firewall strategies. By blocking all incoming traffic unless specifically allowed, the system’s attack surface is significantly minimized.

2. **Dynamic Rules Increase Protection:**  
`iptables` is capable of more than simple port filtering. With modules such as `recent`, it can detect repeated suspicious connection attempts and automatically block potential port scans.

3. **Controlled Access is Essential:**  
Important services such as SSH can remain accessible while unnecessary traffic stays blocked, creating a balance between usability and security.

4. **Testing Validates Configuration:**  
Using tools like `nmap` is necessary to confirm that firewall rules are functioning correctly and providing the intended protection.

5. **Regular Maintenance Matters:**  
Firewall rules should be reviewed and updated regularly to adapt to changing network requirements and new security threats.
 
