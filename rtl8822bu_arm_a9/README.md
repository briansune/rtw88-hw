# RTL8822BU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/f4c1f17c-e3b0-46e1-9d36-bbaf120a475c" height="400"/>|<img src="https://github.com/user-attachments/assets/98e43c49-fd6d-4d87-bd60-61dbdfaf872b" height="400"/>|

```
uname -r
5.4.0

lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.5 LTS
Release:        18.04
Codename:       bionic

Architecture:        armv7l
Byte Order:          Little Endian
CPU(s):              2
On-line CPU(s) list: 0,1
Thread(s) per core:  1
Core(s) per socket:  2
Socket(s):           1
Vendor ID:           ARM
Model:               0
Model name:          Cortex-A9
Stepping:            r3p0
BogoMIPS:            666.66
Flags:               half thumb fastmult vfp edsp neon vfpv3 tls vfpd32
```

### USB Tree

```
[    3.644922] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x3 has wMaxPacketSize 0, skipping
[    3.663084] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x83 has wMaxPacketSize 0, skipping
[    3.695198] Bluetooth: hci0: RTL: examining hci_ver=07 hci_rev=000b lmp_ver=07 lmp_subver=8822
[    3.714207] Bluetooth: hci0: RTL: rom_version status=0 version=2
[    3.729530] Bluetooth: hci0: RTL: loading rtl_bt/rtl8822b_fw.bin
[    3.754363] Bluetooth: hci0: RTL: loading rtl_bt/rtl8822b_config.bin
[    3.771551] Bluetooth: hci0: RTL: cfg_sz 14, total sz 20270


/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/2p, 480M
        |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=, 480M

After driver is inserted.

/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/2p, 480M
        |__ Port 1: Dev 4, If 0, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 4, If 1, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 4, If 2, Class=Vendor Specific Class, Driver=rtw_8822bu, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 004: ID 0bda:b82c Realtek Semiconductor Corp.
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.10
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2 ?
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xb82c
  bcdDevice            2.10
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength          229
    bNumInterfaces          3
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0x80
      (Bus Powered)
    MaxPower              500mA
    Interface Association:
      bLength                 8
      bDescriptorType        11
      bFirstInterface         0
      bInterfaceCount         2
      bFunctionClass        224 Wireless
      bFunctionSubClass       1 Radio Frequency
      bFunctionProtocol       1 Bluetooth
      iFunction               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           3
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x81  EP 1 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0010  1x 16 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x02  EP 2 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x82  EP 2 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       0
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0000  1x 0 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0000  1x 0 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       1
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0009  1x 9 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0009  1x 9 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       2
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0011  1x 17 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0011  1x 17 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       3
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0019  1x 25 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0019  1x 25 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       4
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0021  1x 33 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0021  1x 33 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       5
      bNumEndpoints           2
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0031  1x 49 bytes
        bInterval               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            1
          Transfer Type            Isochronous
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0031  1x 49 bytes
        bInterval               4
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        2
      bAlternateSetting       0
      bNumEndpoints           5
      bInterfaceClass       255 Vendor Specific Class
      bInterfaceSubClass    255 Vendor Specific Subclass
      bInterfaceProtocol    255 Vendor Specific Protocol
      iInterface              2
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x84  EP 4 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x05  EP 5 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x06  EP 6 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x87  EP 7 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               3
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x08  EP 8 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
```

</details>

### Driver Load

The driver is loaded via "insmod"

The -71 fail is normal on USB 2.0 speed only port

```
[  239.686007] rtw_core: loading out-of-tree module taints kernel.
[  240.023085] rtw_8822bu 1-1.1:1.2: Firmware version 30.20.0, H2C version 14
[  240.664056] rtw_8822bu 1-1.1:1.2: write register 0xc4 failed with -71
[  240.673291] rtw_8822bu 1-1.1:1.2: rtw_usb_reg_sec: reg 0x4e0, usb write 1 fail, status: -71
[  240.687277] usbcore: registered new interface driver rtw_8822bu
[  240.732529] usb 1-1.1: USB disconnect, device number 3
[  241.204243] usb 1-1: reset high-speed USB device number 2 using ci_hdrc
[  241.744209] usb 1-1.1: new high-speed USB device number 4 using ci_hdrc
[  241.894899] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x3 has wMaxPacketSize 0, skipping
[  241.894915] usb 1-1.1: config 1 interface 1 altsetting 0 endpoint 0x83 has wMaxPacketSize 0, skipping
[  241.901506] Bluetooth: hci0: RTL: examining hci_ver=07 hci_rev=000b lmp_ver=07 lmp_subver=8822
[  241.902454] Bluetooth: hci0: RTL: rom_version status=0 version=2
[  241.902465] Bluetooth: hci0: RTL: loading rtl_bt/rtl8822b_fw.bin
[  241.902919] Bluetooth: hci0: RTL: loading rtl_bt/rtl8822b_config.bin
[  241.903148] Bluetooth: hci0: RTL: cfg_sz 14, total sz 20270
[  241.904301] rtw_8822bu 1-1.1:1.2: Firmware version 30.20.0, H2C version 14
[  242.645384] Bluetooth: hci0: RTL: fw version 0xab6b705c

Module                  Size  Used by
rtw_8822bu             16384  0
rtw_8822b             217088  1 rtw_8822bu
rtw_usb                24576  1 rtw_8822bu
rtw_core              172032  2 rtw_8822b,rtw_usb
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.27  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 11  bytes 1553 (1.5 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 21  bytes 4029 (4.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     3.50 ms   (jitter: 0.69ms, low: 3.25ms, high: 4.48ms)
    Download:   180.26 Mbps (data used: 292.0 MB)
                 25.30 ms   (jitter: 17.46ms, low: 4.66ms, high: 359.97ms)
      Upload:   191.77 Mbps (data used: 337.1 MB)
                 40.90 ms   (jitter: 20.09ms, low: 13.46ms, high: 328.06ms)
```

### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=4.10 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=4.29 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=4.96 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=6.45 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=3.90 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=3.97 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=3.83 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=7.45 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=5.45 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=4.31 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=5.70 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.60 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=4.21 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=6.21 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=3.93 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=4.21 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=5.45 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=4.41 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=3.84 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19026ms
rtt min/avg/max/mdev = 3.835/4.765/7.456/1.004 ms
```

#### Self-Ping 

```
PING 192.168.1.27 (192.168.1.27) 10000(10028) bytes of data.
10008 bytes from 192.168.1.27: icmp_seq=1 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.27: icmp_seq=2 ttl=64 time=0.123 ms
10008 bytes from 192.168.1.27: icmp_seq=3 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.27: icmp_seq=4 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.27: icmp_seq=5 ttl=64 time=0.113 ms
10008 bytes from 192.168.1.27: icmp_seq=6 ttl=64 time=0.119 ms
10008 bytes from 192.168.1.27: icmp_seq=7 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.27: icmp_seq=8 ttl=64 time=0.126 ms
10008 bytes from 192.168.1.27: icmp_seq=9 ttl=64 time=0.117 ms
10008 bytes from 192.168.1.27: icmp_seq=10 ttl=64 time=0.104 ms
10008 bytes from 192.168.1.27: icmp_seq=11 ttl=64 time=0.101 ms
10008 bytes from 192.168.1.27: icmp_seq=12 ttl=64 time=0.099 ms
10008 bytes from 192.168.1.27: icmp_seq=13 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.27: icmp_seq=14 ttl=64 time=0.126 ms
10008 bytes from 192.168.1.27: icmp_seq=15 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.27: icmp_seq=16 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.27: icmp_seq=17 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.27: icmp_seq=18 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.27: icmp_seq=19 ttl=64 time=0.128 ms
10008 bytes from 192.168.1.27: icmp_seq=20 ttl=64 time=0.114 ms

--- 192.168.1.27 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19722ms
rtt min/avg/max/mdev = 0.099/0.113/0.142/0.013 ms
```
### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy1
        max # scan SSIDs: 4
        max scan IEs length: 2243 bytes
        max # sched scan SSIDs: 0
        max # match sets: 0
        max # scan plans: 1
        max scan plan interval: -1
        max scan plan iterations: 0
        Retry short limit: 7
        Retry long limit: 4
        Coverage class: 0 (up to 0m)
        Device supports T-DLS.
        Supported Ciphers:
                * WEP40 (00-0f-ac:1)
                * WEP104 (00-0f-ac:5)
                * TKIP (00-0f-ac:2)
                * CCMP-128 (00-0f-ac:4)
                * CCMP-256 (00-0f-ac:10)
                * GCMP-128 (00-0f-ac:8)
                * GCMP-256 (00-0f-ac:9)
                * CMAC (00-0f-ac:6)
                * CMAC-256 (00-0f-ac:13)
                * GMAC-128 (00-0f-ac:11)
                * GMAC-256 (00-0f-ac:12)
        Available Antennas: TX 0x3 RX 0x3
        Configured Antennas: TX 0x3 RX 0x3
        Supported interface modes:
                 * IBSS
                 * managed
                 * AP
                 * AP/VLAN
                 * monitor
                 * P2P-client
                 * P2P-GO
        Band 1:
                Capabilities: 0x196f
                        RX LDPC
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        RX STBC 1-stream
                        Max AMSDU length: 7935 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 2 usec (0x04)
                HT Max RX data rate: 300 Mbps
                HT TX/RX MCS rate indexes supported: 0-15, 32
                Bitrates (non-HT):
                        * 1.0 Mbps
                        * 2.0 Mbps
                        * 5.5 Mbps
                        * 11.0 Mbps
                        * 6.0 Mbps
                        * 9.0 Mbps
                        * 12.0 Mbps
                        * 18.0 Mbps
                        * 24.0 Mbps
                        * 36.0 Mbps
                        * 48.0 Mbps
                        * 54.0 Mbps
                Frequencies:
                        * 2412 MHz [1] (20.0 dBm)
                        * 2417 MHz [2] (20.0 dBm)
                        * 2422 MHz [3] (20.0 dBm)
                        * 2427 MHz [4] (20.0 dBm)
                        * 2432 MHz [5] (20.0 dBm)
                        * 2437 MHz [6] (20.0 dBm)
                        * 2442 MHz [7] (20.0 dBm)
                        * 2447 MHz [8] (20.0 dBm)
                        * 2452 MHz [9] (20.0 dBm)
                        * 2457 MHz [10] (20.0 dBm)
                        * 2462 MHz [11] (20.0 dBm)
                        * 2467 MHz [12] (20.0 dBm)
                        * 2472 MHz [13] (20.0 dBm)
                        * 2484 MHz [14] (disabled)
        Band 2:
                Capabilities: 0x196f
                        RX LDPC
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        RX STBC 1-stream
                        Max AMSDU length: 7935 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 2 usec (0x04)
                HT Max RX data rate: 300 Mbps
                HT TX/RX MCS rate indexes supported: 0-15, 32
                VHT Capabilities (0x03d071b2):
                        Max MPDU length: 11454
                        Supported Channel Width: neither 160 nor 80+80
                        RX LDPC
                        short GI (80 MHz)
                        TX STBC
                        SU Beamformee
                        MU Beamformee
                        +HTC-VHT
                VHT RX MCS set:
                        1 streams: MCS 0-9
                        2 streams: MCS 0-9
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT RX highest supported: 780 Mbps
                VHT TX MCS set:
                        1 streams: MCS 0-9
                        2 streams: MCS 0-9
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT TX highest supported: 780 Mbps
                Bitrates (non-HT):
                        * 6.0 Mbps
                        * 9.0 Mbps
                        * 12.0 Mbps
                        * 18.0 Mbps
                        * 24.0 Mbps
                        * 36.0 Mbps
                        * 48.0 Mbps
                        * 54.0 Mbps
                Frequencies:
                        * 5180 MHz [36] (23.0 dBm)
                        * 5200 MHz [40] (23.0 dBm)
                        * 5220 MHz [44] (23.0 dBm)
                        * 5240 MHz [48] (23.0 dBm)
                        * 5260 MHz [52] (23.0 dBm) (radar detection)
                        * 5280 MHz [56] (23.0 dBm) (radar detection)
                        * 5300 MHz [60] (23.0 dBm) (radar detection)
                        * 5320 MHz [64] (23.0 dBm) (radar detection)
                        * 5500 MHz [100] (disabled)
                        * 5520 MHz [104] (disabled)
                        * 5540 MHz [108] (disabled)
                        * 5560 MHz [112] (disabled)
                        * 5580 MHz [116] (disabled)
                        * 5600 MHz [120] (disabled)
                        * 5620 MHz [124] (disabled)
                        * 5640 MHz [128] (disabled)
                        * 5660 MHz [132] (disabled)
                        * 5680 MHz [136] (disabled)
                        * 5700 MHz [140] (disabled)
                        * 5720 MHz [144] (disabled)
                        * 5745 MHz [149] (30.0 dBm)
                        * 5765 MHz [153] (30.0 dBm)
                        * 5785 MHz [157] (30.0 dBm)
                        * 5805 MHz [161] (30.0 dBm)
                        * 5825 MHz [165] (30.0 dBm)
        Supported commands:
                 * new_interface
                 * set_interface
                 * new_key
                 * start_ap
                 * new_station
                 * set_bss
                 * authenticate
                 * associate
                 * deauthenticate
                 * disassociate
                 * join_ibss
                 * set_tx_bitrate_mask
                 * frame
                 * frame_wait_cancel
                 * set_wiphy_netns
                 * set_channel
                 * set_wds_peer
                 * tdls_mgmt
                 * tdls_oper
                 * probe_client
                 * set_noack_map
                 * register_beacons
                 * start_p2p_device
                 * set_mcast_rate
                 * connect
                 * disconnect
                 * set_qos_map
                 * set_multicast_to_unicast
        Supported TX frame types:
                 * IBSS: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * managed: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * AP: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * AP/VLAN: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * mesh point: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * P2P-client: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * P2P-GO: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
                 * P2P-device: 0x00 0x10 0x20 0x30 0x40 0x50 0x60 0x70 0x80 0x90 0xa0 0xb0 0xc0 0xd0 0xe0 0xf0
        Supported RX frame types:
                 * IBSS: 0x40 0xb0 0xc0 0xd0
                 * managed: 0x40 0xd0
                 * AP: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * AP/VLAN: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * mesh point: 0xb0 0xc0 0xd0
                 * P2P-client: 0x40 0xd0
                 * P2P-GO: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * P2P-device: 0x40 0xd0
        software interface modes (can always be added):
                 * AP/VLAN
                 * monitor
        valid interface combinations:
                 * #{ managed } <= 1, #{ AP, P2P-client, P2P-GO } <= 1,
                   total <= 2, #channels <= 1
        HT Capability overrides:
                 * MCS: ff ff ff ff ff ff ff ff ff ff
                 * maximum A-MSDU length
                 * supported channel width
                 * short GI for 40 MHz
                 * max A-MPDU length exponent
                 * min MPDU start spacing
        Device supports TX status socket option.
        Device supports HT-IBSS.
        Device supports SAE with AUTHENTICATE command
        Device supports scan flush.
        Device supports per-vif TX power setting
        Driver supports full state transitions for AP/GO clients
        Driver supports a userspace MPM
        Device supports configuring vdev MAC-addr on create.
```

</details>

### iwconfig

```
wlan0     IEEE 802.11  ESSID:""
          Mode:Managed  Frequency:5.745 GHz  Access Point: F8:6F:B0:0E:AE:E6
          Bit Rate=351 Mb/s   Tx-Power=30 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=58/70  Signal level=-52 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:38   Missed beacon:0
```
### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 52012
[  5] local 192.168.1.27 port 5201 connected to 192.168.1.3 port 52013
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  14.5 MBytes   122 Mbits/sec  114    422 KBytes
[  5]   1.00-2.00   sec  15.8 MBytes   133 Mbits/sec    0    472 KBytes
[  5]   2.00-3.00   sec  16.7 MBytes   140 Mbits/sec    0    502 KBytes
[  5]   3.00-4.00   sec  16.1 MBytes   134 Mbits/sec    0    522 KBytes
[  5]   4.00-5.00   sec  14.8 MBytes   124 Mbits/sec    0    530 KBytes
[  5]   5.00-6.00   sec  16.4 MBytes   138 Mbits/sec    0    533 KBytes
[  5]   6.00-7.00   sec  16.7 MBytes   140 Mbits/sec    0    533 KBytes
[  5]   7.00-8.00   sec  16.9 MBytes   142 Mbits/sec    0    556 KBytes
[  5]   8.00-9.00   sec  16.7 MBytes   140 Mbits/sec    0    577 KBytes
[  5]   9.00-10.00  sec  16.4 MBytes   138 Mbits/sec    0    597 KBytes
[  5]  10.00-11.00  sec  15.8 MBytes   133 Mbits/sec    0    615 KBytes
[  5]  11.00-12.00  sec  16.4 MBytes   137 Mbits/sec    0    629 KBytes
[  5]  12.00-13.00  sec  16.5 MBytes   139 Mbits/sec    0    667 KBytes
[  5]  13.00-14.00  sec  15.7 MBytes   131 Mbits/sec    0    733 KBytes
[  5]  14.00-15.00  sec  15.9 MBytes   134 Mbits/sec    0    826 KBytes
[  5]  15.00-16.00  sec  17.2 MBytes   144 Mbits/sec    0    941 KBytes
[  5]  16.00-17.00  sec  14.3 MBytes   120 Mbits/sec    0    941 KBytes
[  5]  17.00-18.00  sec  14.1 MBytes   118 Mbits/sec    0   1.21 MBytes
[  5]  18.00-19.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  19.00-20.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  20.00-21.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  21.00-22.00  sec  17.5 MBytes   147 Mbits/sec    0   1.21 MBytes
[  5]  22.00-23.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  23.00-24.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  24.00-25.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  25.00-26.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  26.00-27.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  27.00-28.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  28.00-29.00  sec  17.5 MBytes   147 Mbits/sec    0   1.21 MBytes
[  5]  29.00-30.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  30.00-31.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  31.00-32.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  32.00-33.00  sec  17.5 MBytes   147 Mbits/sec    0   1.21 MBytes
[  5]  33.00-34.00  sec  15.0 MBytes   126 Mbits/sec    0   1.21 MBytes
[  5]  34.00-35.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  35.00-36.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  36.00-37.00  sec  17.5 MBytes   146 Mbits/sec    0   1.21 MBytes
[  5]  37.00-38.00  sec  16.2 MBytes   137 Mbits/sec    0   1.21 MBytes
[  5]  38.00-39.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  39.00-40.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  40.00-41.00  sec  17.5 MBytes   147 Mbits/sec    0   1.21 MBytes
[  5]  41.00-42.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  42.00-43.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  43.00-44.00  sec  17.5 MBytes   147 Mbits/sec    0   1.21 MBytes
[  5]  44.00-45.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  45.00-46.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  46.00-47.00  sec  15.0 MBytes   126 Mbits/sec    0   1.21 MBytes
[  5]  47.00-48.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  48.00-49.00  sec  16.2 MBytes   136 Mbits/sec    0   1.21 MBytes
[  5]  49.00-50.00  sec  17.5 MBytes   146 Mbits/sec    0   1.21 MBytes
[  5]  50.00-51.00  sec  11.2 MBytes  94.5 Mbits/sec    0   1.21 MBytes
[  5]  51.00-52.00  sec  13.7 MBytes   115 Mbits/sec    0   1.21 MBytes
[  5]  52.00-53.00  sec  13.8 MBytes   115 Mbits/sec    0   1.21 MBytes
[  5]  53.00-54.00  sec  13.8 MBytes   115 Mbits/sec    0   1.21 MBytes
[  5]  53.00-54.00  sec  13.8 MBytes   115 Mbits/sec    0   1.21 MBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-54.00  sec   878 MBytes   136 Mbits/sec  114             sender
[  5]   0.00-54.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>

### AP Test

#### hostapd.conf

Setup the configuration at /etc/hostapd/hostapd.conf

```
interface=wlan0
driver=nl80211
ieee80211n=1
hw_mode=g
channel=6
ssid=AP-TEST
wpa=2
wpa_passphrase=12345678
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP TKIP
wpa_pairwise=TKIP CCMP
```

#### udhcpd.conf

```
start 192.168.175.2
end 192.168.175.254
interface wlan0
max_leases 234
opt router 192.168.175.1
```

#### Start AP Test
```
sudo hostapd -dd -e /dev/urandom /etc/hostapd/hostapd.conf -B
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr  and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)
<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 52044
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 52045
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.02 MBytes  16.9 Mbits/sec    0    264 KBytes
[  5]   1.00-2.00   sec  2.14 MBytes  18.0 Mbits/sec    9    207 KBytes
[  5]   2.00-3.00   sec  2.14 MBytes  18.0 Mbits/sec    1   1.43 KBytes
[  5]   3.00-4.00   sec  1004 KBytes  8.22 Mbits/sec   52    230 KBytes
[  5]   4.00-5.00   sec  2.27 MBytes  19.0 Mbits/sec    0    230 KBytes
[  5]   5.00-6.00   sec  3.37 MBytes  28.3 Mbits/sec    0    230 KBytes
[  5]   6.00-7.00   sec  2.94 MBytes  24.7 Mbits/sec    0    230 KBytes
[  5]   7.00-8.00   sec  2.70 MBytes  22.6 Mbits/sec    0    230 KBytes
[  5]   8.00-9.00   sec  2.45 MBytes  20.6 Mbits/sec    0    230 KBytes
[  5]   9.00-10.00  sec   376 KBytes  3.08 Mbits/sec    1    230 KBytes
[  5]  10.00-11.00  sec  2.27 MBytes  19.0 Mbits/sec    0    259 KBytes
[  5]  11.00-12.00  sec  3.12 MBytes  26.2 Mbits/sec    0    259 KBytes
[  5]  12.00-13.00  sec  3.49 MBytes  29.3 Mbits/sec    0    259 KBytes
[  5]  13.00-14.00  sec  3.12 MBytes  26.2 Mbits/sec    6    259 KBytes
[  5]  14.00-15.00  sec  2.88 MBytes  24.1 Mbits/sec    2    234 KBytes
[  5]  15.00-16.00  sec  3.31 MBytes  27.8 Mbits/sec    2    214 KBytes
[  5]  16.00-17.00  sec  3.12 MBytes  26.2 Mbits/sec    0    240 KBytes
[  5]  17.00-18.00  sec  3.37 MBytes  28.2 Mbits/sec    0    254 KBytes
[  5]  18.00-19.00  sec  2.51 MBytes  21.1 Mbits/sec    0    258 KBytes
[  5]  19.00-20.00  sec  3.12 MBytes  26.2 Mbits/sec    0    258 KBytes
[  5]  20.00-21.00  sec  2.63 MBytes  22.1 Mbits/sec    7    192 KBytes
[  5]  21.00-22.00  sec   627 KBytes  5.14 Mbits/sec    0    204 KBytes
[  5]  22.00-23.00  sec  2.70 MBytes  22.6 Mbits/sec    0    217 KBytes
[  5]  23.00-24.00  sec  2.21 MBytes  18.5 Mbits/sec    4    218 KBytes
[  5]  24.00-25.00  sec  1.29 MBytes  10.8 Mbits/sec    4    221 KBytes
[  5]  25.00-26.00  sec  2.51 MBytes  21.1 Mbits/sec    0    161 KBytes
[  5]  26.00-27.00  sec  2.02 MBytes  17.0 Mbits/sec    0    185 KBytes
[  5]  27.00-28.00  sec  2.14 MBytes  18.0 Mbits/sec    0    215 KBytes
[  5]  28.00-29.00  sec  3.31 MBytes  27.8 Mbits/sec    0    225 KBytes
[  5]  29.00-30.00  sec  1.84 MBytes  15.4 Mbits/sec    0    228 KBytes
[  5]  30.00-31.00  sec  1.16 MBytes  9.77 Mbits/sec    0    228 KBytes
[  5]  31.00-32.00  sec  2.33 MBytes  19.5 Mbits/sec    0    228 KBytes
[  5]  32.00-33.00  sec  3.25 MBytes  27.2 Mbits/sec    0    232 KBytes
[  5]  33.00-34.00  sec  0.00 Bytes  0.00 bits/sec    1   1.43 KBytes
[  5]  34.00-35.00  sec  1.78 MBytes  14.9 Mbits/sec    6    201 KBytes
[  5]  35.00-36.00  sec  3.31 MBytes  27.8 Mbits/sec    0    241 KBytes
[  5]  36.00-37.00  sec  2.51 MBytes  21.1 Mbits/sec    0    267 KBytes
[  5]  37.00-38.00  sec  2.27 MBytes  19.0 Mbits/sec    0    281 KBytes
[  5]  38.00-39.00  sec  3.68 MBytes  30.8 Mbits/sec    0    287 KBytes
[  5]  39.00-40.00  sec  3.37 MBytes  28.3 Mbits/sec    0    288 KBytes
[  5]  40.00-41.00  sec  3.98 MBytes  33.4 Mbits/sec   61    288 KBytes
[  5]  41.00-42.00  sec  3.86 MBytes  32.4 Mbits/sec    0    288 KBytes
[  5]  42.00-43.00  sec  3.49 MBytes  29.3 Mbits/sec    0    288 KBytes
[  5]  43.00-44.00  sec  3.74 MBytes  31.3 Mbits/sec    2    288 KBytes
[  5]  44.00-45.00  sec  4.04 MBytes  33.9 Mbits/sec    0    288 KBytes
[  5]  45.00-46.00  sec  4.04 MBytes  33.9 Mbits/sec    0    288 KBytes
[  5]  46.00-47.00  sec  3.92 MBytes  32.9 Mbits/sec    0    288 KBytes
[  5]  47.00-48.00  sec  3.43 MBytes  28.8 Mbits/sec    0    288 KBytes
[  5]  48.00-49.00  sec  3.49 MBytes  29.3 Mbits/sec   49    288 KBytes
[  5]  49.00-50.00  sec  4.59 MBytes  38.5 Mbits/sec    0    288 KBytes
[  5]  50.00-51.00  sec  4.78 MBytes  40.1 Mbits/sec    0    288 KBytes
[  5]  51.00-52.00  sec  4.10 MBytes  34.4 Mbits/sec    0    288 KBytes
[  5]  52.00-53.00  sec  4.41 MBytes  37.0 Mbits/sec    0    288 KBytes
[  5]  53.00-54.00  sec  4.47 MBytes  37.5 Mbits/sec    0    288 KBytes
[  5]  53.00-54.00  sec  4.47 MBytes  37.5 Mbits/sec    0    288 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-54.00  sec   155 MBytes  24.0 Mbits/sec  207             sender
[  5]   0.00-54.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
