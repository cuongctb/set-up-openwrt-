 # fix ' the_opkg update command failed with_code 6 ' openwrt

 # method 1:
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

         option name 'phy0-ap0' 
         
         option ipv6 '0'


# method 2:
1. disable ipv6 in network > interface > Interfaces and Devices
2. create new file 

```
vi a && chmod +x a
```

3. copy text and paste into a.
```
#!/bin/bash

# file network address
CONFIG_FILE="/etc/config/network"

# Check for the presence of phy1-sta0 or phy0-sta0
if ! grep -q "option name 'phy1-sta0'" "$CONFIG_FILE" && ! grep -q "option name 'phy0-sta0'" "$CONFIG_FILE"; then
    echo "Not found! phy1-sta0 or phy0-sta0 in $CONFIG_FILE."
    exit 1
fi

# Replace 'phy1-sta0' or 'phy0-sta0' and 'phy1-ap0' or 'phy0-ap0'
sed -i "s/option name 'phy1-sta0'/option name 'phy1-ap0'/g" "$CONFIG_FILE"
sed -i "s/option name 'phy0-sta0'/option name 'phy0-ap0'/g" "$CONFIG_FILE"

# Reboot
echo "Done $CONFIG_FILE."
echo "reboot..."
reboot

```
4. runing
   ```
   sh a
   ```

# set-up-openwrt-

fix openwrt core:
https://github.com/cuongctb/set-up-openwrt-/raw/refs/heads/main/backup-fix-openwrt-2024-11-2-2.tar.gz

fix openwrt basic:
https://github.com/cuongctb/set-up-openwrt-/raw/refs/heads/main/backup-OpenWrt-ngay2-11-basic.tar.gz

