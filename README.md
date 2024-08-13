# Network-Forensics-Lab 🔍🔐

Set up a home lab environment using Kali Linux within VirtualBox to practice network forensics and incident response. Analyzed network traffic with Wireshark, identified a rogue user through DHCP and security logs, and successfully correlated the activity to a specific host device, demonstrating proficiency in forensic investigation.

## Installation 🏗️

* **VirtualBox** --> [Download](https://www.virtualbox.org/wiki/Downloads)
  - Installation Video: [YouTube](https://www.youtube.com/watch?v=omQ6mLF2zYA&t=0s)

* **Kali Linux** -->  [Download](https://www.kali.org/get-kali/#kali-platforms)
  - Installation Video: [YouTube](https://www.youtube.com/watch?v=vnX1NaF4K-Q)

* **Wireshark** -->  [Download](https://www.wireshark.org/download.html)
  - Installation Video: https://www.youtube.com/watch?v=4_7A8Ikp5Cc&t=21s

## Goals 🎯

* Set up a home lab environment with Kali Linux for network forensics.
* Use Wireshark to analyze a .pcap file and identify suspicious activity.
* Correlate the identified IP address with a host device using DHCP logs.
* Determine the responsible user by analyzing security logs.

## Getting Started 🤓

### 1 - Download the lab files:
  1. 

Start by analyzing the .pcap file:

* Open Wireshark and load the provided `SMTP.pcap` file.
* Use a display filter to focus on SMTP traffic:
  ```bash
  smtp
