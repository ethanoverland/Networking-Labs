# Campus Layer 2 Build: Requirements

**Platform:** Cisco CML | **Status:** Planning

## Scenario

A growing company is deploying a new network for a single building. Management has handed over the requirements below. The network must tolerate hardware and link failures, protect itself from user-introduced problems, and be managed securely.

## Scope

- Two distribution switches and three access switches
- Every access switch connects to both distribution switches
- Endpoints fall into five traffic groups: **staff, voice, servers, guest, and management**
- Upstream connectivity only needs to be minimal; the focus is Layer 2 and first-hop redundancy at the distribution layer

## Requirements

| ID | Requirement | Acceptance criteria |
|----|-------------|---------------------|
| **REQ-01** | Traffic groups must be segmented from one another at Layer 2, and guest traffic must be isolated from internal resources. | Each group sits in its own VLAN; a guest endpoint cannot reach staff, server, or management resources. |
| **REQ-02** | The network must survive the loss of any single uplink or either distribution switch. | Continuous traffic from an endpoint recovers after each failure without manual intervention. |
| **REQ-03** | Both uplinks from each access switch must carry traffic under normal conditions, and the STP root for each VLAN must be deliberately chosen, not left to chance. | Root and secondary root are explicitly set per VLAN, split across the two distribution switches; access switches show both uplinks in use across VLANs. |
| **REQ-04** | Each VLAN must have a redundant default gateway that fails over automatically and whose active role aligns with the STP root for that VLAN. | Gateway fails over when the active distribution switch is lost; Layer 2 and Layer 3 primary roles match per VLAN. |
| **REQ-05** | End-user ports must come up immediately but must be protected from rogue switches and unexpected BPDUs. | A switch connected to an end-user port is blocked and the port is disabled. |
| **REQ-06** | Only authorized devices may use end-user ports. Each port must allow one PC plus one IP phone, and violations must be handled safely. | A third MAC address on a port triggers the defined violation action; legitimate devices are unaffected. |
| **REQ-07** | Users must not be able to run a rogue DHCP server or spoof IP/MAC bindings. | A rogue DHCP server on a user port hands out no leases; spoofed ARP traffic is dropped. |
| **REQ-08** | Broadcast, multicast, and unknown-unicast storms on access ports must be rate limited so they cannot take down the network. | A generated storm is throttled and does not disrupt other VLANs or switches. |
| **REQ-09** | Unused ports must be administratively disabled and placed in a non-routable VLAN. | An audit of all switches shows no unused port that is enabled or in a user-facing VLAN. |
| **REQ-10** | Trunks must not negotiate dynamically, must use a non-default native VLAN, and must carry only the VLANs required. | An audit of every trunk shows negotiation disabled, a non-default native VLAN matching on both ends, and a pruned allowed-VLAN list. |
| **REQ-11** | All switches must be managed only via SSH from the management VLAN, with Telnet disabled, authenticated access enforced, accurate time, and centralized logging. | Telnet is refused; SSH works from the management VLAN only; time is synchronized; logs carry timestamps and are sent to a log destination. |
| **REQ-12** | Ports that are disabled by a protection feature must recover automatically after a defined interval. | A triggered err-disable recovers on its own after the configured timer. |

## Deliverables

- Design, build, and verification of every requirement above
- Evidence that each acceptance criterion is met
- Documented failure testing for the redundancy and protection requirements