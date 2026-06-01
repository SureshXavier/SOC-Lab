# SOC-Lab
Building a Splunk SOC Lab: Windows Universal Forwarder, Deployment Server, Syslog, and Firewall Monitoring
Overview

To strengthen my cybersecurity and SIEM skills, I built a complete Splunk-based SOC lab environment using a Windows endpoint and a Kali Linux virtual machine. The objective was to collect, forward, and monitor security logs from multiple sources using Splunk components commonly found in enterprise environments.

Lab Architecture
Windows Endpoint
├── Splunk Universal Forwarder
├── Windows Event Logs
└── Windows Firewall Logs
          │
          ▼
Kali Linux VM
├── Splunk Enterprise
├── Heavy Forwarder
├── Deployment Server
├── Search Head
└── rsyslog Server
Technologies Used
Splunk Enterprise
Splunk Universal Forwarder (UF)
Deployment Server
Heavy Forwarder (HF)
rsyslog
Windows Event Viewer
Windows Defender Firewall
Kali Linux
VMware Workstation
Environment Setup
Windows Endpoint

Installed and configured Splunk Universal Forwarder to collect and forward security logs to the Splunk server running on Kali Linux.

Forwarding Configuration

Configured the Universal Forwarder to send data to the Splunk receiving port:

192.168.252.128:9997
Deployment Server Configuration

Configured the Universal Forwarder as a Deployment Client and connected it to:

192.168.252.128:8089

This allows centralized management of forwarders from the Splunk Deployment Server.

Kali Linux Splunk Server

Configured a single Splunk Enterprise instance to perform multiple roles:

Search Head

Used for searching, analyzing, and visualizing ingested data.

Heavy Forwarder

Configured a receiving port to accept logs from forwarders:

Port: 9997
Deployment Server

Enabled Deployment Server functionality to centrally manage Splunk Universal Forwarders.

Management port:

Port: 8089
Windows Log Collection

Configured the Universal Forwarder to collect key Windows Event Logs.

Application Logs
[WinEventLog://Application]
disabled = 0

Captures:

Application events
Software updates
Service notifications
Security product status events
Security Logs
[WinEventLog://Security]
disabled = 0

Captures:

Logon and logoff activity
Authentication events
Account management
Security auditing events
System Logs
[WinEventLog://System]
disabled = 0

Captures:

Driver events
Service state changes
Operating system events
Hardware-related logs
Windows Firewall Monitoring

Enabled Windows Defender Firewall logging to collect network activity.

Configured:

Log Dropped Packets = Yes
Log Successful Connections = Yes

Firewall log location:

C:\Windows\System32\LogFiles\Firewall\pfirewall.log

Configured Splunk Universal Forwarder to monitor the firewall log:

[monitor://C:\Windows\System32\LogFiles\Firewall\pfirewall.log]
disabled = 0
sourcetype = windows_firewall
Firewall Visibility

Collected information such as:

Allowed connections
Dropped packets
Source IP addresses
Destination IP addresses
Protocol information
Network activity trends
Syslog Infrastructure

Installed and configured rsyslog on Kali Linux.

Enabled Syslog Services

Configured both UDP and TCP Syslog listeners:

UDP 514
TCP 514

This allows the Splunk server to receive logs from:

Linux servers
Firewalls
Routers
Switches
Network appliances
Remote Log Storage

Configured rsyslog to store logs from remote devices in dedicated directories for easier management and ingestion into Splunk.

Example structure:

/var/log/remote/
├── firewall01
├── linux01
├── router01
└── switch01
Data Flow
Windows Endpoint Logs
Windows Event Logs
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Heavy Forwarder
        │
        ▼
Splunk Search Head
Firewall Logs
Windows Firewall
        │
        ▼
pfirewall.log
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Splunk Heavy Forwarder
        │
        ▼
Splunk Search Head
Syslog Events
Linux / Network Devices
        │
        ▼
rsyslog (Port 514)
        │
        ▼
Splunk Enterprise
        │
        ▼
Search and Analysis
Skills Demonstrated
Splunk Administration
Universal Forwarder deployment
Deployment Server configuration
Heavy Forwarder configuration
Data onboarding
Input management
Log Management
Windows Event Log collection
Firewall log monitoring
Syslog collection
Centralized log aggregation
Security Monitoring
Authentication monitoring
System activity monitoring
Network traffic monitoring
Firewall event analysis
Linux Administration
Splunk installation on Kali Linux
Service management
Port configuration
rsyslog configuration
Outcome

Successfully built a functional Splunk SOC lab capable of collecting and centralizing:

Windows Application Logs
Windows Security Logs
Windows System Logs
Windows Firewall Logs
Syslog Events

The lab simulates a real-world enterprise logging architecture and provides hands-on experience with SIEM administration, log ingestion, security monitoring, and centralized log management using Splunk.

Resume Project Description (Short Version)

Built a Splunk-based SOC lab using Kali Linux and Windows, configuring Splunk Enterprise as a Search Head, Heavy Forwarder, and Deployment Server. Implemented centralized log collection for Windows Application, Security, System, Firewall, and Syslog events using Splunk Universal Forwarder and rsyslog, enabling end-to-end security monitoring and log analysis.
