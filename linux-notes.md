# Centos Notes

## 1.Manage Service


<https://www.cyberciti.biz/faq/check-running-services-in-rhel-redhat-fedora-centoslinux/>

- list all services:

```systemctl list-unit-files```

- stop a service:

```systemctl stop httpd```

- start a service:

```systemctl start httpd```

- view status of a service:

```systemctl status httpd```

## 2.Setup Network

- To setup a network interfaces names ens3 (example), create or edit file: ```/etc/sysconfig/network-scripts/ifcfg-ens3```:

```bash
DEVICE="ens3"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=192.168.50.2
NAME="System ens3"
HWADDR=00:0C:29:28:FD:4C
GATEWAY=192.168.50.1
```

- To enable a network interfaces: ```# ip link set eth1 up```
- To disable a network interfaces: ```# ip link set eth1 down```

**To setup configuration for a new network interfaces** - example named ens10 with ip **10.10.10.12** and MAC address **00:0C:29:28:FD:4C**, following these steps:

- Create configuration file: ```/etc/sysconfig/network-scripts/ifcfg-ens10``` with content as follow:

```bash
DEVICE="ens10"
BOOTPROTO=static
ONBOOT=yes
TYPE="Ethernet"
IPADDR=10.10.10.10
NAME="System ens3"
HWADDR=00:0C:29:28:FD:4C

# if you need gateway, you can add this line
GATEWAY=10.10.10.1
```

- Reboot server

## Routing Basic

[https://www.cyberciti.biz/faq/linux-route-add/
](https://www.cyberciti.biz/faq/linux-route-add/)

<http://www.linuxjournal.com/content/linux-advanced-routing-tutorial>

<https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Deployment_Guide/s1-networkscripts-static-routes.html>

 To add a static route to a host address, in other words to a single IP address, issue a command as root:

```bash
~]# ip route add 192.0.2.1 via 10.0.0.1 [dev ifname]
```

Where 192.0.2.1 is the IP address of the host in dotted decimal notation, 10.0.0.1 is the next hop address and ifname is the exit interface leading to the next hop.

To add a static route to a network, in other words to an IP address representing a range of IP addresses, issue the following command as root:

```bash
~]# ip route add 192.0.2.0/24 via 10.0.0.1 [dev ifname]
```

where 192.0.2.0 is the IP address of the destination network in dotted decimal notation and /24 is the network prefix. The network prefix is the number of enabled bits in the subnet mask. This format of network address slash network prefix length is sometimes referred to as classless inter-domain routing (CIDR) notation.