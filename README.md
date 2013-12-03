gre-tun-probe
=============

GRE tunnel probing utility for neutron/compute with OVS

It can be used to probe neutron/openvswitch configuration by sending fake packets in
GRE tunnel via br-tun bridge to see if GRE is processed correctly without spinning up instances.

It create pair of veth interfaces, plug  on of them in the (specified) bridge, add openflow rule 
to openvswitch database to add (specified) GRE label to packets and send them to (specified) out port. 

It bypass ARP broadcast part and 'just send unicast packets'.

To forcefully emulate traffic from guests:

./gre-tun-probe br-tun 0x1 2
or
./gre-tun-probe -c 100 br-tun 0x1 2 192.168.1.1 192.168.1.2 10:0b:a9:bd:26:a8 
(send 100 packets from 192.168.1.1 to 192.168.1.2 with dest. mac 10:0b:a9:bd:26:a8 via bridge br-tun with gre label 0x1 in output port #2).

Notice about nping:

This utility relies on nping, which is shipped with recent versions of nmap (recent: newer than precise), some upgrade may require.

