

The procedure is as follows to set up and configure a static IP information:

1. Open the terminal application.
2. Log in to remote or server using ssh command.
3. Backup /etc/network/interfaces file running **sudo cp /etc/network/interfaces /root/**
4. Edit the /etc/network/interfaces
5. Configure static IP address for enp0s5 Ethernet interface: **address 192.168.2.249**
6. Add subnet mask: **netmask 255.255.255.0**
7. Set up default gateway IP: **gateway 192.168.2.254**
8. Finally add DNS resolver IP: **dns-nameservers 192.168.2.254 8.8.8.8 1.1.1.1**

Let us see all commands and examples in details.

## Finding your network interfaces name on Debian Linux

Use the [ip command](https://www.cyberciti.biz/faq/linux-ip-command-examples-usage-syntax/ "Linux ip Command Examples") as follows to [show/display available Ethernet network interfaces](https://www.cyberciti.biz/faq/linux-list-network-interfaces-names-command/):  
`$ ip -c link show`  
Also, we can try the following [Linux command to show a list of network cards](https://www.cyberciti.biz/faq/linux-list-network-cards-command/):  
`$ sudo lshw -class network -short   # Filter results using [grep](https://www.cyberciti.biz/faq/howto-use-grep-command-in-linux-unix/ "How to use grep command in Linux/ Unix with examples")/[egrep regex command](https://www.cyberciti.biz/faq/grep-regular-expressions/ "Regular expressions in grep ( regex ) with examples")   $ lspci | grep -E -i --color 'network|ethernet|wireless|wi-fi'   $ ip -br -c link show`  
Note down the Debian Linux interface name and type the following [ip command](https://www.cyberciti.biz/faq/linux-ip-command-examples-usage-syntax/ "Linux ip Command Examples") to see [the current IP address assinged to that network interface](https://www.cyberciti.biz/faq/how-to-find-out-the-ip-address-assigned-to-eth0-and-display-ip-only/):  
`$ ip -c addr show enp0s5`  

![How to setup a Static IP address on Debian Linux](https://www.cyberciti.biz/media/new/faq/2021/01/How-to-setup-a-Static-IP-address-on-Debian-Linux.png)

Finding NIC name and IP assigned by the DHCP server on Debian Linux

## Configuring Static IP on Debian 10 or 11

The /etc/network/interfaces[/file] contains network interface configuration information for Debian Linux. Hence, edit the file:  
`$ sudo vim /etc/network/interfaces   ## OR ##   $ sudo nano /etc/network/interfaces`  
Look for the primary network interface enp0s5:

allow-hotplug enp0s5
iface enp0s5 inet dhcp

Remove dhcp and allow-hotplug lines. Append the following configuration to set up/add new static IP on Debian Linux 10/11. Here is my sample config file:

# The loopback network interface
auto lo
iface lo inet loopback
 
# The primary network interface
auto enp0s5
iface enp0s5  inet static
 address 192.168.2.236
 netmask 255.255.255.0
 gateway 192.168.2.254
 dns-domain sweet.home
 dns-nameservers 192.168.2.254 1.1.1.1 8.8.8.8

[Save and close the file when using vim/vi](https://www.cyberciti.biz/faq/linux-unix-vim-save-and-quit-command/) text editor.

## Restart networking service on Debian Linux to switch from DHCP to static IP config

**Warning**: Do not run the following over ssh based session as you will disconnect.

Use the systemctl command as follows:  
`$ sudo systemctl restart networking.service`  
Make sure service restarted without any errors. Hence, type the following command:  
`$ sudo systemctl status networking.service`  
Sample session:

● networking.service - Raise network interfaces
   Loaded: loaded (/lib/systemd/system/networking.service; enabled; vendor preset: enabled)
   Active: active (exited) since Wed 2021-01-27 23:10:00 IST; 1min 38s ago
     Docs: man:interfaces(5)
  Process: 1104 ExecStart=/sbin/ifup -a --read-environment (code=exited, status=0/SUCCESS)
 Main PID: 1104 (code=exited, status=0/SUCCESS)

## See your new IP address assigned on Debian Linux

Again type the following [ip command](https://www.cyberciti.biz/faq/linux-ip-command-examples-usage-syntax/ "Linux ip Command Examples"):  
`$ ip -c addr show   $ ip -c addr show enp0s5`  
![How to configure Static IP on Debian 10 or 11](https://www.cyberciti.biz/media/new/faq/2021/01/How-to-configure-Static-IP-on-Debian-10-or-11.png)  
When you change your IP address, you need to restart other services such as Nginx, SSH, etc. It all depends upon how you configured those services with IP binding. Make sure you adjust the firewall settings too.

## A note about /etc/network/interfaces.d/ directory

**WARNING!** The following is an advanced configuration and is only recommended if you know various networking concepts. The nixCraft or author is not responsible for network connectivity loss.

You can place the network config in a separate file under /etc/network/interfaces.d/. I tested the following with Debian 11 with source keyword:

source /etc/network/interfaces.d/*

In other words, config lines beginning with “source” are used to include stanzas from other files. So configuration can be split into many files for ease of management. The word “source” is followed by the path of a file to be sourced. Shell wildcards can be used. Here is how /etc/network/interfaces looks now:  
`$ sudo [cat](https://www.cyberciti.biz/faq/linux-unix-appleosx-bsd-cat-command-examples/ "cat Command in Linux / Unix with examples") /etc/network/interfaces`  
Outputs:

# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
 
source /etc/network/interfaces.d/*
 
# The loopback network interface
auto lo
iface lo inet loopback

Here is my servers bridge network config file named /etc/network/interfaces.d/br0  
`$ sudo vim /etc/network/interfaces.d/br0`  
Append the following config to create br0 interface using eno1 Ethernet interface. For example:

auto br0
iface br0 inet static
	address 192.168.2.19
	broadcast 192.168.2.255
	netmask 255.255.255.0
	gateway 192.168.2.254
	# If the resolvconf package is installed, you should not edit 
	# the resolv.conf configuration file manually. Set name server here
        dns-nameservers 192.168.2.236 192.168.2.237
        dns-domain sweet.home
	# If you have multiple interfaces such as eth0 and eth1
	# bridge_ports eth0 eth1  
	bridge_ports eno1
	bridge_stp off           # disable Spanning Tree Protocol
        bridge_waitport 0    # no delay before a port becomes available
        bridge_fd 0          # no forwarding delay

Then restart networking service on Debian Linux or [reboot the Linux machine](https://www.cyberciti.biz/faq/howto-reboot-linux/ "Reboot Linux System Command") using the [shutdown command](https://www.cyberciti.biz/faq/howto-shutdown-linux/ "How To Shutdown Linux Using Command Line")/[reboot command](https://www.cyberciti.biz/faq/howto-reboot-linux/ "Reboot Linux System Command"). For instance:  
`$ sudo reboot`  
OR  
`$ systemctl restart networking.service`

## Conclusion

You learned how to convert the existing DHCP to static IP address settings on Debian Linux version 9/10/11. See Debian Linux [man page online](https://www.debian.org/doc/manuals/debian-reference/ch05.en.html) or type the following command:  
`$ man interfaces   $ man nmcli`