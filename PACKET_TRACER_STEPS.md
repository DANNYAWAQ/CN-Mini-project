# Step-by-step Cisco Packet Tracer implementation (novice level)

## Prerequisite
Install and open Cisco Packet Tracer. The project is built inside Packet Tracer, not by executing Python code. Device labels and interface names might vary slightly by release.

## A. Place and connect devices (approximately 5 minutes)
1. Add **1 Switches > 2960**, **2 End Devices > Server**, and **2 End Devices > PC**.
2. Rename using Config > Global > Display Name or labels: `Switch0`, `DNS_Server`, `Web_Server`, `CSE_PC`, `Faculty_PC`.
3. With Connections > Copper Straight-Through, make four links:
   - DNS_Server FastEthernet0 → Switch0 FastEthernet0/1
   - Web_Server FastEthernet0 → Switch0 FastEthernet0/2
   - CSE_PC FastEthernet0 → Switch0 FastEthernet0/3
   - Faculty_PC FastEthernet0 → Switch0 FastEthernet0/4
4. Wait for switch links to become green. Router is not needed.

## B. Assign the server IP addresses
5. DNS_Server > Desktop > IP Configuration > Static: IP `192.168.10.2`, Subnet Mask `255.255.255.0`.
6. Web_Server > Desktop > IP Configuration > Static: IP `192.168.10.3`, Subnet Mask `255.255.255.0`.
7. Leave default gateway empty on both servers.

## C. Turn on DNS and add the A record
8. DNS_Server > Services > DNS > DNS Service **On**.
9. Enter: Name `www.cse.test`, Type `A Record`, Address `192.168.10.3`, then press **Add**.
10. Confirm the new record is visible in the DNS record table.

## D. Host the departmental webpage
11. Web_Server > Services > HTTP > HTTP **On**.
12. Choose `index.html` from the file list and click Edit.
13. Open `website/index.html` on your laptop, copy all text, paste into the simulator editor and Save.
14. Keep the default HTTP service on TCP port 80.

## E. Configure PCs
15. CSE_PC > Desktop > IP Configuration > Static:
    - IP `192.168.10.10`
    - Subnet Mask `255.255.255.0`
    - DNS Server `192.168.10.2`
    - Default Gateway **blank**
16. Faculty_PC > Desktop > IP Configuration > Static:
    - IP `192.168.10.11`
    - Subnet Mask `255.255.255.0`
    - DNS Server `192.168.10.2`
    - Default Gateway **blank**

## F. Verify normal operation
17. CSE_PC > Desktop > Command Prompt. Run `ping 192.168.10.2` and `ping 192.168.10.3`.
18. Run `ping www.cse.test`. It should resolve to 192.168.10.3 and then ping the website host.
19. CSE_PC > Desktop > Web Browser > `http://192.168.10.3` > Go. Department page should load.
20. Open `http://www.cse.test` > Go. Same page should load after DNS resolution.
21. Repeat named-domain browsing from Faculty_PC.
22. First pings sometimes time out during ARP learning; repeat after ARP completes. If a ping fails, inspect cables and addresses.

## G. Watch packets move (Simulation mode)
23. At the bottom right, switch **Realtime → Simulation**.
24. Use **Edit Filters** to focus on DNS, HTTP, TCP, ARP, and ICMP (enable only the types you want to view).
25. Clear or reset the event list as needed. Open CSE_PC's browser and enter `http://www.cse.test`.
26. Press **Capture/Forward** several times (or **Auto Capture/Play**) and observe DNS query → DNS reply → TCP/HTTP exchange. Click a colored PDU/event to inspect OSI information.
27. DNS responses may be cached, so you may need to restart the simulation or use a fresh PC/session to see a DNS query again. Do not assume every website load generates a new query.

## H. Deliberate failure tests (restore after each)
### Failure 1: DNS service stopped
28. DNS_Server > Services > DNS > **Off**. Try accessing domain name from a client without a cached entry; resolution should fail.
29. Compare direct IP `http://192.168.10.3` which should still work. Turn DNS service **On** again.

### Failure 2: Wrong A record
30. Temporarily change `www.cse.test` A record to `192.168.10.99` using the DNS records list (delete old record/add wrong record as required).
31. Domain resolves to the wrong address, so the webpage should not load; direct IP should still work. Restore `192.168.10.3`.

### Failure 3: HTTP disabled
32. Web_Server > Services > HTTP > **Off**. DNS resolution/ping can still succeed, but loading the webpage fails.
33. Turn HTTP **On** again.

### Failure 4: Physical link disconnected
34. Use delete connection (or temporarily disable server interface) to disconnect Web_Server from Switch0. Web access and ping should fail.
35. Reconnect and repeat tests; it should recover once the link is up and learning settles.

## I. Collect metrics
36. Log the four ping responses and RTT figures, if Packet Tracer provides numeric RTT values. Record any packet losses.
37. Run e.g. 5 browser trials for both URL-by-IP and URL-by-name, count successes; repeat with DNS and HTTP failures.
38. Record DNS/HTTP PDU counts and the simulation timestamp values shown in your version if available; they are **simulated** timing indicators, not real network latency.
39. Populate `TEST_REPORT.md` with *your observed* data, screenshots and Packet Tracer version.

## J. Save
40. File > Save As > `mini_dns_website.pkt` inside the project folder. Save screenshots separately if desired.

## Troubleshooting
- IP works, name fails: check client DNS IP, DNS On, spelling and A record.
- Neither works: check subnet mask, IP, physical link, server status, ARP learning.
- Ping by name works, browser fails: check HTTP On and web page saved correctly.
- DNS still works immediately after turning it Off: cached response may exist; test on a fresh client or restart simulation.
- UI differs: use logical-equivalent Services > DNS and Services > HTTP settings.
