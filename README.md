# openwrt
openwrt
wget -O /bin/myip "https://raw.githubusercontent.com/zysyft/openwrt/main/myip" && chmod +x /bin/myip
wget -O /bin/speedtest "https://raw.githubusercontent.com/vitoharhari/speedtest/main/speedtest" && chmod +x /bin/speedtest
wget -O /bin/myip "https://raw.githubusercontent.com/helmiau/OpenWrt-Rpi/main/files/bin/myip" && chmod +x /bin/myip
wget -O /bin/neofetch "https://raw.githubusercontent.com/helmiau/openwrt-config/main/neopet" && chmod +x /bin/neofetch

## aria2

opkg update
opkg install aria2
cd /root
wget https://github.com/ziahamza/webui-aria2/archive/master.zip
opkg install unzip
unzip master.zip
mkdir -p /www/webui
cd webui-aria2-master/docs
mv * /www/webui
opkg install nano
mkdir -p /etc/aria2
nano /etc/aria2/aria2.conf

dir=/root/Downloads
enable-rpc=true
rpc-listen-port=6800
rpc-listen-all=true
check-integrity=false
file-allocation=none
log=/dev/null
console-log-level=error

aria2c --conf-path=/etc/aria2/aria2.conf --daemon=true

## samba

opkg install ntfs-3g samba4-server samba4-libs luci-app-samba4

nano rc local
sleep 1

ntfs-3g /dev/sda5 /mnt/sda5 -o rw,lazytime,noatime,big_writes
aria2c --conf-path=/etc/aria2/aria2.conf --daemon=true
exit 0
