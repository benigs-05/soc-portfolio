
Components of Snort: 
1. Packet Decoder  - collects and prepares packet for preprocessing
2. Pre-processors - arranges and modifies the packets for the detection engine
3. Detection Engine - component that processes, dissects, and analyzes packets 
4. Logging and Alerting - 
5. Outputs and Plugins - output integration (alerts -> mysql)

# Snort Rules 
1. Community rules - free ruleset 
2. Registered rules - free (requires registration)
3. Subscriber rules - paid (requires subscription) Updated twice a week T TH


# Scope and Detection (Rule Paths)

HOME_NET - what we are protecting - 'any' or '192.168.10.1/24'
EXTERNAL_NET - 'any' OR '!$HOME_NET'
RULE_PATH - hardcoded rule path - /etc/snort/rules
SO_RULE_PATH - registered and subscriber rules $RULE_PATH/so_rules
PREPROC_RULE_PATH - $RULE_PATH/plugin_rules

```
These are **variables in `snort.conf`. They tell Snort *which network you protect* and _where to load rule files_. They are not alerts or commands you run individually.
```

For example, if your protected network is `192.168.10.0/24`, a rule can say:

```
alert tcp $EXTERNAL_NET any -> $HOME_NET 80 (msg:"Traffic to web server"; sid:1000003; rev:1;)
```

The `$` means “use the value of this variable.”



# IPS MODE OF SNORT 

#config daq - IPS Mode selection - ex. afpacket
#config daq_mode - activating the inline mode - inline 
#config logdir - hardcoded default log path - /var/logs/snort 

```
Data Acquisition Modules (DAQs) are specialized libraries used for packet I/O, providing flexibility in processing packets. It is possible to select the DAQ type and mode for different purposes.
```

- PCAP: Default mode, known as Sniffer mode.
- Afpacket: Inline mode, known as IPS mode.
- Ipq: Inline mode on Linux by using Netfilter. It replaces the snort_inline patch.  
- Nfq: Inline mode on Linux.
- Ipfw: Inline on OpenBSD and FreeBSD by using divert sockets, with the pf and ipfw firewalls.
- Dump: Testing mode of inline and normalisation.

This is the part of `snort.conf` that decides **which rule files Snort loads**.

```
# site-specific rules             → Just a comment/section label
include $RULE_PATH/local.rules    → Load your local.rules file
#include .../example.rules        → Commented out; do not load this file
```

