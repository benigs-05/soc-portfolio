# Class B 

128.0.0.0 - 191.255.255.255

**Private IP Address**
172.16.0.0 - 172.31.0.0

In class B:
- The Network portion is the first 2 octet **172.16**.0.1
- The Host portion is the last 2 octet 172.16.**0.1**
- A class B is a /16
- It has a subnet mask **255.255**.0.0
- It creates more host but less networks in compared to a Class C network 

Example of a class B network:
Network ID: **172.16.0.0**
Broadcast ID/Address: **172.16.255.255**
Subnet mask: **255.255.0.0**
CIDR Notation: **/16**

Changing all the IP address from our previous LAN
<img width="756" height="754" alt="image" src="https://github.com/user-attachments/assets/5204403f-4acd-4f7a-afe9-0aa41b81c50a" />

<img width="630" height="338" alt="image" src="https://github.com/user-attachments/assets/e9241bce-0ee7-4b71-a600-400561396cc0" />

We get this network with four hosts: 
PC0 - 172.16.0.1
PC1 - 172.16.0.2
PC2 - 172.16.0.3
PC3 - 172.16.0.4

<img width="171" height="71" alt="image" src="https://github.com/user-attachments/assets/5fef826b-968a-40af-a6bd-08dc89ea1d80" />

We can use the "Add Simple PDU (Protocol Data Unit)" tool to allow to quickly test connectivity between 2 devices by sending a ping.

We can do this by:

1. Clicking the Icon.
2. Selecting a source Device.
3. Selecting a destination device.
4. Packet tracer will automatically create a test packet.

<img width="617" height="89" alt="image" src="https://github.com/user-attachments/assets/20a3c252-a9a6-48c1-aa7f-f6e008917b18" />

This shows a successful connectivity between the hosts as they belong to the same network. 

Let's now try changing the last 2 octet of PC0, from 172.16.0.1 - > **172.16.1.1**

<img width="700" height="337" alt="image" src="https://github.com/user-attachments/assets/c47508e1-3183-48e3-996c-35300955d1e7" />

- Then try pinging the host PC1
<img width="682" height="205" alt="image" src="https://github.com/user-attachments/assets/9f4c907e-ce7e-4b65-902c-37f5db65cc4a" />

- This shows that it can still ping it since we're only changing the host portion, but changing the first 2 octet will make it so that it can't communicate to a different host, assuming that the network that it's changed to is a different network that it originally had. 
- Let's try changing PC0 to 172.16.1.1 to **172.17.1.1** and test connectivity. 

<img width="702" height="266" alt="image" src="https://github.com/user-attachments/assets/53c72af1-743f-47c8-8199-47f479dba3ad" />

<img width="663" height="185" alt="image" src="https://github.com/user-attachments/assets/60795feb-3cde-4158-846b-75a2bd7c2b28" />

- With that change, it doesn't let us ping PC1 again since we're on a different network this time. PC0 is now part of the network **172.17.0.0/16**




