# Seapath Cluster Network

Seapath default recommended architecture is to use 3 hosts, directly interconnected to each other in a loop topology ("cluster network"). This network will be used for:
- ceph clustering communication (public and private network)
- corosync clustering communication (used by pacemaker)
- vxlan trafic to extend the VM bridges topology


It would also be possible to use external switches for this cluster network, but the high availability requirements would demand to use 2 switches (in case one fails), interconnected together (2 times in case one link fails), to connect every host to both switches and to use a mecanism like LACP to deal with multiple paths.

We think that for a 3-node cluster, a no-switch architecture is simple to create, manage, debug, etc.

![cluster_network1.svg](cluster_network1.svg)


We propose a layer 2 networking solution (using OpenVSwitch since it's included in the seapath distribution), where each host runs a software bridge (we call it "team0"), with 2 ports connected to external network interfaces. Each of the 2 network interfaces is connected to one of the other host. The ip address for the host on this cluster network is directly set to the team0 bridge: 

<img src="cluster_network2.svg" width="800" />


This will create an extended L2 network accross the 3 nodes, each node having a L3 ip address for all the mentionned communications, however this will create an obvious loop. L2 loops needs to be dealt with using some form of spanning tree protocol. We propose to use RSTP.
In this example we set a smaller rstp priority on the host1, which will make rstp cut the loop between the other 2 nodes by setting one port to "discarding" mode.

<img src="cluster_network3.svg" width="800" />
