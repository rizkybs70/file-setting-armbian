

#  Setting file for server

## Network
*beraku untuk distro dengan basis debian, ubuntu dll*
kadang lebih mudah(atau sudah terbiasa)mendefinisikan interface network secara manual, dengan cara memodifikasi file interfaces di /etc/network/, ketimbang membiarkan NetworkManager.service memanage semua network interface yang ada didevice kita. berikut cara mendisable NetworkManager (lakukan dengan hati2, jika memodifikasi lewat ssh)

 **1.** Pertama kita check network intrface mana yang dimanage oleh NetworkManager.  
   `` nmcli dev status  ``
   ```
    DEVICE TYPE
    eth1 802-3-ethernet connected  
	eth0 802-3-ethernet connected
	.....
	....
	..
	.
```
 **2.** Misalkan, kita akan membuat network interface eth0 dengan menggunakan ip address static. edit file /etc/network/interfaces.
```
auto eth0
iface eth0 inet static
```
ubah mac address (hanya contoh),
 ```
hwaddress ether 00:15:18:01:81:42
address 192.168.99.8
netmask 255.255.255.0
gateway 192.168.99.1
dns-nameservers 192.168.99.1 8.8.8.8
```
```
source /etc/network/interfaces.d/*
# Network is managed by Network manager
auto lo
iface lo inet loopback
# Network interfaces
allow-hotplug eth0
iface eth0 inet dhcp
hwaddress ether 00:15:18:01:81:42
```
 **3.** Disable NetworkManager.service
 ```
sudo systemctl stop NetworkManager.service  
sudo systemctl disable NetworkManager.service  
sudo systemctl mask NetworkManager.service
```

## DTB
*Tested debian dan ubuntu*

DTB mod ke 2GB agar usage RAM bisa sampai habis
