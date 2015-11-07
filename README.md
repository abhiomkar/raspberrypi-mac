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
    $ arp -a
    d-link123.home (192.168.1.1) at bc:f6:85:4d:dd:ea on en1 ifscope [ethernet]
    raspberrypi.home (192.168.1.3) at b8:27:eb:fc:2a:28 on en1 ifscope [ethernet]
    abhinays-iphone.home (192.168.1.4) at d0:25:98:9e:27:31 on en1 ifscope [ethernet]
    ? (192.168.1.255) at (incomplete) on en1 ifscope [ethernet]

as you can see from above output of `arp` command our RaspberryPi is connected to 192.168.1.3. You can connect to directly using IP address or the hostname `raspberrpi`

    ssh pi@raspberrpi

default password for login is `raspberry` (username: pi)




