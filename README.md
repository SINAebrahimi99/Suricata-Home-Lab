# Suricata-Home-Lab
Set up Suricata to act as NIDS and create some rules and review the output log


## About 
Suricata is a Network Intrusion Detection System (actually, its a multi functional cybersecurity tool, but Im focusing on this part for now).

Suricata monitors network traffic coming in and out of the network. It uses a set of detection rules to look for malicious patterns within the traffic and detect any potential attempts to compromise the network.

 In case of any detection, it will create an alert and send that alert to the user.

![Diagram](https://github.com/user-attachments/assets/505f8fbe-cb01-47be-8011-00250ec89203)

In this diagram, Suricata is being used in NIPS mode, working inline in the network flow from the internet to the internal network. In NIDS mode, we use a SPAN port instead .

## Set up Suricata

after creating out machine and getting ip from our home router (in Bridged mod) now its time to intsall Suricata.

to do that we use : 
```bash
sudo apt install suricata
```
![install suricata](https://github.com/user-attachments/assets/62807f4a-972f-4b93-8e01-750b3f24e15b)

then we must update the rules that come with suricata :
```bash
sudo suricata-update
```
![update rules](https://github.com/user-attachments/assets/f6a0f256-9bd4-4560-98bc-4105711f14b2)

## Create a Custom Rule

suricata default rule files path is ```/var/lib/suricata/rules/suricata```

lets take a look at it :

![image](https://github.com/user-attachments/assets/03c3e5bc-d2df-4f68-8fc6-89af6147c1da)


![cat rules](https://github.com/user-attachments/assets/f4d88b45-4d0a-409b-9f3a-e64ed3dd420d)


## Suricata Rules Format

Suricata uses specific rules to define patterns of traffic that should be monitored, alerted on, or blocked.

note! : Snort and Suricata rules structure are the same and you can use your rule for both tools (especially for basic detection scenarios).

every suricata rule is made of 3 main part : Action, Header, Rule Option

``` (Action) [protocol] [source_ip] [source_port] -> [destination_ip] [destination_port] (options) ```

![image](https://github.com/user-attachments/assets/7f1a6c3d-3750-4223-97bd-8fa8251d834c)

this is an example rule, in this rule the red part is Action, the green part is Header and the blue part is Option
















