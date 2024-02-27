<h3> Windows DC Preparation Steps </h3>

<h4> Configure DNS Forwarding </h4>

1. On your Windows Domain Controller (DC), open the Command Prompt.
2. Execute the following command to add a DNS forwarder:

C:> dnscmd 127.0.0.1 /ZoneAdd ipa_domain /Forwarder ipa_ip_address

Replace `ipa_domain` with your IPA domain and `ipa_ip_address` with the IP address of your IPA server.

#

<h3> Linux Machine Configuration </h3>

<h6> Initial Setup </h6>

1. **Set Hostname**: Configure the hostname as required.

2. **Disable IPv6**: To disable IPv6, modify the following system setting:

net.ipv6.conf.<interface0>.disable_ipv6 = 1


Replace `<interface0>` with your network interface name.

#

<h3> Installing FreeIPA </h3>

<h6> Enable FreeIPA Repository </h6>

Run the following command to activate the repo for FreeIPA:

dnf module -y install idm:DL1/dns --skip-broken


<h6> Update System and Install Packages </h6>

Execute these commands to update your system and install necessary packages:

yum update -y
yum install -y "*ipa-server" "*ipa-server-trust-ad" bind bind-dyndb-ldap


<h6> Troubleshooting Installation </h6>

If you encounter the error:

ipa-server-install: error: option setup-dns: Integrated DNS requires 'ipa-server-dns' package


Resolve it by running:

dnf install ipa-server-dns


<h6> Install FreeIPA Server </h6>

To install and configure the FreeIPA server, use:

ipa-server-install -a mypassword1 -p mypassword2 --domain=ipa_domain --realm=IPA_DOMAIN --setup-dns --no-forwarders -U


Replace `mypassword1` and `mypassword2` with your chosen passwords, and adjust `ipa_domain` and `IPA_DOMAIN` accordingly.
