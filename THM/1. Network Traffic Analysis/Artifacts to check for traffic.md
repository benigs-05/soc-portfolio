1. DNS Queries - **Source IP**(tells us what device internally is trying to make that request), **Destination IP**, **Domain** trying to contact, **Timestamps**(Correlation of events)  
2. DNS Queries and Replies (So the content itself) - helps us determine the nature of the connection 
3. Check records since this can be a vector to send commands 

We can monitor the Application header. We can get the domain, the directory. And the response can also provide that


**IPs, Ports and Flags**

First SYN - for establishing connection
"My starting sequence is 0, can receive data this size (64240), and segments to be (1460) "
```
Ethernet frame
└── IP packet
    └── TCP segment
        └── HTTP data
```
**TCP segment**

Contains TCP information:

- source port
- destination port
- sequence number
- acknowledgment number
- TCP flags: SYN, ACK, FIN, RST, PSH
- window size
- TCP payload/data
**IP packet**

Contains IP information:

- source IP
- destination IP
- TTL
- protocol field, like TCP or UDP
- fragmentation info
**Ethernet frame**

Contains local network delivery info:

- source MAC
- destination MAC
- EtherType
- frame check sequence


At packet 6, a different IP tried to hijack the connection by guessing the Seq number, and even injecting data given that len =20 
To successfully inject into a TCP session, the attacker needs to know or guess:

- source IP
- destination IP
- source port
- destination port
- current sequence number
- current acknowledgment number
- timing/window

If the attacker is **on-path**, they can observe the traffic and learn those values.

Firewall logs 

For this packets (Rules - TCP data (Which is Len) [dependent on the value of the data], and SYN/FIN [1] consumes space)
1st packet  - sender initiates a connection 


	 1st line's whole frame size is **74**, so it includes the IP, TCP headers, Application
	 -can contain Seq values that can point to session hijacking. Not because it's a high number but because of the context of it. 
	 - Length column points to the whole packet size. So in the first part, it's 74 bytes. 
	 - Len = x is the actual size of the Application Data  
	 - Win is flow control 
	 - MSS (Maximum Segment Size) - Largest TCP data chunk (segments, not packet) - maximum size of the application data - both sides negotiate for this limit
	**Seq**

> “The number of the first byte I am sending.”

**Ack**

> “The next byte I expect from you.”

And two special flags consume sequence numbers:

- `SYN` consumes `1`
- `FIN` consumes `1`
**Tools for Inspecting Packet**
**VirustTotal** - for domains and IP 