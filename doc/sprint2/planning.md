RCOMP 2021-2022 Project - Sprint 2 planning
===========================================
### Sprint master: 1201386 ###

# 1. Sprint's backlog #
| Task | Task Description                                                                                                                                                                                                 |
|------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|T.2.1 | Development of a layer two and layer three Packet Tracer simulation for building one, encompassing the campus backbone. Integration of every member's Packet Tracer simulations into a single simulation.        |
|T.2.2 | Development of a layer two and layer three Packet Tracer simulation for building two, encompassing the campus backbone.                                                                                          |
|T.2.3 | Development of a layer two and layer three Packet Tracer simulation for building three, encompassing the campus backbone.                                                                                        |
|T.2.4 | Development of a layer two and layer three Packet Tracer simulation for building four, encompassing the campus backbone.                                                                                         |


# 2. Technical decisions and coordination #
* **Packet Tracer Version:** V 8.1.1

#### Devices naming
* **Routers:** [R][Router Number]_Building Number (Example: R3_B3)
* **Switches:** [Cross Connect Type][Switch Number]_Building Number (Example: CP1_B1)
* **PCs or Laptops:** PC|Laptop Number_Building Number (Example: PC1_B1)
* **Wireless Access Points:** WAP Number_Building Number (Example: WAP1_B1)
* **IP-phones:** IPphone number_Building Number (Example: ipPhone1_B2)

#### VLAN database
* **Range of VLAN IDs used:** 240 – 270

Campus range: 240 - 270

| Building    | Vlan Id Range |
| ----------- | -----------   |
| 1 + Backbone|  240 - 245    |
| 2           |  246 - 250	  |
| 3           |  251 - 255	  |
| 4           |  256 - 260	  |

| ID da VLAN | Nome da VLAN  |
|------------|---------------|
|240         |backbone       |
|241         |b1groundfloor  |
|242         |b1floorone     |
|243         |b1wifi         |
|244         |b1dmz          |
|245         |b1voip         |
|246         |b2groundfloor  |
|247         |b2floorone     |
|248         |b2wifi         |
|249         |b2dmz          |
|250         |b2voip         |
|251         |b3groundfloor  |
|252         |b3floorone     |
|253         |b3wifi         |
|254         |b3dmz          |
|255         |b3voip         |
|256         |b4groundfloor  |
|257         |b4floorone     |
|258         |b4wifi         |
|259         |b4dmz          |
|260         |b4voip         |

####   VTP Domain
* **VTP Domain:** rc22deg1

#### IPv4 network

| Building    | Nodes  |IPv4 Networks    | 
|-------------|--------|-----------------|
|1 + Backbone | 520    |172.16.200.0/22  |
|2            | 219    |172.16.204.0/24  |
|3            | 188    |172.16.205.0/24  |
|4            | 175    |172.16.206.0/24  |


# 3. Subtasks assignment #
* 1200720 - Development of a layer two and layer three Packet Tracer simulation for building three, encompassing the campus backbone.
* 1201239 - Development of a layer two and layer three Packet Tracer simulation for building two, encompassing the campus backbone.
* 1201382 - Development of a layer two and layer three Packet Tracer simulation for building four, encompassing the campus backbone.
* 1201386 - Development of a layer two and layer three Packet Tracer simulation for building one, encompassing the campus backbone. Integration of every member's Packet Tracer simulations into a single simulation.
  

