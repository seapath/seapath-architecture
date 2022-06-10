# Welcome to Seapath!

Seapath is a code base that will help create and manage a cluster of machines (hosts) able to run guest operating systems (virtual machines).
Deploying a seapath cluster will be done in several steps:
- choose whether you want to use a Yocto custom image or a standard debian OS
- create the seapath host installation medium
	- for Yocto, follow the directions of the [yocto-bsp](https://github.com/seapath/yocto-bsp) repo
	- for Debian, follow the directions of the [build_debian_iso](https://github.com/seapath/build_debian_iso) repo
- use the choosen seapath  host installation medium on 3 machines
- create a [cluster network](cluster-network.md) (to properly interconnect the 3 nodes)
- configure the cluster using the [ansible](https://github.com/seapath/ansible) repo
	- for Yocto installs, use the main branch
	- for Debian installs, use the debian-main branch
- You can then use the ansible module provided in the [ansible](https://github.com/seapath/ansible) repo to deploy VMs to your cluster
