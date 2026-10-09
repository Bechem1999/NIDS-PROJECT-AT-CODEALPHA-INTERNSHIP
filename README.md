# 🛡️ Network Intrusion Detection System (NIDS)

![CodeAlpha](https://img.shields.io/badge/Internship-CodeAlpha-blue)
![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-red)
![Snort](https://img.shields.io/badge/Snort-3.12.2.0-4B0082)
![Kali Linux](https://img.shields.io/badge/Platform-Kali%20Linux-557C94?logo=kalilinux&logoColor=white)
![Networking](https://img.shields.io/badge/Focus-Network%20Security-orange)
![IDS](https://img.shields.io/badge/Technology-NIDS-green)
![Status](https://img.shields.io/badge/Status-Completed-success)
![Ethical](https://img.shields.io/badge/Purpose-Educational%20%7C%20Authorized-lightgrey)

---

## 📌 Project Overview

This project was developed as part of the **CodeAlpha Cyber Security Internship**, under **Task 4: Network Intrusion Detection System (NIDS)**.

The objective was to set up a network-based Intrusion Detection System capable of monitoring network traffic, identifying suspicious activity through configured detection rules, and generating alerts when matching traffic is detected.

For this project, **Snort 3.12.2.0** was deployed on **Kali Linux** and configured to monitor network traffic through the active network interface.

A custom ICMP detection rule was created and tested using controlled network traffic generated within the authorized laboratory environment.

The project successfully demonstrated the complete basic IDS workflow:

```text
Network Traffic
      ↓
     eth0
      ↓
   Snort 3
      ↓
 Detection Rules
      ↓
 Traffic Analysis
      ↓
 IDS Alert
      ↓
```

# 🎯 Project Objectives
The main objectives of this project were to:
- Set up a network-based Intrusion Detection System.
- Configure Snort for network traffic monitoring.
- Identify the active network interface.
- Create a custom detection rule.
- Monitor network traffic for suspicious activity.
- Generate controlled test traffic.
- Detect ICMP traffic using a custom rule.
- Generate and analyze IDS alerts.
- Demonstrate basic security response and investigation.
- Document the complete implementation process.
 Security Investigation

| Tool / Technology | Purpose |
|---|---|
| **Snort 3.12.2.0** | Network Intrusion Detection |
| **Kali Linux** | Cybersecurity testing environment |
| **Linux Terminal** | Configuration and monitoring |
| **ICMP / Ping** | Controlled test traffic |
| **Git & GitHub** | Version control and documentation |

# 💻 System Environment
Operating System : Kali Linux
IDS              : Snort 3.12.2.0
Network Interface: eth0
Kali IP Address  : 10.0.0.3
Gateway          : 10.0.0.1
Network          : 10.0.0.0/24

# 🔎 Network Configuration
The active network interface was identified using:
ip addr
and:
ip route
The active interface was:
eth0

The network configuration identified during the project was:
IP Address : 10.0.0.3
Gateway    : 10.0.0.1
Network    : 10.0.0.0/24

# ⚙️ Snort Configuration
The main Snort 3 configuration file used in the project was:

/etc/snort/snort.lua

A backup of the original configuration was created before making project changes:

/etc/snort/snort.lua.backup

This was done to preserve the original configuration and provide a recovery point during testing.

# 📂 Snort Rules
The Snort rules directory was located at:
/etc/snort/rules/

The custom detection rule was placed in:
/etc/snort/rules/local.rules

# 🚨 Custom IDS Detection Rule

The custom Intrusion Detection System (IDS) rule was developed using Snort 3 to detect ICMP traffic within the authorized test environment.

The rule was saved in the following file:

```text
/etc/snort/rules/local.rules
```

## Custom Rule

```text
alert icmp any any -> any any (msg:"CODEALPHA ICMP TRAFFIC DETECTED"; sid:1000001; rev:1;)
```

### Rule Explanation

- **`alert`**: Generates an alert when the rule matches traffic.
- **`icmp`**: Specifies the protocol to detect.
- **`any any -> any any`**: Matches ICMP traffic between any source and destination. The port fields are not meaningful for ICMP.
- **`msg`**: Defines the alert message.
- **`sid:1000001`**: Identifies the custom Snort rule.
- **`rev:1`**: Specifies the rule revision.

## 🧪 Configuration Testing

Before starting the IDS, the Snort configuration and custom rule were validated using:

```bash
sudo snort -c /etc/snort/snort.lua \
-R /etc/snort/rules/local.rules \
-T
```

### Validation Result

The configuration test completed successfully, displaying:

```text
Snort successfully validated the configuration (with 0 warnings).
```

This confirmed that Snort could load the configuration and custom detection rule without configuration warnings.

## 📡 Network Monitoring

Snort was started on the active network interface, `eth0`, using the following command:

```bash
sudo snort -c /etc/snort/snort.lua \
-R /etc/snort/rules/local.rules \
-i eth0 \
-A alert_fast
```

### Command Explanation

- **`-c`**: Specifies the Snort configuration file.
- **`-R`**: Loads the custom detection rules.
- **`-i eth0`**: Specifies the network interface to monitor.
- **`-A alert_fast`**: Displays alerts in a concise format.

The IDS remained active while test traffic was generated from another terminal.

## 🧪 Controlled ICMP Traffic Test

To verify that the custom rule worked, controlled ICMP traffic was generated toward the configured network gateway.

The command used was:

```bash
ping -c 4 10.0.0.1
```

### Ping Test Result

The test produced the following result:

```text
4 packets transmitted
4 packets received
0% packet loss
```

This confirmed that the gateway responded to the ICMP test traffic.

## 🚨 IDS Detection Result

While the ping test was running, Snort detected the ICMP traffic and generated alerts matching the custom rule.

### Example Alert

```text
[1:1000001:1] "CODEALPHA ICMP TRAFFIC DETECTED"
```

The detected traffic included:

```text
{ICMP} 10.0.0.2 -> 10.0.0.1
```

### Detection Summary

| Test Component | Result |
|---|---|
| Snort installation | Successful |
| Configuration validation | Successful |
| Custom rule loading | Successful |
| Network interface monitoring | Successful |
| ICMP traffic generation | Successful |
| Custom rule matching | Successful |
| IDS alert generation | Successful |

# 🔄 Detection Workflow
The complete detection process can be summarized as:

        ICMP Traffic
              │
              ▼
        Network Interface
             eth0
              │
              ▼
          Snort 3
              │
              ▼
        Custom Rule
        SID 1000001
              │
              ▼
       Rule Match Detected
              │
              ▼
        IDS Alert Generated
              │
              ▼
     Security Investigation


  #   📊 Alert Analysis
The generated alert demonstrated that:
- Network traffic was successfully captured.
- Snort was actively monitoring the network interface.
- The custom ICMP rule was loaded.
- The rule successfully matched the test traffic.
- Snort generated an identifiable security alert.
- The alert could be used by a security analyst for further investigation.

  #  📚 Learning Outcomes
This project provided practical experience in:
- Network traffic monitoring
- Intrusion Detection Systems
- Snort 3
- IDS rule development
- ICMP traffic analysis
- Network interfaces
- Linux networking
- Security alerts
- Security event investigation
- IDS configuration
- Cybersecurity documentation
- GitHub project management

# 💡 Key Lessons Learned
One of the most important lessons from this project was that an IDS does not simply "watch the network."
It depends on well-defined detection rules to identify traffic patterns that deserve attention.
The project demonstrated the relationship between:

Network Traffic
       +
Detection Rules
       ↓
Security Events
       ↓
Alerts
       ↓
Investigation
       ↓
Security Response

# 🔐 Ethical and Legal Considerations
This project was developed strictly for:
- Educational purposes
- Cybersecurity training
- Authorized testing
- Controlled laboratory experimentation
The traffic used for testing was generated within an authorized environment.
The project should not be used to monitor, scan, attack, or interfere with networks or systems without explicit authorization.

# 👨🏽‍💻 Author

ATEMLEFAC NKAFU BECHEM 
Cybersecurity Engineer

LinkedIn: https://www.linkedin.com/in/atemlefac-nkafu-bechem-179987248

CodeAlpha Cyber Security Internship
