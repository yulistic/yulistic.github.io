+++
author = "yulistic"
date = "2018-03-07T14:03:39+09:00"
description = "How to configure a DHCP server with dnsmasq."
draft = false
tags = ["dnsmasq","DHCP server", "Ubuntu", "Linux"]
title = "Configuring dnsmasq only for DHCP server in Ubuntu PC"
topics = ["tips"]
type = "post"

+++

# Purpsose
To configure my own DHCP server with `dnsmasq` on my Ubuntu PC. A commercial router is running together.  
(Actually, I wanted to setup a PXE boot server with `dnsmasq`.)

# Environment
* A local LAN with the router that can disable its DHCP server functionality.
* Ubuntu 16.04 machine, `dnsmasq` installed.

# Solution
1. Install `dnsmasq`.
    ```
    sudo apt install dnsmasq
    ```

2. Configure `dnsmasq` by writing the default configuration file(`/etc/dnsmasq.conf`) or a new file in the path `/etc/dnsmasq.d/`(For example, `/etc/dnsmasq.d/dhcp.conf`). The default configuration file includes a neat and detailed description of each configuration parameter.
    ```
    # Set the interface on which dnsmasq operates.
    # If not set, all the interfaces is used.
    #interface=enp5s0

    # To disable dnsmasq's DNS server functionality.
    port=0

    # To enable dnsmasq's DHCP server functionality.
    dhcp-range=192.168.0.50,192.168.0.150,255.255.255.0,12h
    #dhcp-range=192.168.0.50,192.168.0.150,12h

    # Set static IPs of other PCs and the Router.
    dhcp-host=90:9f:44:d8:16:fc,iptime,192.168.0.1,infinite		# Router
    dhcp-host=31:25:99:36:c2:bb,server-right,192.168.0.3,infinite	# PC1	
    dhcp-host=ac:97:0e:f2:6f:ab,yul-x230,192.168.0.13,infinite	# PC2

    # Set gateway as Router. Following two lines are identical.
    #dhcp-option=option:router,192.168.0.1
    dhcp-option=3,192.168.0.1

    # Set DNS server as Router.
    dhcp-option=6,192.168.0.1

    # Logging.
    log-facility=/var/log/dnsmasq.log	# logfile path.
    log-async
    log-queries	# log queries.
    log-dhcp	# log dhcp related messages.
    ```

3. (Re)start dnsmasq service. You can check status of dnsmasq with `systemctl` command.
    ```
    sudo service dnsmasq restart
    sudo systemctl status dnsmasq.service
    ```

4. Also you need to set the `dnsmasq` server ip. My network interface name was `enp5s0`. Set it as yours.
Also, the server address was set to `192.168.0.10` in the following example.
    ```
    # interfaces(5) file used by ifup(8) and ifdown(8)
    auto lo
    iface lo inet loopback

    auto enp5s0
    iface enp5s0 inet static
	address 192.168.0.10
	netmask 255.255.255.0
	broadcast 192.168.0.255
	network 192.168.0.1
    ```

5. Restart networking service. If it does not work, just reboot the machine.
    ```
    sudo service networking restart
    ```

6. You need to disable DHCP server functionality of your router. Restart the `dnsmasq` service after disabling it.

# Other tips
1. You can register `dnsmasq` as startup service. (Make it run whenever the machine is rebooted.)
    ```
    update-rc.d dnsmasq defaults
    ```

2. Checking the list of current clients that received IPs from DHCP service.
    ```
    sudo cat /var/lib/misc/dnsmasq.leases
    ```

3. To read logs when the log file is not set in the configuration file.
    ```
    sudo journalctl -u dnsmasq.service
    ```

4. To test the configuration.
    ```
    dnsmasq --test
    ```
