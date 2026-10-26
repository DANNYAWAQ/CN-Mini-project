# Five-minute demonstration and viva

## 5-minute demonstration timeline
**0:00–0:45 Problem and goal.** "IP addresses are hard to remember. We use a local DNS server to resolve our department website's name to its IP address, and a local HTTP server to host the website."

**0:45–1:30 Topology and IPs.** Show Switch0, two Server-PTs, two PCs, all on 192.168.10.0/24. Explain why there is no router on one subnet.

**1:30–2:15 Configuration.** Open DNS_Server > Services > DNS and show `www.cse.test → 192.168.10.3`; then Web_Server > Services > HTTP and show saved `index.html`.

**2:15–3:15 Working demo.** On CSE_PC, first browse `http://192.168.10.3` and then `http://www.cse.test`. Open Faculty_PC and repeat by domain name.

**3:15–4:15 Packet flow and failure.** Switch to Simulation mode and observe DNS and HTTP events. Turn DNS Off and try the domain using a fresh client/session; show that direct IP still reaches the web server if HTTP is on. Restore DNS.

**4:15–5:00 Results and conclusion.** Show test report with actual counts and ping loss/RTT if available. "This models the relationship between DNS name resolution and HTTP website delivery on a LAN."

## Viva questions and concise answers
1. **What is DNS?** Domain Name System; it maps domain names to records such as IP addresses.
2. **Why is DNS useful?** Humans remember names more easily than IPs; mappings can change without changing the name users type.
3. **What is an A record?** A DNS record that maps a domain name to an IPv4 address.
4. **What is a DNS server?** A system that answers DNS queries from clients based on available records or other resolution mechanisms.
5. **What is HTTP?** Application protocol used to request and transfer web content.
6. **Which ports are involved?** DNS typically UDP 53, sometimes TCP 53; HTTP TCP 80.
7. **Why use a switch?** It connects Ethernet nodes and forwards frames by destination MAC address.
8. **Why no router?** All devices share the same subnet, so communication does not cross IP network boundaries.
9. **What does 192.168.10.0/24 mean?** 24 network-prefix bits; mask 255.255.255.0; ordinary host range 192.168.10.1–192.168.10.254.
10. **What happens if DNS is stopped?** New name resolution fails; the webpage might remain accessible by direct IP.
11. **What if HTTP is stopped but DNS works?** Name-to-IP resolution can succeed, but the website cannot be served over HTTP.
12. **Can ping a domain work with HTTP Off?** Yes, if DNS and ICMP connectivity still work.
13. **What does ICMP do?** Network diagnostic/control messaging; ping uses Echo Request and Echo Reply.
14. **What is ARP?** Resolves an IPv4 address to a link-layer MAC address on the local network.
15. **Why static server IPs?** DNS A records need stable target addresses unless records are kept updated.
16. **Why `.test`?** It is a reserved testing domain, not a registered public domain.
17. **Does the project provide internet DNS?** No, it simulates a configured local DNS service within one Packet Tracer LAN.
18. **Did you code DNS from scratch?** No; this is a Packet Tracer DNS/HTTP service configuration and simulation project. The webpage HTML is customized.
19. **What is Simulation mode?** Packet Tracer's view to inspect and step through supported packet events.
20. **What metrics did you collect?** Ping RTT/loss, successful name/website requests, and optionally simulated event or recovery timing.
21. **Difference between IP and domain?** IP addresses identify network endpoints/interfaces; domain names are human-readable identifiers mapped using DNS.
22. **What's a DNS query?** A client request asking for a record like an A record for a particular name.
23. **Why is Web_Server different from DNS_Server?** One answers name lookups and the other serves HTML; separating them clarifies each protocol.
24. **What if the wrong A record is used?** The client connects to the wrong IP or fails to connect.
25. **Future scope?** Router + second subnet, DHCP, backup DNS, larger records, HTTPS, and comparing resolution success under failures.

## Speak carefully
- Say "Packet Tracer simulation of a mini DNS service," not "I coded a full recursive DNS resolver."
- Packet Tracer's displayed times are simulated, not measurements of a real physical network.
- Do not claim Wireshark captured simulator-internal traffic unless you separately tested a real network.
