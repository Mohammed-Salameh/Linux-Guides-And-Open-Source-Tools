<h3> Configure DNS Forwarding </h3>

1. On your Windows Domain Controller (DC), open the Command Prompt.
2. Execute the following command to add a DNS forwarder:
```bash
C:> dnscmd 127.0.0.1 /ZoneAdd ipa_domain /Forwarder ipa_ip_address
```
Replace `ipa_domain` with your IPA domain and `ipa_ip_address` with the IP address of your IPA server.

#

<h3> Linux Machine Configuration </h3>

<h5> Initial Setup </h5>

- **Set Hostname**: Configure the hostname as required.

- **Disable IPv6**: To disable IPv6, modify the following system setting:
```bash
net.ipv6.conf.<interface0>.disable_ipv6 = 1
```

Replace `<interface0>` with your network interface name.

#

<h3> Installing FreeIPA </h3>

<h5> Enable FreeIPA Repository </h5>

Run the following command to activate the repo for FreeIPA:
```bash
dnf module -y install idm:DL1/dns --skip-broken
```

<h5> Update System and Install Packages </h5>

Execute these commands to update your system and install necessary packages:
```bash
yum update -y
yum install -y "*ipa-server" "*ipa-server-trust-ad" bind bind-dyndb-ldap
```

<h5> Troubleshooting Installation </h5>

If you encounter the error:
```bash
ipa-server-install: error: option setup-dns: Integrated DNS requires 'ipa-server-dns' package
```

Resolve it by running:

dnf install ipa-server-dns


<h5> Install FreeIPA Server </h5>

To install and configure the FreeIPA server, use:
```bash
ipa-server-install -a mypassword1 -p mypassword2 --domain=ipa_domain --realm=IPA_DOMAIN --setup-dns --no-forwarders -U
```

Replace `mypassword1` and `mypassword2` with your chosen passwords, and adjust `ipa_domain` and `IPA_DOMAIN` accordingly.
