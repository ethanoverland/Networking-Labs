# Two-Site Network with FortiGate Firewalls and a Site-to-Site VPN
### Scenario

A small company has a headquarters and a branch office. HQ has users and servers on separate VLANs, and the branch has a small user network. Both sites reach the internet through an ISP, and you need to connect them securely, control what traffic is allowed, and keep routing dynamic so the network can grow.
---

### 1. Network Foundation
 - VLANs
    - HQ
       - 10 - Users
       - 20 - Servers
       - 99 - Management
     - Branch
	     - 10 - Users
	     - 99 - Management
 - IP Scheme
	 - HQ - Users
		 - 10.1.10.0/24
	 - HQ - Servers
		 - 10.1.20.0/24
	 - HQ - Management
		 - 10.1.99.0/24
	 - Branch - Users
		 - 10.2.10.0/24
	 - Branch - Management
		 - 10.2.99.0/24
 - Basic Routes
---
### 2. FortiGate FW Policy
- 
---
### 3. Site to Site VPN
- 
---
### 4. Dynamic Routing
- 
---
### 5. Break/Fix
- 
---
### 6. Lessons Learned
- 
---
