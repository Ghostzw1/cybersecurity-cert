# Course 3 — Connect and Protect: Networks and Network Security

**Coverage:** covered according to reported study progress. **Document type:** newly prepared AI-assisted revision summary. The examples are illustrative, not captured traffic or a completed network investigation.

## 1. Architecture and communication

A network connects devices so they can exchange data. A LAN covers a local environment; a WAN connects over wider areas. A switch commonly forwards frames within a local network, while a router forwards packets between networks. An access point supports wireless connections. A firewall applies rules to traffic crossing its enforcement point.

The models below help locate a problem rather than describing every implementation perfectly:

| TCP/IP model | Related OSI layers | Questions to ask |
|---|---|---|
| Application | Application, presentation, session | What service or protocol is being used? |
| Transport | Transport | Which ports and transport behavior are involved? |
| Internet | Network | What are the source, destination, and route? |
| Network access | Data link, physical | Can the local devices communicate over the link? |

Encapsulation adds information at successive layers so data can travel and be interpreted. TCP supports an ordered byte stream with reliability mechanisms. UDP sends datagrams without TCP's delivery and ordering guarantees; an application can implement its own reliability where needed.

An IP address identifies an interface for network communication. A subnet prefix describes the network portion of an address. A MAC address is used in local link-layer communication. Ports help distinguish transport endpoints; a port number alone does not establish that traffic is benign.

## 2. Network operations and protections

| Protocol or mechanism | Purpose | Security question |
|---|---|---|
| DNS | Resolve names and other DNS records | Is the query going to an expected resolver, and does the answer make sense? |
| DHCP | Supply network configuration to clients | Is the configuration supplied by an authorized server? |
| HTTPS | HTTP protected using TLS | Is the certificate valid for the intended service? |
| SSH | Encrypted remote access | Who may connect, and how is access authenticated and logged? |
| ICMP | Network control and error messages | Does the pattern fit normal troubleshooting or unexpected activity? |
| VPN | Protect traffic across a tunnel | Which traffic is covered, where does the tunnel end, and who can access it? |

Subnetting and segmentation can separate systems with different trust requirements. Access rules are still needed between segments. A proxy acts on behalf of a client or service; its role depends on the design. Wireless protection includes appropriate encryption, authentication, and separation of guest and business access.

Cloud networking still needs access control, monitoring, and secure configuration. Responsibility is shared between the provider and customer according to the service model; moving a workload does not remove responsibility for its data and permissions.

## 3. Intrusion and traffic analysis

- **DoS and DDoS:** attempts to disrupt availability, with distributed attacks using multiple sources. A traffic spike can also be legitimate demand, so investigate context.
- **Packet sniffing:** observing network traffic. Authorized captures support troubleshooting; unauthorized access may expose information.
- **Spoofing:** presenting a false identity or address. An address in a packet should not be treated as conclusive proof of a person's identity.
- **On-path attacks:** interfering with communication between parties. Authentication and encryption help protect a connection, but endpoints and trust configuration still matter.

Packet captures and logs answer different questions. A capture contains packets observed at a particular point; a log describes events that a device or application chose to record. Capture location, filters, encryption, and missing data limit what an analyst can conclude.

**Original worked reasoning example:** A browser cannot reach a service. First identify whether name resolution succeeds. If it does, examine reachability and connection behavior before blaming the application. Repeated connection attempts without a response can have several explanations, including filtering, routing problems, or an unavailable destination. Correlate with another source before calling it an attack.

Tools such as tcpdump and Wireshark support packet analysis. A useful report states the time range, source, relevant addresses and protocols, observation, interpretation, and limits. It should not infer a payload's contents when encryption or capture limits prevent seeing them.

## 4. Hardening

Hardening reduces unnecessary exposure and makes systems easier to operate securely. Examples include patching, removing unused services, restricting administrative access, using strong authentication, separating networks, maintaining logs, and testing backups.

For brute-force attempts, consider multi-factor authentication, rate controls, monitoring, and appropriate account policies. Lockout rules need care because an attacker may deliberately trigger them to disrupt access.

A recommendation should connect an observed issue to a control and a verification step:

| Fictional issue | Proposed control | How to check it |
|---|---|---|
| Guest devices can reach an administration interface | Separate guest access and restrict the management path | Test allowed and denied connections from the appropriate segments |
| An unused remote service is exposed | Disable it through an approved change | Check listening services and external reachability afterward |
| Security logs are not available centrally | Configure suitable log collection and retention | Generate an authorized test event and confirm it arrives with a usable timestamp |

These are revision examples, not findings from a real organization. An operational change should have an owner, a maintenance plan where needed, and a way to restore service if the change causes a problem.

**Course reference:** [Networks and Network Security](https://www.coursera.org/learn/networks-and-network-security). [TCP specification](https://www.rfc-editor.org/rfc/rfc9293.html) and [UDP specification](https://www.rfc-editor.org/rfc/rfc768.html) provide protocol detail. See [LABS.md](../LABS.md) for the course analysis activities awaiting personal artifacts.
