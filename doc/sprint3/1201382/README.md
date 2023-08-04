RCOMP 2021-2022 Project - Sprint 3 - Member 1201382 folder
===========================================


### Building 4

-------------------------------------------------------------------
#### OSPF (Open Shortest Path First)

Static routes between buildings were eliminated, except for the default route connecting to the ISP
  (since without this route there would be no internet distribution across the campus).


- R0_B4 router configuration
    - **Router(config)#** router ospf 4
    - **Router(config)#** network 172.16.200.0 0.0.0.127 area 0
    - **Router(config)#** network 172.16.206.0 0.0.0.255 area 4
    

-------------------------------------------------------------------
#### HTTP Server

- A server was placed in the DMZ VLAN to take over the HTTP service.
- Added a building identifier to an HTML page.

![HTML.PNG](resources/webpage1.0.png)

![HTML.PNG](resources/webpage2.0.png)

-------------------------------------------------------------------

#### DHCPv4 Service

- The router in each building must be configured to provide a DHCPv4 service to all local networks excluding
  the DMZ networks and the backbone.

* Floor 0:
  - **Router(config)#** ip dhcp pool b4groundfloor
  - **Router(dhcp-config)#** network 172.16.206.192 255.255.255.224
  - **Router(dhcp-config)#** default-router 172.16.206.193
  - **Router(dhcp-config)#** dns-server 172.16.206.226
  - **Router(config)#** domain-name rcomp-21-22-de-g1

*Floor 1:
  - **Router(config)#** ip dhcp pool b4floorone
  - **Router(dhcp-config)#** network 172.16.206.128 255.255.255.192
  - **Router(dhcp-config)#** default-router 172.16.206.129
  - **Router(dhcp-config)#** dns-server 172.16.206.226
  - **Router(dhcp-config)#** domain-name rcomp-21-22-de-g1
  
* WiFi:
  - **Router(config)#** ip dhcp pool b4wifi
  - **Router(dhcp-config)#** network 172.16.206.0 255.255.255.128
  - **Router(dhcp-config)#** default-router 172.16.206.1
  - **Router(dhcp-config)#** dns-server 172.16.206.226
  - **Router(dhcp-config)#** domain-name rcomp-21-22-de-g1

* VoIP:
  - **Router(config)#** ip dhcp pool b4voip
  - **Router(dhcp-config)#** network 172.16.206.240 255.255.255.240
  - **Router(dhcp-config)#** default-router 172.16.206.241
  - **Router(dhcp-config)#** option 150 ip 172.16.206.241
  - **Router(dhcp-config)#** dns-server 172.16.206.226 
  - **Router(dhcp-config)#** domain-name rcomp-21-22-de-g1

* Gateway addresses have been deleted from the pool:
  - **Router(config)#** ip dhcp excluded-address 172.16.206.193
  - **Router(config)#** ip dhcp excluded-address 172.16.206.129
  - **Router(config)#** ip dhcp excluded-address 172.16.206.1
  - **Router(config)#** ip dhcp excluded-address 172.16.206.241


-------------------------------------------------------------------

#### VoIP Service

- On the ports of the switches connected to the phones, the respective voice vlan was activated, and the access vlan deactivated.

- Automatic phone registration and directory number assignment
  - **Router(config)#** telephony-service
  - **Router(config-telephony)#** auto-reg-ephone
  - **Router(config-telephony)#** ip source-address 172.16.206.241 port 2000
  - **Router(config-telephony)#** max-ephones 40
  - **Router(config-telephony)#** max-dn 40
  - **Router(config-telephony)#** auto assign 11 to 12
  - **Router(config)#** ephone-dn 11
  - **Router(config-ephone-dn)#** number 4000
  - **Router(config)#** ephone-dn 12
  - **Router(config-ephone-dn)#** number 4001


- Calls forwarding

  - dial-peer voice 1 voip
  - destination-pattern 1…
  - session target ipv4:172.16.200.1

  - dial-peer voice 2 voip
  - destination-pattern 2…
  - session target ipv4:172.16.200.2

  - dial-peer voice 3 voip
  - destination-pattern 3…
  - session target ipv4:172.16.200.3

- The image below shows mobile 1000 communicating with telephone 1001.

![VoIPServiceB4.png](./resources/telefones_comunicacao.png)

-------------------------------------------------------------------

#### DNS

The DNS table is shown below.

![dns´_b4.png](./resources/dns_b4.png)


-------------------------------------------------------------------

#### NAT

- Static NAT was used to redirect traffic, and the commands below were used for this purpose:

  - **Router(config)#** ip nat inside source static tcp 172.16.206.227 80 172.16.200.4 80
  - **Router(config)#** ip nat inside source static tcp 172.16.206.227 443 172.16.200.4 443
  - **Router(config)#** ip nat inside source static tcp 172.16.206.226 53 172.16.200.4 53
  - **Router(config)#** ip nat inside source static udp 172.16.206.226 53 172.16.200.4 53


- Finally, each VLAN was placed inside the NAT created, except the backbone, through the commands:
  - ip nat inside
  - ip nat outside

-------------------------------------------------------------------

#### ACLs

As for the ACLs, I tried to implement them, but as I can't get them to work, there's only a configuration file in the resources with my attempt - "R0_B4_startup-config_ACLs.txt".

- access-list 5 permit 172.16.200.0 0.0.0.127
- access-list 100 permit ip 172.16.206.192 0.0.0.31 any
- access-list 100 permit icmp any any echo
- access-list 100 permit icmp any any echo-reply
- access-list 100 permit ip any host 255.255.255.255
- access-list 100 permit udp any host 172.16.206.193 eq tftp
- access-list 100 permit tcp any host 172.16.206.193 eq 2000
- access-list 100 permit ospf any any
- access-list 100 deny ip any host 172.16.206.193
- access-list 100 permit ip any any

- access-list 101 permit ip 172.16.206.128 0.0.0.191 any
- access-list 101 permit icmp any any echo-reply
- access-list 101 permit icmp any any echo
- access-list 101 permit ip any host 255.255.255.255
- access-list 101 permit udp any host 172.16.206.129 eq tftp
- access-list 101 permit tcp any host 172.16.206.129 eq 2000
- access-list 101 permit ospf any any
- access-list 101 deny ip any host 172.16.206.129
- access-list 101 permit ip any any

- access-list 102 permit ip 172.16.206.0 0.0.0.127 any
- access-list 102 permit icmp any any echo
- access-list 102 permit icmp any any echo-reply
- access-list 102 permit ip any host 255.255.255.255
- access-list 102 permit udp any host 172.16.206.1 eq tftp
- access-list 102 permit tcp any host 172.16.206.1 eq 2000
- access-list 102 permit ospf any any
- access-list 102 deny ip any host 172.16.206.1
- access-list 102 permit ip any any
 
- access-list 103 permit ip 172.16.206.240 0.0.0.15 any
- access-list 103 permit icmp any any echo
- access-list 103 permit icmp any any echo-reply
- access-list 103 permit ip any host 255.255.255.255
- access-list 103 permit udp any host 172.16.206.241 eq tftp
- access-list 103 permit tcp any host 172.16.206.241 eq 2000
- access-list 103 permit ospf any any
- access-list 103 deny ip any host 172.16.206.241
- access-list 103 permit ip any any

- access-list 104 permit udp any host 172.16.206.226 eq domain
- access-list 104 permit tcp any host 172.16.206.227 eq www
- access-list 104 permit ip 172.16.206.224 0.0.0.15 any
- access-list 104 permit ip any host 255.255.255.255
- access-list 104 permit udp any host 172.16.206.225 eq tftp
- access-list 104 permit tcp any host 172.16.206.225 eq 2000
- access-list 104 permit ospf any any
- access-list 104 deny ip any host 172.16.206.225
- access-list 104 permit ip any any
- access-list 104 permit ospf any host 172.16.206.1

- access-list 105 deny ip 172.16.206.128 0.0.0.63 any
- access-list 105 deny ip 172.16.206.0 0.0.0.127 any
- access-list 105 deny ip 172.16.206.128 0.0.0.63 any
- access-list 105 deny ip 172.16.206.192 0.0.0.31 any
- access-list 105 deny ip 172.16.206.240 0.0.0.15 any
- access-list 105 permit icmp any any echo
- access-list 105 permit icmp any any echo-reply
- access-list 105 permit ospf any any
- access-list 105 permit tcp any host 172.16.206.1 eq 2000
- access-list 105 permit tcp any host 172.16.206.1 eq 1720
- access-list 105 permit tcp any eq 1720 host 172.16.206.1
- access-list 105 permit udp any host 172.16.206.1 eq domain
- access-list 105 permit tcp any host 172.16.206.1 eq www
- access-list 105 deny ip any host 172.16.206.1
- access-list 105 permit ip any any

-------------------------------------------------------------------