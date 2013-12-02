gre-tun-probe
=============

GRE tunnel probing utility

Used to probe neutron/openvswitch configuration by sending fake packets in
gre tunnel in br-tun bridge.

It create veth interface, plug in in the (specified) bridge, add openflow rule 
to openvswitch to add (specified) GRE label and send to (specified) out port. 
It allows to see if GRE set up working correctly without other components of 
neutron. It bypass ARP broadcast part and 'just send unicast packets'.

To forcefully emulate traffic from guests:

./gre-tun-probe br-tun 0x1 2
or
./gre-tun-probe -c 100 br-tun 0x1 2 192.168.1.1 192.168.1.2 10:0b:a9:bd:26:a8 
(send 100 packets from 192.168.1.1 to 192.168.1.2 with dest. mac 10:0b:a9:bd:26:a8 via bridge br-tun with gre label 0x1 in output port #2).

It relies on nping utility, which is shipped with recent version of nmap (recent: newer than precise), some upgrade may require. 

