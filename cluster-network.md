# Seapath Cluster Network

Seapath default recommended architecture is to use 3 hosts, directly interconnected to each other in a loop topology ("cluster network").

It is also possible to use external switches, but the high availability requirements would demand to use 2 switches (in case one fails), interconnected together (2 times in case one link fails), to connect every host to both switches and to use a mecanism like LACP to deal with multiple paths.

We think that for a 3-node cluster, a no-switch architecture is simple to create, manage, debug, etc.

![cluster_network1.svg](cluster_network1.svg)

We propose a layer 2 networking solution, where each host runs a software bridge (we call it "team0"), with 2 ports connected to external network interfaces. Each of the 2 network interfaces is connected to one of the other host. The ip address for the host on this cluster network is directly set to the team0 bridge: 

![cluster_network2.svg](cluster_network2.svg)
