---
title: Automatic IP Allocation and the Weave Proxy
layout: default
---


If [automatic IP address allocation](/site/ipam/overview-init-ipam.md) is enabled in Weave (by default IPAM is enabled),
then containers started via the proxy are automatically assigned an IP address, *without having to specify any
special environment variables or any other options*.

    host1$ docker run -ti ubuntu

To use a specific subnet, we pass a `WEAVE_CIDR` to the container, e.g.

    host1$ docker run -ti -e WEAVE_CIDR=net:10.32.2.0/24 ubuntu

To start a container without connecting it to the Weave network, pass
`WEAVE_CIDR=none`, for example:

    host1$ docker run -ti -e WEAVE_CIDR=none ubuntu


###Disabling Automatic IP Address Allocation

If you do not want an IP to be assigned by default, the proxy needs to
be passed the `--no-default-ipalloc` flag, for example:

    host1$ weave launch-proxy --no-default-ipalloc

In this configuration, containers with no `WEAVE_CIDR` environment
variable are not connected to the Weave network. 

Containers started with a `WEAVE_CIDR` environment variable are handled as before. 
To automatically assign an address in this mode, start the
container with a blank `WEAVE_CIDR`, for example:

    host1$ docker run -ti -e WEAVE_CIDR="" ubuntu
    
**See Also**

 * [Address Allocation with IP Address Management (IPAM)](/site/ipam/overview-init-ipam.md)
 * [How to Manually Specify IP Addresses and Subnets](/site/using-weave/manual-ip-address.md)    