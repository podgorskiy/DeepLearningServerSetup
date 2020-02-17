# Direct Ethernet Connection

To list all ethernet ports:

    ip link
___    

To see device info of the ethernet port:

    ethtool <device name>
---
To check if port is connected to something:

    cat /sys/class/net/<device name>/carrier

Will print `1` if connected and `0` if not.

---

Check active eathernet ports and binded IP addresses:

    ifconfig
---
Set static IP addpress for the device:

    sudo nano /etc/netplan/01-netcfg.yaml

Where `01-netcgf.yaml` is a config file, name may vary.

Example configuration for a machine with ports eno1 (connected to internet) and eno2 (connected to other machine):

    # This file describes the network interfaces available on your system
    # For more information, see netplan(5).
    network:
      version: 2
      renderer: networkd
      ethernets:
        eno1:
          dhcp4: yes
        eno2:
          dhcp4: no
          addresses: [192.168.1.1/24]

To apply config:

    sudo netplan apply
---
Check writing speed:
    
    dd if=/dev/zero of=/data/test.img bs=10M count=256 conv=fdatasync

Where `/data/test.img` path to the file to write to.
