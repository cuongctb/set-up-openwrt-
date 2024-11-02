 # fix ' the_opkg update command failed with_code 6 ' openwrt
 1. network > firewall > General Settings : accept Forward in firewall.
 2. disable ipv6 in network > interface > Interfaces and Devices
3. del 'eth0.1' devices ?
 4.  
```
vi /etc/config/network && reboot
```
orginal:

config device

        option name 'phy0-sta0'
        
        option ipv6 '0'
        
after:

config device

         option name 'phy1-ap0' 
         
         option ipv6 '0'


# set-up-openwrt-

fix openwrt core:
https://github.com/cuongctb/set-up-openwrt-/raw/refs/heads/main/backup-fix-openwrt-2024-11-2-2.tar.gz

fix openwrt basic:
https://github.com/cuongctb/set-up-openwrt-/raw/refs/heads/main/backup-OpenWrt-ngay2-11-basic.tar.gz

