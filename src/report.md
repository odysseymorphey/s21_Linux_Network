## Instrument ipcalc

### Networks and masks

1. Network address of 192.167.38.54/13
![ipcalc1](screenshots/ipcalc1.png)
2. Conversion of the mask 255.255.255.0 to prefix and binary,
![ipcalc2](screenshots/ipcalc2.png)
/15 to normal and binary
![ipcalc3](screenshots/ipcalc3.png)
11111111.11111111.11111111.11110000 to normal and prefix
![ipcalc4](screenshots/ipcalc4.png)
3. Minimum and maximum host in 12.167.38.4 network with masks:\
/8
![ipcalc5](screenshots/ipcalc5.png)
11111111.11111111.00000000.00000000
![ipcalc6](screenshots/ipcalc6.png)
/4
![ipcalc7](screenshots/ipcalc7.png)
4.
    `127.0.0.2`, `127.1.0.1` have a loopback channel\
    `194.34.23.100`, `128.0.0.1`  does not have a loopback channel

5.
    `10.0.0.45/8` - private\
    `134.43.0.2/16` - public\
    `192.168.4.2/16` - private\
    `172.20.250.4/12` - private\
    `172.0.2.1/12` - public\
    `192.172.0.1/12` - semi private\
    `172.68.0.2/12` - public\
    `172.16.255.255/12` - private\
    `10.10.10.10/8` - private\
    `192.169.168.1/16`- public

6.
    `10.10.0.2`\
    `10.10.10.10`\
    `10.10.1.255`

## Static routing between two machines
- Existing network interfaces
- ws-1
![ipa_ws1](screenshots/ipa_ws1.png)
- ws-2
![ipa_ws2](screenshots/ipa_ws2.png)
- network interface corresponding to the internal network is `enp0s8`
- yaml ws-1
![yaml_ws1](screenshots/yaml_ws1.png)
- yaml ws-2
![yaml_ws2](screenshots/yaml_ws2.png)
- `ip a` after netplan applying
- ws-1
![ipa2_ws1](screenshots/ipa2_ws1.png)
- ws-2
![ipa2_ws2](screenshots/ipa2_ws2.png)

2.1 Adding static route manually

- Adding static route for ws-1
![static_ws1](screenshots/static_ws1.png)
- Adding static route for ws-2
![static_ws2](screenshots/static_ws2.png)

- Pinging ws-1
![ping_ws1](screenshots/ping_ws1.png)
- Pinging ws-2
![ping_ws2](screenshots/ping_ws2.png)

2.2 Adding a static route with saving

- Static route via yaml for ws-1
![static2_ws1](screenshots/static2_ws1.png)
- Statc route via yaml for ws-2
![static2_ws2](screenshots/static2_ws2.png)

- Pinging ws-1
![ping2_ws1](screenshots/ping2_ws1.png)
- Pinging ws-2
![ping2_ws2](screenshots/ping2_ws2.png)

## iperf3 utility

- 8 Mbps = 1 MB/s\
100 MBs = 800000 Kbps\
1 Gbps = 1000 Mbps

- Checking connection speed
- ws-1
![iperf3_ws1_1](screenshots/iperf3_ws1_1.png)
![iperf3_ws1_2](screenshots/iperf3_ws1_2.png)

- ws-2
![iperf3_ws2_1](screenshots/iperf3_ws2_1.png)
![iperf3_ws2_1](screenshots/iperf3_ws2_2.png)

## Network firewall

- ws-1
![firewall_ws1](screenshots/firewall_ws1.png)
- ws-2
![firewall_ws2](screenshots/firewall_ws2.png)

- running `chmod +x /etc/firewall.sh` and `/etc/firewall.sh` commands
- ws-1
![firewall2_ws1](screenshots/firewall2_ws1.png)
- ws-2
![firewall2_ws2](screenshots/firewall2_ws2.png)
> The difference in strategies lies in the fact that initially in the ws-1 machine we allow pinging, and then prohibit. In the ws-2 machine everything is exactly the opposite.

4.2 nmap utility

- Can not pinging the machine
![nmap](screenshots/nmap.png)

## Static network routing

5.1 Configuration addresses

- configuring yaml file for machines
- ws-11
![yaml_ws11](screenshots/yaml_ws_11.png)
- ws-21
![yaml_ws21](screenshots/yaml_ws_21.png)
- ws-22
![yaml_ws22](screenshots/yaml_ws_22.png)
- r1
![yaml_r1](screenshots/yaml_r1.png)
- r2
![yaml_r2](screenshots/yaml_r2.png)

- Restarting network services, ip showing and pinging
- r1
![ip_r1](screenshots/ip_r1.png)
- r2
![ip_r2](screenshots/ip_r2.png)
- ws-11
![ip_ws11](screenshots/ip_ws11.png)
- ws-21
![ip_ws21](screenshots/ip_ws21.png)
- ws-22
![ip_ws22](screenshots/ip_ws22.png)

5.2 Enabling IP forwarding

- r1
![syctl_r1](screenshots/sysctl_r1.png)
![sysctl2_r1](screenshots/sysctl2_r1.png)
- r2
![sysctl_r2](screenshots/sysctl_r2.png)
![sysctl2_r2](screenshots/sysctl2_r2.png)

5.3. Default route configuration

- Adding gateway and run command `ip r`

- ws-11
![gate_ws11](screenshots/gate_ws11.png)
![ipr_ws11](screenshots/ipr_ws11.png)
- ws-21
![gate_ws21](screenshots/gate_ws21.png)
![ipr_ws21](screenshots/ipr_ws21.png)
- ws-22
![gate_ws22](screenshots/gate_ws22.png)
![ipr_ws22](screenshots/ipr_ws22.png)
- r1
![gate_r1](screenshots/gate_r1.png)
![ipr_r1](screenshots/ipr_r1.png)
- r2
![gate_r2](screenshots/gate_r2.png)
![ipr_r2](screenshots/ipr_r2.png)

- Ping r2 router from ws11
![ping3_ws11](screenshots/ping3_ws11.png)
![tcpdump_r2](screenshots/tcpdump_r2.png)

5.4 Adding static routes
- r1
![stroute_r1](screenshots/gate_r1.png)
![ipr2_r1](screenshots/ipr2_r1.png)
- r2
![stroute_r2](screenshots/gate_r2.png)
![ipr2_r2](screenshots/ipr2_r2.png)
- ws-11
![ipr2_ws11](screenshots/ipr2_ws11.png)
- A path other than 10.10.0.0 is selected in the report because this address points to all addresses.

5.5 List of paths

- r1 dump
![tcpdump_r1](screenshots/tcpdump_r1.png)
- ws-11 traceroute
![traceroute_ws11](screenshots/traceroute_ws11.png)
- The traceroute utility sends udp packets to the specified address. Each packet contains a lifetime variable (ttl), which decreases with each node traversed. The utility will respond with the `ICMP PORT_UNREACHABLE` message if the lifetime ends or the packet reaches the recipient.

5.6 Using ICMP protocol in routing

- ws-11 pinging 10.30.0.11
![ping4_ws11](screenshots/ping4_ws11.png)
- r1 icmp filter in tcpdump
![traceroute_icmp_r1](screenshots/traceroute_icmp_r1.png)

## Dynamic IP configuration using DHCP

- r2 dhcp.conf
![dhcp_r2](screenshots/dhcp_r2.png)
- r2 resolve.conf
![resolve_r2](screenshots/resolve_r2.png)
- ws-11 `ip a`
![ipa_ws21](screenshots/ipa_ws21.png)
- pinging ws-22 from ws-21
![ping5_ws21](screenshots/ping5_ws21.png)
- ws-11 netplan
![yaml2_ws11](screenshots/yaml2_ws11.png)
- r1 dhcp.conf
![dhcp_r1](screenshots/dhcp_r1.png)
- r1 resolv.conf
![resolve_r1](screenshots/resolve_r2.png)
- ws-11 `ip a`
![ipa_ws11](screenshots/ipa_ws11.png)

- ws-21 dhcp setup
- ws-21 `ip a` before
![ipa_ws21_before](screenshots/ipa_ws21_before.png)
- ws-21 `ip a` after
![ipa_ws21_after](screenshots/ipa_ws21_after.png)
- `dhclient -r` for reset current address
- `dhclient -v` for get new address

## NAT

- changing ports.conf in ws-22
![ports_ws22](screenshots/ports_ws22.png)
- changing ports.conf in r2
![ports_r2](screenshots/ports_ws22.png)
- starting apache on r1
![apache_start_r1](screenshots/apache_start.png)
- starting apache on ws-22
![apache_start_ws22](screenshots/apache_start.png)
- ping ws22 from r1. ws22 should not be pinged
![nat_ping_ws22](screenshots/nat_ping_r1.png)
- ping ws22 after adding rule in firewall.sh
![nat_ping2_r1](screenshots/nat_ping2_r1.png)

- ws-22
![telnet_ws22](screenshots/telnet_ws22.png)
- r1
![telnet_r1](screenshots/telnet_r1.png)

- firewall
![nat_firewall](screenshots/nat_firewall.png)
- ws-21 local tcp forwarding
- `ssh -L local_port:remote_ip:remote_port user@hostname`
![local](screenshots/local.png)
- ws-11 remote tcp forwarding
- `ssh -R remote_port:local_ip:local_port user@hostname`
![remote](screenshots/remote.png)
