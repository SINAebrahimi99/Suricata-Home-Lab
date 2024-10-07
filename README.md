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

before write our rule lets breakdown the suricata rules format :

## Suricata Rules Format

Suricata uses specific rules to define patterns of traffic that should be monitored, alerted on, or blocked.

note! : Snort and Suricata rules structure are the same and you can use your rule for both tools (especially for basic detection scenarios).

every suricata rule is made of 3 main part : Action, Header, Rule Option

``` (Action) [protocol] [source_ip] [source_port] -> [destination_ip] [destination_port] (options) ```

![image](https://github.com/user-attachments/assets/7f1a6c3d-3750-4223-97bd-8fa8251d834c)

this is an example rule, in this rule the red part is Action, the green part is Header and the blue part is Option

now i will create my rule file :

![image](https://github.com/user-attachments/assets/1388a0bd-8db6-41ae-9953-b84fe436ba12)

this is the simple rule that i wrote :
![rule](https://github.com/user-attachments/assets/168b880c-b342-487d-b4b5-59766c4a0b80)

lets break it down :

`alert` =  an alert should be generated when the rule matches, this is Action part

`ICMP` = Internet Control Message Protocol 

`any any -> any any` = every src_ip and src_port to every dest_ip and dest_port

`msg:"ICMP Ping Detected"` = This message will be logged when the rule triggers

`itype:8` = ICMP type that the rule is looking for

`sid:1000001` = rule sid

`rev:1` = the revision number of the rule. If the rule is updated or modified, this number should be incremented

-------------------------------------------------------------------------------------------------------------------------------------------

now the next step is to tell suricata to use this rule file too alongside the suricata local rules :

lets open the suricata conf file : (```/etc/suricata/suricata.yaml```)

![image](https://github.com/user-attachments/assets/902d686b-ba44-4b69-9ffd-ccee475a3752)

now i add sina.rules to this part :

![image](https://github.com/user-attachments/assets/e6351694-7248-4d18-85fa-76458c2a0fbc)


## Run Suricata 

at first restart suricata to make sure that changes are on board and then run suricata

![image](https://github.com/user-attachments/assets/b1063bf2-9ff3-486e-8982-f00f4d2b2f64)



``` -c /etc/suricata/suricata.yaml ``` to ensure that we verity our rules 

``` -i enp0s3 -v ``` to select enp0s3 interface in verbose mode 


![image](https://github.com/user-attachments/assets/6716ac94-59f3-4c4a-86d9-67fa78fdfc9b)

now Suricata is running !


## Trigger an alert 

i will use ping command to send ICMP packet to a well known DNS server like 8.8.8.8 :

![image](https://github.com/user-attachments/assets/b25789eb-246c-42f2-8a2a-d5735ba14a53)

now lets check the log file, suricata log file path is `/var/log/suricata/eve.json` :

![image](https://github.com/user-attachments/assets/109e6f77-987d-4193-ba80-0bcbe1ae4699)

as you can see the log file and alert of sending ICMP packet to 8.8.8.8 is here !










