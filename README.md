---
# Fortigate Cyber Threat Intel

This repository provides a compact Cyber Threat Intelligence (CTI) feed for Fortigate Firewalls. Powered by AI/ML reinforcement learning, it delivers a minimal list of malicious IP addresses that blocks 60–70% of attacks. The small size ensures compatibility with most Fortigate models and uses minimal CPU resources, making it an efficient security solution for your network. This is "Security for the 99%"



### Script Contribution

*Contributed by:* 
UAS.com.ph
---

### Prerequisites

- Download the `WatchDogBlocklist-current.csv` file to your desktop.
- If needed, rename the file to `WatchDogBlocklist-current.csv`. Rename it to [blocklist-addresses.conf]
- Then Upload the file to your Fortigate firewall.
- Check for Limitations. For example on a FortiGate 400F:
--Maximum 5,000 address objects
--Maximum 600 IPs per address group
---

---

### Installation

Import the blocklist file into your Fortigate Firewall using the following command:

```shell
execute batch-script tftp blocklist-addresses.conf

```

---

### Firewall Rules

Add the following firewall filter rules to drop connections from IPs listed in the WatchDogBlocklist:

```plaintext
config firewall policy
edit 0
    set name "Deny_WAN_Attempts"
    set srcintf "wan1"              # adjust if different
    set dstintf "wan1"
    set srcaddr "Blocked_IP_Group_1" "Blocked_IP_Group2"
    set dstaddr "all"
    set action deny
    set schedule "always"
    set service "ALL"
    set logtraffic enable           # Optional: disable if you want less logging
next
end

```

You can verify and monitor with this command (Or enable hitcount in GUI:
Policy & Objects > Firewall Policy > Columns > Hit Count
) : 
```plaintext
diagnose firewall iprope policy list
```
---

Please help improve the effectiveness by alerting us to false positives and false negatives.

---


