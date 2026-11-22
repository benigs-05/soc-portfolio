


![Screenshot](../../../assets/images/pasted-image-20260917113013.png)





![Screenshot](../../../assets/images/pasted-image-20260917113045.png)



Alert (Type of action)- IDS 
Reject (Type of action)- IPS


Actions for rules:
1. Alert - generate and log 
2. Log 
3. Drop - block and log the packet 
4. Reject - block the packet, log it, and terminate the packet session 

Protocols: 
1. TCP
2. UDP
3. ICMP
4. IP

# For IP 


![Screenshot](../../../assets/images/pasted-image-20260917113455.png)


# For Ports 


![Screenshot](../../../assets/images/pasted-image-20260917113523.png)



Direction 

-> source to destination
<> bidirectional 

# Rules options 


![Screenshot](../../../assets/images/pasted-image-20260917113804.png)





# Payload options within rules 



![Screenshot](../../../assets/images/pasted-image-20260917113921.png)



for fast_pattern, it checks the initial rule and if it's there it checks the rest of the rule 

```
GET found + www found     → This rule can alert
GET found + no www        → This rule does not alert
No GET                    → Snort skips this rule quickly
```

# Non-Payload Data Rule Options 



Once a rule is created, it should be in a local rules in "local.rules" where it is located in /etc/snort/rules/local.rules

for editing rules 
```
sudo gedit /etc/snort/rules/local.rules
```


