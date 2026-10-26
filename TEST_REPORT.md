# Test report and performance measurements

**Student:** __________  **Date:** __________  **Packet Tracer version:** __________
**Note:** Fill in *observed* values after running the simulator. No numeric results in this template are fabricated.

## Test cases
| ID | Condition | Action | Expected behavior | Observed result | Pass/Fail |
|---|---|---|---|---|---|
| T1 | Normal | Ping DNS_Server at 192.168.10.2 | Successful replies | ______ | ____ |
| T2 | Normal | Ping Web_Server at 192.168.10.3 | Successful replies | ______ | ____ |
| T3 | Normal | Browse http://192.168.10.3 | Department page loads | ______ | ____ |
| T4 | Normal | Browse http://www.cse.test | DNS resolves; department page loads | ______ | ____ |
| T5 | Normal | Repeat on Faculty_PC | Website loads | ______ | ____ |
| T6 | DNS failure | Turn DNS Off; use fresh client/session | Name lookup fails, direct IP may work | ______ | ____ |
| T7 | Wrong mapping | Change A record to 192.168.10.99 | Domain fails to reach actual web host | ______ | ____ |
| T8 | HTTP failure | Turn HTTP Off | DNS/ping may work, browser fails | ______ | ____ |
| T9 | Cable failure | Disconnect Web_Server | Ping/HTTP fail; recover on reconnection | ______ | ____ |

## Packet-level verification (Simulation mode)
Capture and screenshot representative events: ARP, DNS query, DNS response, TCP connection (SYN/SYN-ACK/ACK when displayed), HTTP request and response. Packet Tracer does not require Wireshark for simulated internal traffic; this is simulator packet inspection.

## Raw trial log
| Trial | Client | Test (IP URL / name URL / ping) | DNS service | HTTP service | Success (1/0) | Reply count | Sent count | RTT values (ms if available) | Simulation time / event count (if available) |
|---|---|---|---|---|---|---|---|---|---|
| 1 | CSE_PC | Name URL | On | On | ___ | — | — | — | ____ |
| 2 | CSE_PC | IP URL | On | On | ___ | — | — | — | ____ |
| 3 | Faculty_PC | Name URL | On | On | ___ | — | — | — | ____ |
| 4 | CSE_PC | Name URL | Off | On | ___ | — | — | — | ____ |
| 5 | CSE_PC | IP URL | Off | On | ___ | — | — | — | ____ |

## Performance metrics (calculate from your observations)
1. **Ping packet loss (%)** = `(sent - received) / sent * 100`. Example calculation only: if 4 sent / 3 received, loss = 25%.
2. **Ping average RTT (ms)** = sum of individual successful reply RTTs / number of successful replies. Use reported average if detailed RTT is unavailable.
3. **DNS resolution success rate (%)** = successful name resolutions / attempted name resolutions * 100.
4. **Website access success rate (%)** = successful page loads / attempted page loads * 100.
5. **Service recovery time** = time between enabling DNS/HTTP or restoring a cable and first confirmed successful request. If only simulation event time is available, label it simulated time; otherwise measure with a stopwatch and note that manual actions influence this metric.
6. **Traffic observation:** number of DNS and HTTP events in Simulation mode under a comparable repeated procedure. Do not call simulator event count network throughput.

## Summary table
| Metric | Normal network | DNS Off | HTTP Off | Web link down |
|---|---|---|---|---|
| DNS resolution success rate | ____ | ____ | ____ | ____ |
| Website access success rate by name | ____ | ____ | ____ | ____ |
| Website access success rate by IP | ____ | ____ | ____ | ____ |
| Packet loss to Web_Server | ____ | ____ | ____ | ____ |
| Average ping RTT | ____ | ____ | ____ | ____ |
| Restoration / recovery time (if measured) | ____ | ____ | ____ | ____ |

## Results discussion prompts
- Did browsing by direct IP work when DNS failed? Why?
- Did turning off HTTP affect ping replies? Why not necessarily?
- Does first-contact ARP add packets / delay in simulation?
- What is Packet Tracer's limitation versus a real network?

**Screenshots:** topology, DNS A record, HTTP index page, successful browser, Simulation PDU/event view, DNS-off/browser failure, HTTP-off/browser failure.
