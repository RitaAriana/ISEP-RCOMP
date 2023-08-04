RCOMP 2021-2022 Project - Sprint 3 planning
===========================================
### Sprint master: 1201382 ###
(This file is to be created/edited by the sprint master only)

# 1. Sprint's backlog #
Considering the previous sprint, the team is now required continue working on the regarding building in order to
adapt the static routing into a dynamic routing. For this process, the OSPF will be the protocol used.

| Task | Task Description                                                                                                                                                                                                 |
|------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|T.3.1 | Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 1.      |
|T.3.2 | Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 2. Final integration of each member’s Packet Tracer simulation into a single simulation. |
|T.3.3 | Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 3.                                                                                       |
|T.3.4 | Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 4.                                                                                      |


# 2. Technical decisions and coordination #
In this section, all technical decisions taken in the planning meeting should be mentioned. 		

-   All member used Cisco Packet Tracer version 8.1.1.

-   VTP domain name must be rc22deg1.

-   Devices naming convention follows the rule "DeviceName"-"BuildingName"-"Floor" i.e.(ICC-B2-F0).

-   The main output is the Packet Tracer simulation file for the corresponding building, it should be named BuildingN.pkt, with N being the number which identifies the building.

-	The **OSPF area ids** are:
     - Backbone: 0
     - Building 1: 1
     - Building 2: 2
     - Building 3: 3
     - Building 4: 4


-	The **VoIP prefixes** are:
     - Building 1: 1...
     
     - Building 2: 2...
     
     - Building 3: 3...
     
     -Building 4: 4...


-	The highest level DNS domain will be part of Building 1, naming **rcomp-21-22-de-g1**.
     It will be used as if it was the DNS root domain.

-	The other DNS domains will be created locally in each building, naming **building-X.rcomp-21-22-de-g1**.
     The letter *X* will identify the building's number.

-	In each building, all DNS servers will have the unqualified DNA name as **ns**.
     While Building 1 will have **ns.rcomp-21-22-de-g1**, the others will have **ns.building-X.rcomp-21-22-de-g1**.

-	The **IPv4 node address** for each DNS name server are:
     - **Building 1 - ns.rcomp-21-22-de-g1**
        B1-DMZ: 172.16.202.0

	 - **Building 2 - ns.building-2.rcomp-21-22-de-g2**
		B2-DMZ: 172.16.204.224
		
	 - **Building 3 - ns.building-3.rcomp-21-22-de-g2**
		B3-DMZ: 172.16.205.192
		
	 - **Building 4 - ns.building-4.rcomp-21-22-de-g2**
		B4-DMZ: 172.16.206.224
	 

# 3. Subtasks assignment #

#### Example: ####


* 1200720 - Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 3. 
* 1201239 - Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 2. Final integration of each member’s Packet Tracer simulation into a single simulation.
* 1201382 - Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 4.
* 1201386 - Update the campus.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 1.
  
