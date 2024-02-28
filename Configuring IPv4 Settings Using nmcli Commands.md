
**Description:**
This document provides a step-by-step guide on how to modify the IPv4 settings of a network interface using the NetworkManager 
command-line tool, `nmcli`. It demonstrates how to assign an IP address, set a gateway, change the network configuration method, 
and specify a DNS value for an interface.

1. The command `nmcli connection modify <interface_name> ipv4.address <ip/prefix>` is used to assign an IPv4 address to an interface.
For brevity, `connection` can be replaced with `con` and `modify` with `mod`.

2. The following commands are executed as root:

   - Assign the IP address `192.168.1.4` with a `/24` prefix to `enp0s3` interface:  `nmcli con mod enp0s3 ipv4.addresses 192.168.1.4/24`
   - Set the gateway for the `enp0s3` interface to `192.168.1.1`: `nmcli con mod enp0s3 ipv4.gateway 192.168.1.1`
   - Switch from DHCP to static/manual configuration:`nmcli con mod enp0s3 ipv4.method manual`
   - Assign the DNS value `8.8.8.8` to the `enp0s3` interface:  `nmcli con mod enp0s3 ipv4.dns "8.8.8.8"`
   - To save the above changes and reload the `enp0s3` interface: `nmcli con up enp0s3`, which confirms the successful activation of the connection.

3. For users who prefer a graphical interface for network configurations, you can use nmtui to achieve the same settings in a GUI environment.
