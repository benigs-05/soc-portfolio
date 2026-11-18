Can either be a HIDS or NIDS 

**Objectives**:
1. Overview of IPS/IDS
2. Snort Overview 
3. Writing IDS rules 
4. Detecting Intrusion with Snort 


Can be:
1. Signature-based
2. Behavior-based
3. Policy-based

Modes of Snort: 
1. Packet sniffer - captures traffic, doesn't analyze, more on observing (insights on network traffic)
2. Packet Logging Mode - Logs traffic as PCAP as well as the detections from it (deeper analysis)
3. NIDS mode - monitors traffic in real time and applies rule files to identify any match. Either knowledge-based or anomaly based 


# First Interaction with Snort 
```
snort -V
```
check if snort is installed 

```
snort -c /etc/snort/snort.conf -T
```
-c identifies configuration
-T tests the configuration


# Snort sniffer mode 
```
-v display the TCP/IP output in console [who is talking and how]
```

```
-d display the packet data [what data is inside]
```

```
-e display the link-layer headers [Which MAC address actually sent this frame?]
```

```
-X display the full packet details in hex [for inspecting the raw bytes of the entire captured packet] parang 'yong view sa wireshark when clicking packets 
```

```
-i defines the specific network interface to listen to
```

Can mix flags like:
```
sudo snort -v -i eth0
```

# Logger Mode 
```
-l logger mode, target log, and alert output directory [tells where to save]
```
Default output folder is /var/log/snort 
Default action is to dump as tcpdump format in /var/log/snort 

```
-K ASCII Log packets in ASCII format [human readable format]
```

```
-r reading option: review the logged events in snort 
```

```
-n specify the number of packets to be processed or read. Snort will stop after that number 
```

Examples: 
```
sudo snort -dev -l [packet sniffer + log]
```

has -d, -e, -v, and then -l 

For isolation 
- `sudo snort -r logname.log -X`
- `sudo snort -r logname.log icmp`
- `sudo snort -r logname.log tcp`
- `sudo snort -r logname.log 'udp and port 53'


# IDS/IPS Mode 

```
-N disable logging [don't save packet logs]
```
example:
```
sudo snort -c /etc/snort/snort.conf -i eth0 -N
```

`-N` disables **packet logging**. Snort can still inspect traffic and generate alerts; it just won’t save packet copies to its packet log. This is different from `-l`, which chooses _where_ logs go.

---
```
-D background mode [Run snort in the background]
```
example:
```
sudo snort -c /etc/snort/snort.conf -i eth0 -D
```

`-D` runs Snort as a **daemon**, meaning it continues in the background and gives you your terminal prompt back. It does _not_ mean “show data”; lowercase `-d` does that.

---

```
-A <mode> [choose how alerts are presented] 
```
example: 
```
sudo snort -c /etc/snort/snort.conf -i eth0 -A console
```

`-A` requires a mode after it. Here, `console` displays rule alerts in the terminal. Other alert formats include brief or more detailed output; available names vary between Snort 2 and 3
-cmg, basic header details with payload in hex and text format 
none: disabling alert 

fast - generates an alert file and a log (no console)
full - alert file + log (all possible information on the action)

none - doesn't generate an alert file, but generates a log file 

We can also user-defined rules 

# SNORT IPS MODE ACTIVATION
``
```
snort -c /etc/snort/snort.conf -q -Q --daq afpacket -i eth0:eth1 -A console
```

-Q-- daq afpacket 


# PCAP Investigation with Snort 

Parameters: 
```
-r/ --pcap-single- [read a signle pcap]
```

```
--pcap-list="" [read pcaps, separated by a space]
```

```
--pcap-show [show pcap name on console during processing]
```

Example commands: 
```
sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10
```

`-q` hides extra Snort messages, so alert focused 

```
sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console -n 10
```

reading multiple pcap files 

```
sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console --pcap-show
```

pcap shows separates it so that it's alerted under the pcap name 


```
sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-1.pcap
```

```
sudo                            Run with elevated permissions
-c /etc/snort/snort.conf        Load Snort's configuration and rules
-A full                         Write alerts in the detailed “full” format
-l .                            Put output files in the current directory (.)
-r mx-1.pcap                    Read packets from this PCAP
```



