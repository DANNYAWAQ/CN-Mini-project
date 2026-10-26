# Topic 23: Mini DNS Server with Local Website Hosting

**Implementation:** Cisco Packet Tracer simulation (built-in DNS + HTTP server), with a small HTML departmental webpage. No Python or custom GUI required.

> Important scope note: This configures Packet Tracer's built-in DNS service; it does **not** program a DNS server from scratch. Confirm with your professor that simulation-based implementation is accepted. A working `.pkt` simulation file must be saved from Packet Tracer by the student; none is included in this archive.

## Problem statement
Computer users find numerical IP addresses difficult to remember. A local DNS service can map a memorable departmental name to the IP of an internal website, making the website accessible to PCs in a campus LAN.

## Objectives
1. Design a small departmental LAN.
2. Configure a DNS A record for `www.cse.test`.
3. Host a departmental webpage on an HTTP server.
4. Verify website access by IP and DNS name.
5. Simulate DNS/HTTP packets and demonstrate deliberate DNS and HTTP failures.
6. Collect measured results for ping RTT, resolution/website success and recovery time.

## Devices and topology
- 1 × Cisco 2960 switch (Switch0)
- 2 × Server-PT (DNS_Server and Web_Server)
- 2 × PC-PT (CSE_PC and Faculty_PC)
- 4 × Copper Straight-Through cables, each endpoint to a switch FastEthernet port
- All hosts within `192.168.10.0/24`; no router required for local connectivity

See `topology.svg` and `PACKET_TRACER_STEPS.md`.

## IP plan
| Device | IPv4 | Mask | DNS (for clients) | Switch port |
|---|---|---|---|---|
| DNS_Server | 192.168.10.2 | 255.255.255.0 | n/a | Fa0/1 |
| Web_Server | 192.168.10.3 | 255.255.255.0 | n/a | Fa0/2 |
| CSE_PC | 192.168.10.10 | 255.255.255.0 | 192.168.10.2 | Fa0/3 |
| Faculty_PC | 192.168.10.11 | 255.255.255.0 | 192.168.10.2 | Fa0/4 |

No default gateway is needed, because all devices are on the same subnet and no router is present. Leave gateway blank. These are private lab IPs, not public website addresses.

## DNS entry
- DNS service: On
- Record type: A
- Name: `www.cse.test`
- Address: `192.168.10.3`

The reserved `.test` domain is appropriate for experiments; this name only resolves for our configured clients within this simulation.

## Web service
- HTTP service: On
- `index.html`: paste text from `website/index.html` into the Web_Server > Services > HTTP > index.html editor; save.
- Browser URL: `http://www.cse.test`.

## Protocol/message format design
This is a protocol-configuration project, not a newly designed wire protocol.

1. Client uses ARP to find the local DNS server's MAC when necessary.
2. Client sends a DNS query for `www.cse.test` (normally UDP destination port 53).
3. DNS server replies with an A record containing `192.168.10.3`.
4. Client establishes a TCP connection to the web server on port 80.
5. Client sends an HTTP GET request for `/`; web server returns the HTML page.
6. ICMP Echo Request/Reply packets are used for ping testing.

Expected logical DNS question: `QNAME=www.cse.test; QTYPE=A; QCLASS=IN`.
Expected logical answer: `www.cse.test A 192.168.10.3`.
Expected HTTP request: `GET / HTTP/1.1` (the simulator may display HTTP specifics differently).

## Files
- `PACKET_TRACER_STEPS.md`: click-by-click simulator build and test instructions
- `topology.svg`: architecture diagram
- `website/index.html`: copy/paste local webpage source code
- `TEST_REPORT.md`: normal/failure cases, raw results table and formulas
- `DEMO_AND_VIVA.md`: 5-minute presentation and viva answers
- `README.md`: report-ready overview and concepts

## What to submit
1. Your saved `mini_dns_website.pkt` from Packet Tracer (create it following the steps).
2. The project folder or ZIP containing HTML, diagram, README, tests and demonstration notes.
3. Screenshots of a working browser, DNS table, Simulation mode event list, and failure tests.
4. Measured results in `TEST_REPORT.md`. Never present placeholder values as measurements.

## Limitations and upgrades
- This is a single-LAN simulation, not a public DNS service, domain registration or internet-hosted website.
- No cross-subnet routing, automatic DHCP, real-world DNS recursion, or TLS.
- Packet Tracer emulates selected protocols and features; measured simulation times should not be claimed as real-world network latency.
- Possible upgrades: add a router and second subnet, multiple domain records, optional DHCP, or a basic Python DNS implementation if custom coding is demanded.
