# Suricata-Home-Lab
Set up Suricata to act as NIDS and create some rules and review the output log


## About 
Suricata is a Network Intrusion Detection System (actually, its a multi functional cybersecurity tool, but Im focusing on this part for now).

Suricata monitors network traffic coming in and out of the network. It uses a set of detection rules to look for malicious patterns within the traffic and detect any potential attempts to compromise the network.

 In case of any detection, it will create an alert and send that alert to the user.

<!--![Diagram](https://github.com/user-attachments/assets/505f8fbe-cb01-47be-8011-00250ec89203)-->

In this diagram, Suricata is being used in NIPS mode, working inline in the network flow from the internet to the internal network. In NIDS mode, we use a SPAN port instead .

## Set up Suricata

after creating out machine and getting ip from our home router (in Bridged mod) now its time to intsall Suricata.

to do that we use : 
```bash
sudo apt install suricata
```
