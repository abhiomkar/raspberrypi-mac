# RaspberryPi Setup (Mac)

Insert SD Microcard to your Mac & Unmount the disk

    df -h
    diskutil unmount /dev/disk1s2

Format with ExFAT using Disk Utility App & write the downloaded image (Raspbian) to disk

    sudo dd bs=1m if=2015-09-24-raspbian-jessie.img of=/dev/rdisk1

Imaging takes few minutes, after successful imaging you should see the disk mounted with Linux files in it (with the name of 'boot'), Insert this SD Microcard to RaspberryPi,
Connect Power (5V / ~700mA), Ethernet Cable to RaspberryPi. RaspberryPi automatically boots the Debian OS and connects to the network.

Do advance IP Scan on your Mac to find out which IP address the RaspberryPi is connected to.

    $ ifconfig | grep broadcast
    	inet 192.168.1.2 netmask 0xffffff00 broadcast 192.168.1.255
    $ arp -a
    d-link123.home (192.168.1.1) at bc:f6:85:4d:dd:ea on en1 ifscope [ethernet]
    raspberrypi.home (192.168.1.3) at b8:27:eb:fc:2a:28 on en1 ifscope [ethernet]
    abhinays-iphone.home (192.168.1.4) at d0:25:98:9e:27:31 on en1 ifscope [ethernet]
    ? (192.168.1.255) at (incomplete) on en1 ifscope [ethernet]

as you can see from above output of `arp` command our RaspberryPi is connected to 192.168.1.3. You can connect to directly using IP address or the hostname `raspberrpi`

    ssh pi@raspberrpi

default password for login is `raspberry` (username: pi), you should be able to login to RaspberryPi.

If you want connect to Wifi, get a USB Wifi Adapter (I recommend [TP-Link TL-WN725N 150Mbps Wireless N Nano USB Adapter](http://www.amazon.in/gp/product/B008IFXQFU?psc=1&redirect=true&ref_=oh_aui_detailpage_o06_s00)). 

Turn off the RaspberryPi before inserting USB Wifi Adapter and turn it on with Ethernet cable & USB Wifi Adapter connected and ssh to RaspberryPi.


	# check the system logs if your RaspberryPi detected the new device (WLAN Adapter)
	dmesg | more
	
	# configure Wifi Network
	sudo vi /etc/network/interfaces

add SSID and network password, contents of the above should look something like this:

	auto lo
	iface lo inet loopback
	iface eth0 inet dhcp
	
	allow-hotplug wlan0
	auto wlan0
	
	iface wlan0 inet dhcp
	   wpa-ssid "Your Network SSID"
	   wpa-psk "Your Password"
		
Reload network intefaces, it should connect to network via wlan0

	sudo service networking reload
	
	ifconfig
		
	wlan0       Link encap:Ethernet  HWaddr 60:e3:27:0b:98:02
				inet addr:192.168.1.5  Bcast:192.168.1.255  Mask:255.255.255.0
				inet6 addr: fe80::62e3:27ff:fe0b:9802/64 Scope:Link
				UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
				RX packets:946 errors:0 dropped:42 overruns:0 frame:0
				TX packets:633 errors:0 dropped:4 overruns:0 carrier:0
				collisions:0 txqueuelen:1000
				RX bytes:153657 (150.0 KiB)  TX bytes:106735 (104.2 KiB)
				
Now you can disconnect the Ethernet cable and reboot RaspberryPi, it should automatically connect to Wifi on boot.