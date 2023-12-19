This is a slightly modified version of the PROX (Packet pROcessing eXecution engine).
When configured in routing mode and sub mode l3, the original code always trigger an ARP request to the main transmit port configured
for the core that received the packet to be routed. However, the destination or the gateway may not be on that port.
For example, using the below configuration:

[core 3s0]
name=Routing
task=0
mode=routing
sub mode=l3
local ipv4=10.23.118.245
gateway ipv4=10.23.118.244
route table=lpm4
rx port=if0
tx port=if0,if1
drop=no

A L3 packet is received with destination IPv4 address 192.10.10.10, this must be routed to the gateway at IP 10.23.164.244
that is configured on port 1/if1 to reach the destination. The original behaviour is triggering a ARP request on port 0/if0
requesting the MAC address of IP 10.23.164.244, which is not on the network connected to this port.

The code has been modified to avoid sending ARP request when a lua table is available for routing, therefore the destination
MAC address is available there. In this case, the modified code SEND MBUF directly to the port specified in lua table.
For example:

lpm4.next_hops = {
   {id = 1,  port_id = 1, ip = ip("10.23.164.244"), mac = mac("00:50:56:aa:45:e5"), mpls = 0},
}

The packet is routed and sent directly to the gateway at MAC address 00:50:56:aa:45:e5.

This behaviour is controlled by the following introduced configuration parameter of sub mode l3:
- mac from lua = yes/no

If this parameter is included in the configuration without sub mode l3, it is ignored.

Note that the folllowing core configuration (reverting the tx ports), will cause the PROX to not reply to the ARP request
sent from the outside on rx port 0/if0. Therefore failing to receive packets.

[core 3s0]
name=Routing
task=0
mode=routing
sub mode=l3
;fast path handle arp=yes
local ipv4=10.23.118.245
gateway ipv4=10.23.118.244
route table=lpm4
rx port=if0
tx port=if1,if0
drop=no
