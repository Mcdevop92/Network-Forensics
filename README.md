# Network-Forensics-Lab 🔍🔐

Set up a home lab environment using Kali Linux within VirtualBox to practice network forensics and incident response. Analyzed network traffic with Wireshark, identified a rogue user through DHCP and security logs, and successfully correlated the activity to a specific host device, demonstrating proficiency in forensic investigation.

# Scenario:
You’ve been hired to the Security Operations Center of the company Corporan Carriers, LLC. Office to help track down the employee behind some nefarious activity. On April 19th, 2023 at 12:50PM an employee at Corporan Carriers, LLC. sent their deepest darkest secrets to everyone within the company. Or did they? This employee claims that someone else at the company is impersonating them, and your job is to hunt for who this rogue user is.

## Goals 🎯

* Set up a home lab environment with Kali Linux for network forensics.
* Use Wireshark to analyze a .pcap file and identify suspicious activity.
* Correlate the identified IP address with a host device using DHCP logs.
* Determine the responsible user by analyzing security logs.

## Installation 🏗️

* **VirtualBox** --> [Download](https://www.virtualbox.org/wiki/Downloads)
  - Installation Video: [YouTube](https://www.youtube.com/watch?v=omQ6mLF2zYA&t=0s)

* **Kali Linux** -->  [Download](https://www.kali.org/get-kali/#kali-platforms)
  - Installation Video: [YouTube](https://www.youtube.com/watch?v=vnX1NaF4K-Q)

* **Wireshark** -->  [Download](https://www.wireshark.org/download.html)
  - Installation Video:  [YouTube] (https://www.youtube.com/watch?v=4_7A8Ikp5Cc&t=21s)

## Getting Started 🤓

### 0 - Download the lab files:
  1. SMTP.pcap
  2. DHCP.txt
  3. Security_log.rtf

### 1 - Find the IP Address
* Open up the .pcap file in Wireshark 📄
  ![image](https://github.com/user-attachments/assets/7d81aaa2-d14f-435b-bd19-a44b05419f68)

Note: there are 60 packets, so use the display filter to sort out the unnecessary ones. Hits: we are looking for an email --> <b>smtp<b/>

You should get something like this:
![image](https://github.com/user-attachments/assets/f1c1d9a7-ffd0-4de3-9b04-5559988841b5)

With the applied filter we should see a more filtered out list and the ones that remain all use Simple Mail Transfer Protocol. We are very close but still to apply a more specify filter to find our target. ...... Hint: use the "FROM" filter 

you should get something like this: 
![image](https://github.com/user-attachments/assets/21698138-33b5-40d2-9bb2-a3d394d1ddf1)

Now thart we have filtered out a single packet, we should see the info column that the mail is coming from the compromised user's account, but what we really want is the IP address: <b>10.10.1.4</b> because this tells us where within the network the rogue user performed these actions, and by taking a look at our DHCP log, we can match this information up to the name of the host computer that the rogue user acted from as well.
Start by analyzing the .pcap file:

### 2 - Correlate to the Host Computer
Use the DHCP log file to match the found IP address. DCHP (Dynamic Host Configuration Protocol) is how a server assigns IP addresses to hosts/devices on the network.
* Open the DHCP log
* Identify the six events that occurred right before 12:50PM and check whose IP address <b>10.10.1.4</b> belongs to
    * hint: locate the event at 12:11:27PM
You should stop here and continue with the investigation by yourself but.... if you still need help continue in the next line
------------------------------------------------------------------------------------------------------------------------------------

We should see that the event at 12:11:27PM does just what we were looking for and assigned the IP address used by the rogue user from our .pcap file to the host device <b>USER2</b>. Amazing! We now know which computer the rogue user acted from, and by taking a look at the security log from the host device, we should be able to determine which employee at the company was logged in during that time!

### 3 - Analyze the Security Log
* Open the Security Log file with any word-processing program. (🪟 Microsoft Word, 🪟 WordPad, 🍏 Pages, 🍏 TextEdit, etc)
* Take a moment to read through the logs. What do you notice?
The first two were a logon/logoff session on host computer USER1, and the corresponding user section states this was by Jane Doe. The last two, however, were a logon/logoff session on host computer USER2.
* Find the corresponding user for these logs, and we should have our answer!
Not only is USER2 the host device we suspected, but if we take a look at the duration of time in which John Doe was logged in, this perfectly overlaps with the time in which the sensitive emails were sent! We’ve finally discovered our culprit, and John will certainly have some explaining to do.
