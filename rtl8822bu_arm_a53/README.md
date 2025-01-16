# RTL8822BU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/c12ba077-8607-4d30-9a82-540f9692712e" height="400"/>|<img src="https://github.com/user-attachments/assets/98e43c49-fd6d-4d87-bd60-61dbdfaf872b" height="400"/>|

```
Architecture:        aarch64
Byte Order:          Little Endian
CPU(s):              2
On-line CPU(s) list: 0,1
Thread(s) per core:  1
Core(s) per socket:  2
Socket(s):           1
Vendor ID:           ARM
Model:               4
Model name:          Cortex-A53
Stepping:            r0p4
CPU max MHz:         1199.9990
CPU min MHz:         299.9990
BogoMIPS:            66.66
Flags:               fp asimd aes pmull sha1 sha2 crc32 cpuid
```

### USB Tree

```
[    6.152970] usb 1-1.1: New USB device found, idVendor=0bda, idProduct=b82c, bcdDevice= 2.10
[    6.161318] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[    6.168621] usb 1-1.1: Product: 802.11ac NIC
[    6.172881] usb 1-1.1: Manufacturer: Realtek
[    6.177143] usb 1-1.1: SerialNumber: 123456


/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=, 480M

After driver is inserted.

/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
        |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 5000M
        |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 5000M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=rtw_8822bu, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 002 Device 003: ID 0bda:b82c Realtek Semiconductor Corp.
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               3.00
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2 ?
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0         9
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xb82c
  bcdDevice            3.00
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength          349
    bNumInterfaces          3
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0x80
      (Bus Powered)
    MaxPower              126mA
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
        bMaxBurst               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x02  EP 2 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               3
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x82  EP 2 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               3
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        bMaxBurst               0
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
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               3
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x05  EP 5 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               3
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x06  EP 6 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               3
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
        bMaxBurst               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x08  EP 8 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               3
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[   49.038749] rtw_core: loading out-of-tree module taints kernel.
[   57.830748] rtw_8822bu 1-1.1:1.2: Firmware version 30.20.0, H2C version 14
[   58.449269] rtw_8822bu 1-1.1:1.2: write register 0xc4 failed with -71
[   58.455758] rtw_8822bu 1-1.1:1.2: rtw_usb_reg_sec: reg 0x4e0, usb write 1 fail, status: -71
[   58.464368] usbcore: registered new interface driver rtw_8822bu
[   58.549550] usb 1-1.1: USB disconnect, device number 3
[   58.878246] usb 2-1.1: new SuperSpeed Gen 1 USB device number 3 using xhci-hcd
[   58.898471] usb 2-1.1: config 1 interface 1 altsetting 0 endpoint 0x3 has wMaxPacketSize 0, skipping
[   58.898478] usb 2-1.1: config 1 interface 1 altsetting 0 endpoint 0x83 has wMaxPacketSize 0, skipping
[   58.898685] usb 2-1.1: New USB device found, idVendor=0bda, idProduct=b82c, bcdDevice= 3.00
[   58.898691] usb 2-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[   58.898695] usb 2-1.1: Product: 802.11ac NIC
[   58.898700] usb 2-1.1: Manufacturer: Realtek
[   58.898704] usb 2-1.1: SerialNumber: 123456
[   58.934611] rtw_8822bu 2-1.1:1.2: Firmware version 30.20.0, H2C version 14
[   58.957768] random: crng init done
[   58.957773] random: 7 urandom warning(s) missed due to ratelimiting
[   59.171920] Bluetooth: hci0: RTL: examining hci_ver=07 hci_rev=000b lmp_ver=07 lmp_subver=8822
[   59.172880] Bluetooth: hci0: RTL: rom_version status=0 version=2
[   59.172885] Bluetooth: hci0: RTL: loading rtl_bt/rtl8822b_fw.bin
[   59.173059] Bluetooth: hci0: RTL: loading rtl_bt/rtl8822b_config.bin
[   59.173147] Bluetooth: hci0: RTL: cfg_sz 14, total sz 20270
[   59.915888] Bluetooth: hci0: RTL: fw version 0xab6b705c
[   65.018054] wlan0: authenticate with 
[   65.770348] wlan0: send auth to  (try 1/3)
[   65.771865] wlan0: authenticated
[   65.774198] wlan0: associate with  (try 1/3)
[   65.821185] wlan0: RX AssocResp from  (capab=0x1011 status=0 aid=3)
[   65.831956] wlan0: associated
[   65.848517] wlan0: Limiting TX power to 35 (35 - 0) dBm as advertised by 
[   65.853239] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready

Module                  Size  Used by
rtw_8822bu             16384  0
rtw_8822b             221184  1 rtw_8822bu
rtw_usb                24576  1 rtw_8822bu
rtw_core              208896  2 rtw_usb,rtw_8822b
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.27  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 83  bytes 10809 (10.8 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 28  bytes 3127 (3.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     5.48 ms   (jitter: 5.62ms, low: 3.38ms, high: 12.33ms)
    Download:   196.88 Mbps (data used: 252.6 MB)
                 12.26 ms   (jitter: 9.70ms, low: 7.01ms, high: 245.60ms)
      Upload:   207.23 Mbps (data used: 108.2 MB)
                 47.67 ms   (jitter: 22.86ms, low: 5.29ms, high: 200.28ms)
```

### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=3.74 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=3.90 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.50 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=8.25 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=16.2 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=8.90 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=3.76 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=10.2 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=3.48 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=3.55 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=3.50 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=3.46 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=5.88 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=4.14 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=15.0 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=22.9 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=3.51 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=3.60 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=6.21 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=4.05 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19031ms
rtt min/avg/max/mdev = 3.469/6.897/22.960/5.263 ms
```

#### Self-Ping 

```
PING 192.168.1.27 (192.168.1.27) 10000(10028) bytes of data.
10008 bytes from 192.168.1.27: icmp_seq=1 ttl=64 time=0.106 ms
10008 bytes from 192.168.1.27: icmp_seq=2 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.27: icmp_seq=3 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=4 ttl=64 time=0.071 ms
10008 bytes from 192.168.1.27: icmp_seq=5 ttl=64 time=0.065 ms
10008 bytes from 192.168.1.27: icmp_seq=6 ttl=64 time=0.072 ms
10008 bytes from 192.168.1.27: icmp_seq=7 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=8 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.27: icmp_seq=9 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=10 ttl=64 time=0.078 ms
10008 bytes from 192.168.1.27: icmp_seq=11 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.27: icmp_seq=12 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.27: icmp_seq=13 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.27: icmp_seq=14 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=15 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=16 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=17 ttl=64 time=0.072 ms
10008 bytes from 192.168.1.27: icmp_seq=18 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.27: icmp_seq=19 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.27: icmp_seq=20 ttl=64 time=0.060 ms

--- 192.168.1.27 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19433ms
rtt min/avg/max/mdev = 0.060/0.065/0.106/0.014 ms
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
                        * 5180 MHz [36] (20.0 dBm) (radar detection)
                        * 5200 MHz [40] (20.0 dBm) (radar detection)
                        * 5220 MHz [44] (20.0 dBm) (radar detection)
                        * 5240 MHz [48] (20.0 dBm) (radar detection)
                        * 5260 MHz [52] (20.0 dBm) (radar detection)
                        * 5280 MHz [56] (20.0 dBm) (radar detection)
                        * 5300 MHz [60] (20.0 dBm) (radar detection)
                        * 5320 MHz [64] (20.0 dBm) (radar detection)
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
                        * 5745 MHz [149] (33.0 dBm)
                        * 5765 MHz [153] (33.0 dBm)
                        * 5785 MHz [157] (33.0 dBm)
                        * 5805 MHz [161] (33.0 dBm)
                        * 5825 MHz [165] (33.0 dBm)
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
                 * testmode
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
          Mode:Managed  Frequency:5.745 GHz  Access Point: 
          Bit Rate=351 Mb/s   Tx-Power=33 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=49/70  Signal level=-61 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```
### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 54881
[  5] local 192.168.1.27 port 5201 connected to 192.168.1.3 port 54882
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  15.3 MBytes   129 Mbits/sec    0    262 KBytes
[  5]   1.00-2.00   sec  15.7 MBytes   132 Mbits/sec    0    533 KBytes
[  5]   2.00-3.00   sec  16.2 MBytes   136 Mbits/sec    0    533 KBytes
[  5]   3.00-4.00   sec  14.5 MBytes   122 Mbits/sec    0    533 KBytes
[  5]   4.00-5.00   sec  14.6 MBytes   122 Mbits/sec    0    533 KBytes
[  5]   5.00-6.00   sec  15.0 MBytes   125 Mbits/sec    0    533 KBytes
[  5]   6.00-7.00   sec  12.3 MBytes   103 Mbits/sec    0    533 KBytes
[  5]   7.00-8.00   sec  14.5 MBytes   122 Mbits/sec    0    533 KBytes
[  5]   8.00-9.00   sec  15.5 MBytes   130 Mbits/sec    0    533 KBytes
[  5]   9.00-10.00  sec  14.4 MBytes   121 Mbits/sec    0    533 KBytes
[  5]  10.00-11.00  sec  16.5 MBytes   139 Mbits/sec    0    533 KBytes
[  5]  11.00-12.00  sec  13.5 MBytes   114 Mbits/sec    0    533 KBytes
[  5]  12.00-13.00  sec  13.5 MBytes   113 Mbits/sec    0    533 KBytes
[  5]  13.00-14.00  sec  15.3 MBytes   129 Mbits/sec    0    533 KBytes
[  5]  14.00-15.00  sec  14.6 MBytes   122 Mbits/sec    0    533 KBytes
[  5]  15.00-16.00  sec  15.7 MBytes   132 Mbits/sec    0    533 KBytes
[  5]  16.00-17.00  sec  13.4 MBytes   113 Mbits/sec    0    533 KBytes
[  5]  17.00-18.00  sec  14.2 MBytes   119 Mbits/sec    0    533 KBytes
[  5]  18.00-19.00  sec  16.8 MBytes   141 Mbits/sec    0    533 KBytes
[  5]  19.00-20.00  sec  14.6 MBytes   123 Mbits/sec    0    533 KBytes
[  5]  20.00-21.00  sec  16.8 MBytes   141 Mbits/sec    0    533 KBytes
[  5]  21.00-22.00  sec  14.6 MBytes   123 Mbits/sec    0    533 KBytes
[  5]  22.00-23.00  sec  15.8 MBytes   133 Mbits/sec    0    533 KBytes
[  5]  23.00-24.00  sec  16.9 MBytes   142 Mbits/sec    0    533 KBytes
[  5]  24.00-25.00  sec  14.9 MBytes   125 Mbits/sec    0    533 KBytes
[  5]  25.00-26.00  sec  15.6 MBytes   131 Mbits/sec    0    533 KBytes
[  5]  26.00-27.00  sec  14.6 MBytes   123 Mbits/sec    0    533 KBytes
[  5]  27.00-28.00  sec  16.7 MBytes   140 Mbits/sec    0    533 KBytes
[  5]  28.00-29.00  sec  14.6 MBytes   122 Mbits/sec    0    533 KBytes
[  5]  29.00-30.00  sec  15.6 MBytes   131 Mbits/sec    0    533 KBytes
[  5]  30.00-31.00  sec  17.0 MBytes   142 Mbits/sec    0    533 KBytes
[  5]  31.00-32.00  sec  15.4 MBytes   129 Mbits/sec    0    533 KBytes
[  5]  32.00-33.00  sec  15.5 MBytes   130 Mbits/sec    0    533 KBytes
[  5]  33.00-34.00  sec  15.4 MBytes   130 Mbits/sec    0    533 KBytes
[  5]  34.00-35.00  sec  15.5 MBytes   130 Mbits/sec    0   1.30 MBytes
[  5]  35.00-36.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  36.00-37.00  sec  13.8 MBytes   115 Mbits/sec    0   1.30 MBytes
[  5]  37.00-38.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  38.00-39.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  39.00-40.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  40.00-41.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  41.00-42.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  42.00-43.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  43.00-44.00  sec  13.8 MBytes   115 Mbits/sec    0   1.30 MBytes
[  5]  44.00-45.00  sec  11.2 MBytes  94.4 Mbits/sec    0   1.30 MBytes
[  5]  45.00-46.00  sec  12.5 MBytes   105 Mbits/sec    0   1.30 MBytes
[  5]  46.00-47.00  sec  12.5 MBytes   105 Mbits/sec    0   1.30 MBytes
[  5]  47.00-48.00  sec  13.8 MBytes   115 Mbits/sec    0   1.30 MBytes
[  5]  48.00-49.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  49.00-50.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  50.00-51.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  51.00-52.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  52.00-53.00  sec  11.2 MBytes  94.4 Mbits/sec    0   1.30 MBytes
[  5]  53.00-54.00  sec  15.0 MBytes   126 Mbits/sec    0   1.30 MBytes
[  5]  54.00-55.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  55.00-56.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  56.00-57.00  sec  16.2 MBytes   136 Mbits/sec    0   1.30 MBytes
[  5]  57.00-58.00  sec  15.0 MBytes   126 Mbits/sec  472    934 KBytes
[  5]  58.00-59.00  sec  16.2 MBytes   136 Mbits/sec    0   1.02 MBytes
[  5]  59.00-60.00  sec  16.2 MBytes   136 Mbits/sec    0   1.02 MBytes
[  5]  60.00-61.00  sec  12.5 MBytes   105 Mbits/sec    0   1.02 MBytes
[  5]  61.00-62.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.02 MBytes
[  5]  62.00-63.00  sec  8.75 MBytes  73.4 Mbits/sec    0   1.02 MBytes
[  5]  63.00-64.00  sec  8.75 MBytes  73.4 Mbits/sec    0   1.02 MBytes
[  5]  64.00-65.00  sec  10.0 MBytes  83.9 Mbits/sec    0   1.02 MBytes
[  5]  65.00-66.00  sec  10.0 MBytes  83.9 Mbits/sec    0   1.02 MBytes
[  5]  66.00-67.00  sec  10.0 MBytes  83.9 Mbits/sec    0   1.02 MBytes
[  5]  67.00-68.00  sec  12.5 MBytes   105 Mbits/sec    0   1.02 MBytes
[  5]  68.00-69.00  sec  16.2 MBytes   136 Mbits/sec    0   1.02 MBytes
[  5]  69.00-70.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.02 MBytes
[  5]  70.00-71.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.02 MBytes
[  5]  71.00-72.00  sec  10.0 MBytes  83.9 Mbits/sec    0   1.02 MBytes
[  5]  72.00-73.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.02 MBytes
[  5]  72.00-73.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.02 MBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-73.00  sec  1.01 GBytes   119 Mbits/sec  472             sender
[  5]   0.00-73.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
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
Accepted connection from 192.168.175.86, port 54923
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 54924
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.46 MBytes  20.7 Mbits/sec    7   97.0 KBytes
[  5]   1.00-2.00   sec  2.27 MBytes  19.0 Mbits/sec    0    111 KBytes
[  5]   2.00-3.00   sec  3.12 MBytes  26.2 Mbits/sec    0    131 KBytes
[  5]   3.00-4.00   sec  2.88 MBytes  24.2 Mbits/sec    0    131 KBytes
[  5]   4.00-5.00   sec  3.12 MBytes  26.2 Mbits/sec    1    131 KBytes
[  5]   5.00-6.00   sec  1.84 MBytes  15.4 Mbits/sec    1    104 KBytes
[  5]   6.00-7.00   sec  2.94 MBytes  24.7 Mbits/sec    9   95.5 KBytes
[  5]   7.00-8.00   sec  2.21 MBytes  18.5 Mbits/sec    0    113 KBytes
[  5]   8.00-9.00   sec  2.70 MBytes  22.6 Mbits/sec    0    131 KBytes
[  5]   9.00-10.00  sec  2.51 MBytes  21.1 Mbits/sec    0    144 KBytes
[  5]  10.00-11.00  sec  3.68 MBytes  30.8 Mbits/sec    0    161 KBytes
[  5]  11.00-12.00  sec  2.02 MBytes  17.0 Mbits/sec    0    170 KBytes
[  5]  12.00-13.00  sec  3.00 MBytes  25.2 Mbits/sec    0    185 KBytes
[  5]  13.00-14.00  sec  2.45 MBytes  20.6 Mbits/sec    1    145 KBytes
[  5]  14.00-15.00  sec  2.51 MBytes  21.1 Mbits/sec    0    167 KBytes
[  5]  15.00-16.00  sec  2.88 MBytes  24.2 Mbits/sec    0    181 KBytes
[  5]  16.00-17.00  sec  1.59 MBytes  13.4 Mbits/sec    0    188 KBytes
[  5]  17.00-18.00  sec  3.31 MBytes  27.8 Mbits/sec    0    188 KBytes
[  5]  18.00-19.00  sec  3.31 MBytes  27.8 Mbits/sec    0    195 KBytes
[  5]  19.00-20.00  sec  2.88 MBytes  24.2 Mbits/sec    0    210 KBytes
[  5]  20.00-21.00  sec  2.45 MBytes  20.6 Mbits/sec    3    210 KBytes
[  656.616084] rtw_8822bu 2-1.1:1.2: error beacon valid
[  656.621128] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  656.627318] rtw_8822bu 2-1.1:1.2: failed to download beacon
[  656.691399] rtw_8822bu 2-1.1:1.2: error beacon valid
[  656.696430] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  656.702610] rtw_8822bu 2-1.1:1.2: failed to download beacon
[  656.795417] rtw_8822bu 2-1.1:1.2: error beacon valid
[  656.800444] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  656.855535] rtw_8822bu 2-1.1:1.2: error beacon valid
[  656.860571] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  21.00-22.00  sec  2.51 MBytes  21.1 Mbits/sec    0    210 KBytes
[  5]  22.00-23.00  sec  4.04 MBytes  33.9 Mbits/sec    0    210 KBytes
[  5]  23.00-24.00  sec  3.74 MBytes  31.3 Mbits/sec    0    210 KBytes
[  5]  24.00-25.00  sec  3.86 MBytes  32.4 Mbits/sec    0    210 KBytes
[  5]  25.00-26.00  sec  3.92 MBytes  32.9 Mbits/sec    0    217 KBytes
[  5]  26.00-27.00  sec  4.04 MBytes  33.9 Mbits/sec    0    231 KBytes
[  5]  27.00-28.00  sec  4.53 MBytes  38.0 Mbits/sec    0    245 KBytes
[  5]  28.00-29.00  sec  3.86 MBytes  32.4 Mbits/sec    0    257 KBytes
[  665.504238] rtw_8822bu 2-1.1:1.2: error beacon valid
[  665.509272] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  29.00-30.00  sec  3.49 MBytes  29.3 Mbits/sec    0    258 KBytes
[  665.558084] rtw_8822bu 2-1.1:1.2: error beacon valid
[  665.563990] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  30.00-31.00  sec  4.04 MBytes  33.9 Mbits/sec    0    258 KBytes
[  666.983396] rtw_8822bu 2-1.1:1.2: error beacon valid
[  666.988430] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  667.039340] rtw_8822bu 2-1.1:1.2: error beacon valid
[  667.044406] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  667.095706] rtw_8822bu 2-1.1:1.2: error beacon valid
[  667.100916] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  667.150834] rtw_8822bu 2-1.1:1.2: error beacon valid
[  667.156015] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  667.205353] rtw_8822bu 2-1.1:1.2: error beacon valid
[  667.211386] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  31.00-32.00  sec  2.82 MBytes  23.6 Mbits/sec    2    258 KBytes
[  668.498983] rtw_8822bu 2-1.1:1.2: error beacon valid
[  668.504016] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  32.00-33.00  sec  3.92 MBytes  32.9 Mbits/sec    0    258 [  668.555615] rtw_8822bu 2-1.1:1.2: error beacon valid
KBytes
[  668.562811] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  669.139651] rtw_8822bu 2-1.1:1.2: error beacon valid
[  669.145171] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  669.195020] rtw_8822bu 2-1.1:1.2: error beacon valid
[  669.200241] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  33.00-34.00  sec  4.04 MBytes  33.9 Mbits/sec    0    191 KBytes
[  5]  34.00-35.00  sec  4.29 MBytes  36.0 Mbits/sec    0    225 KBytes
[  671.242816] rtw_8822bu 2-1.1:1.2: error beacon valid
[  671.247956] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  671.299373] rtw_8822bu 2-1.1:1.2: error beacon valid
[  671.304520] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  35.00-36.00  sec  4.23 MBytes  35.5 Mbits/sec    0    245 KBytes
[  671.631606] rtw_8822bu 2-1.1:1.2: error beacon valid
[  671.636708] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  671.687805] rtw_8822bu 2-1.1:1.2: error beacon valid
[  671.692837] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  36.00-37.00  sec  4.66 MBytes  39.1 Mbits/sec    0    255 KBytes
[  672.645151] rtw_8822bu 2-1.1:1.2: error beacon valid
[  672.650188] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  672.700110] rtw_8822bu 2-1.1:1.2: error beacon valid
[  672.706207] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  37.00-38.00  sec  4.96 MBytes  41.6 Mbits/sec    1    258 KBytes
[  673.601825] rtw_8822bu 2-1.1:1.2: error beacon valid
[  673.607039] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  673.657829] rtw_8822bu 2-1.1:1.2: error beacon valid
[  673.662857] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  673.858173] rtw_8822bu 2-1.1:1.2: error beacon valid
[  673.863311] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  673.915451] rtw_8822bu 2-1.1:1.2: error beacon valid
[  673.920576] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  38.00-39.00  sec  4.10 MBytes  34.4 Mbits/sec    0    258 KBytes
[  674.631298] rtw_8822bu 2-1.1:1.2: error beacon valid
[  674.636711] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  674.687676] rtw_8822bu 2-1.1:1.2: error beacon valid
[  674.692813] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  674.743559] rtw_8822bu 2-1.1:1.2: error beacon valid
[  674.748702] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  39.00-40.00  sec  4.29 MBytes  36.0 Mbits/sec    3    212 KBytes
[  676.024685] rtw_8822bu 2-1.1:1.2: error beacon valid
[  676.029780] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  676.079596] rtw_8822bu 2-1.1:1.2: error beacon valid
[  676.084677] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  676.161644] rtw_8822bu 2-1.1:1.2: error beacon valid
[  676.166674] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  676.218014] rtw_8822bu 2-1.1:1.2: error beacon valid
[  676.223286] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  676.276341] rtw_8822bu 2-1.1:1.2: error beacon valid
[  676.281529] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  40.00-41.00  sec  3.43 MBytes  28.8 Mbits/sec    0    238 KBytes
[  5]  41.00-42.00  sec  4.29 MBytes  36.0 Mbits/sec    0    251 KBytes
[  677.808088] rtw_8822bu 2-1.1:1.2: error beacon valid
[  677.814580] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  677.864460] rtw_8822bu 2-1.1:1.2: error beacon valid
[  677.870819] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  42.00-43.00  sec  4.29 MBytes  36.0 Mbits/sec    2    254 KBytes
[  678.706307] rtw_8822bu 2-1.1:1.2: error beacon valid
[  678.711349] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  678.761321] rtw_8822bu 2-1.1:1.2: error beacon valid
[  678.766352] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  678.830656] rtw_8822bu 2-1.1:1.2: error beacon valid
[  678.835687] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  678.885214] rtw_8822bu 2-1.1:1.2: error beacon valid
[  678.890244] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  678.939703] rtw_8822bu 2-1.1:1.2: error beacon valid
[  678.944734] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  678.995289] rtw_8822bu 2-1.1:1.2: error beacon valid
[  679.000322] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  43.00-44.00  sec  2.82 MBytes  23.6 Mbits/sec    0    254 KBytes
[  679.721928] rtw_8822bu 2-1.1:1.2: error beacon valid
[  679.726962] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  679.779476] rtw_8822bu 2-1.1:1.2: error beacon valid
[  679.784695] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  680.103521] rtw_8822bu 2-1.1:1.2: error beacon valid
[  680.108580] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  680.160931] rtw_8822bu 2-1.1:1.2: error beacon valid
[  680.166150] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  44.00-45.00  sec  4.17 MBytes  34.9 Mbits/sec    0    254 KBytes
[  680.999185] rtw_8822bu 2-1.1:1.2: error beacon valid
[  681.004216] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  681.055079] rtw_8822bu 2-1.1:1.2: error beacon valid
[  681.060179] rtw_8822bu 2-1.1:1.2: failed to download drv rsvd page
[  5]  44.00-45.00  sec  4.17 MBytes  34.9 Mbits/sec    0    254 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-45.00  sec   152 MBytes  28.4 Mbits/sec   30             sender
[  5]   0.00-45.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
