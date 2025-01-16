# RTL8822CU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/be785ae2-ea1b-43bd-84cd-0b81bae539a8" height="400"/>|<img src="https://github.com/user-attachments/assets/7e8d57a1-f909-450b-bafc-016ef499520b" height="400"/>|

```
uname -r
6.1.111-rt42

cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

lscpu
Architecture:                         aarch64
CPU op-mode(s):                       32-bit, 64-bit
Byte Order:                           Little Endian
CPU(s):                               2
On-line CPU(s) list:                  0,1
Thread(s) per core:                   1
Core(s) per socket:                   2
Socket(s):                            1
Vendor ID:                            ARM
Model:                                0
Model name:                           Cortex-A35
Stepping:                             r1p0
BogoMIPS:                             66.66
Vulnerability Gather data sampling:   Not affected
Vulnerability Itlb multihit:          Not affected
Vulnerability L1tf:                   Not affected
Vulnerability Mds:                    Not affected
Vulnerability Meltdown:               Not affected
Vulnerability Mmio stale data:        Not affected
Vulnerability Reg file data sampling: Not affected
Vulnerability Retbleed:               Not affected
Vulnerability Spec rstack overflow:   Not affected
Vulnerability Spec store bypass:      Not affected
Vulnerability Spectre v1:             Mitigation; __user pointer sanitization
Vulnerability Spectre v2:             Not affected
Vulnerability Srbds:                  Not affected
Vulnerability Tsx async abort:        Not affected
Flags:                                fp asimd evtstrm aes pmull sha1 sha2 crc32
                                       cpuid
```

### USB Tree

```
[  192.697473] rtw_core: loading out-of-tree module taints kernel.
[  193.141310] rtw_8822cu 1-1:1.2: Firmware version 9.9.15, H2C version 15
[  193.148644] rtw_8822cu 1-1:1.2: WOW Firmware version 9.9.4, H2C version 15
[  193.545849] usbcore: registered new interface driver rtw_8822cu

# Before driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 1, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 2, Class=Vendor Specific Class, Driver=, 480M

# After driver is inserted.

/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 1, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 2, Class=Vendor Specific Class, Driver=rtw_8822cu, 480M
```

<details>

<summary>USB Details</summary>

```
lsusb -v -s 001:002

Bus 001 Device 002: ID 0bda:c82c Realtek Semiconductor Corp. 802.11ac NIC
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xc82c
  bcdDevice            0.00
  iManufacturer           1 Realtek
  iProduct                2 802.11ac NIC
  iSerial                 3 123456
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength       0x00e5
    bNumInterfaces          3
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0xa0
      (Bus Powered)
      Remote Wakeup
    MaxPower              500mA
    Interface Association:
      bLength                 8
      bDescriptorType        11
      bFirstInterface         0
      bInterfaceCount         2
      bFunctionClass        224 Wireless
      bFunctionSubClass       1 Radio Frequency
      bFunctionProtocol       1 Bluetooth
      iFunction               4 Bluetooth Radio
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           3
      bInterfaceClass       224 Wireless
      bInterfaceSubClass      1 Radio Frequency
      bInterfaceProtocol      1 Bluetooth
      iInterface              4 Bluetooth Radio
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
      iInterface              4 Bluetooth Radio
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
      iInterface              4 Bluetooth Radio
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
      iInterface              4 Bluetooth Radio
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
      iInterface              4 Bluetooth Radio
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
      iInterface              4 Bluetooth Radio
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
      iInterface              4 Bluetooth Radio
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
      iInterface              2 802.11ac NIC
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
Device Qualifier (for other device speed):
  bLength                10
  bDescriptorType         6
  bcdUSB               2.00
  bDeviceClass            0
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  bNumConfigurations      1
can't get debug descriptor: Resource temporarily unavailable
Device Status:     0x0000
  (Bus Powered)
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
lsmod
Module                  Size  Used by
rtw_8822cu             16384  0
rtw_8822c             471040  1 rtw_8822cu
rtw_usb                24576  1 rtw_8822cu
rtw_core              217088  2 rtw_usb,rtw_8822c
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.20  netmask 255.255.252.0  broadcast 192.168.3.255
        inet6   prefixlen 64  scopeid 0x20<link>
        ether   txqueuelen 1000  (Ethernet)
        RX packets 41  bytes 6712 (6.7 KB)
        RX errors 0  dropped 7  overruns 0  frame 0
        TX packets 56  bytes 9977 (9.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
# 2G Band
   Speedtest by Ookla

Idle Latency:     6.66 ms   (jitter: 8.24ms, low: 3.55ms, high: 17.51ms)
    Download:    36.33 Mbps (data used: 56.4 MB)
                112.97 ms   (jitter: 45.35ms, low: 3.31ms, high: 1083.62ms)
      Upload:    22.26 Mbps (data used: 36.9 MB)
                196.22 ms   (jitter: 60.67ms, low: 14.56ms, high: 1083.89ms)

$ 5G Band
   Speedtest by Ookla

Idle Latency:     3.29 ms   (jitter: 0.06ms, low: 3.22ms, high: 3.36ms)
    Download:   183.65 Mbps (data used: 278.1 MB)
                 17.84 ms   (jitter: 18.10ms, low: 7.05ms, high: 325.95ms)
      Upload:    44.98 Mbps (data used: 39.1 MB)
                125.58 ms   (jitter: 48.65ms, low: 10.67ms, high: 347.23ms)
```

### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=18.2 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=4.24 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=18.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=7.57 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=14.3 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=4.29 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=6.34 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=15.8 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=4.53 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=6.49 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=4.12 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=9.47 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=10.5 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=8.09 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=7.04 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=4.90 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=4.24 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=295 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=15.5 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=4.25 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 4.117/23.152/294.895/62.526 ms
```

#### Self-Ping 

```
PING 192.168.1.20 (192.168.1.20) 10000(10028) bytes of data.
10008 bytes from 192.168.1.20: icmp_seq=1 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.20: icmp_seq=2 ttl=64 time=0.094 ms
10008 bytes from 192.168.1.20: icmp_seq=3 ttl=64 time=0.085 ms
10008 bytes from 192.168.1.20: icmp_seq=4 ttl=64 time=0.087 ms
10008 bytes from 192.168.1.20: icmp_seq=5 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.20: icmp_seq=6 ttl=64 time=0.141 ms
10008 bytes from 192.168.1.20: icmp_seq=7 ttl=64 time=0.147 ms
10008 bytes from 192.168.1.20: icmp_seq=8 ttl=64 time=0.144 ms
10008 bytes from 192.168.1.20: icmp_seq=9 ttl=64 time=0.113 ms
10008 bytes from 192.168.1.20: icmp_seq=10 ttl=64 time=0.151 ms
10008 bytes from 192.168.1.20: icmp_seq=11 ttl=64 time=0.081 ms
10008 bytes from 192.168.1.20: icmp_seq=12 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.20: icmp_seq=13 ttl=64 time=0.147 ms
10008 bytes from 192.168.1.20: icmp_seq=14 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.20: icmp_seq=15 ttl=64 time=0.090 ms
10008 bytes from 192.168.1.20: icmp_seq=16 ttl=64 time=0.078 ms
10008 bytes from 192.168.1.20: icmp_seq=17 ttl=64 time=0.099 ms
10008 bytes from 192.168.1.20: icmp_seq=18 ttl=64 time=0.144 ms
10008 bytes from 192.168.1.20: icmp_seq=19 ttl=64 time=0.148 ms
10008 bytes from 192.168.1.20: icmp_seq=20 ttl=64 time=0.147 ms

--- 192.168.1.20 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19438ms
rtt min/avg/max/mdev = 0.078/0.121/0.151/0.026 ms
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy0
        max # scan SSIDs: 4
        max scan IEs length: 323 bytes
        max # sched scan SSIDs: 4
        max # match sets: 0
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
                Capabilities: 0x19ef
                        RX LDPC
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        TX STBC
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
                Capabilities: 0x19ef
                        RX LDPC
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        TX STBC
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
                 * remain_on_channel
                 * set_tx_bitrate_mask
                 * frame
                 * frame_wait_cancel
                 * set_wiphy_netns
                 * set_channel
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
                 * Unknown command (140)
        WoWLAN support:
                 * wake up on disconnect
                 * wake up on magic packet
                 * wake up on pattern match, up to 12 patterns of 1-128 bytes,
                   maximum packet offset 0 bytes
                 * can do GTK rekeying
                 * wake up on GTK rekey failure
                 * wake up on network detection, up to 4 match sets
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
        Device supports randomizing MAC-addr in scans.
        max # scan plans: 1
        max scan plan interval: -1
        max scan plan iterations: 0
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
                 * managed: 0x40 0xb0 0xd0
                 * AP: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * AP/VLAN: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * mesh point: 0xb0 0xc0 0xd0
                 * P2P-client: 0x40 0xd0
                 * P2P-GO: 0x00 0x20 0x40 0xa0 0xb0 0xc0 0xd0
                 * P2P-device: 0x40 0xd0
        Supported extended features:
                * [ RRM ]: RRM
                * [ SET_SCAN_DWELL ]: scan dwell setting
                * [ FILS_STA ]: STA FILS (Fast Initial Link Setup)
                * [ CONTROL_PORT_OVER_NL80211 ]: control port over nl80211
                * [ TXQS ]: FQ-CoDel-enabled intermediate TXQs
```

</details>

### iwconfig

```
wlan0     IEEE 802.11  ESSID:""
          Mode:Managed  Frequency:2.437 GHz  Access Point: 
          Bit Rate=81 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=51/70  Signal level=-59 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:20   Missed beacon:0
```

### Server & Client Test via iperf3 (PC-Router-DUT)

BT or ZigBee devices are introducing degradation to 2.4G Band.

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.18, port 57255
[  5] local 192.168.1.20 port 5201 connected to 192.168.1.18 port 57256
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  2.28 MBytes  19.1 Mbits/sec    5   92.7 KBytes
[  5]   1.00-2.00   sec  4.47 MBytes  37.5 Mbits/sec    0    267 KBytes
[  5]   2.00-3.00   sec  3.00 MBytes  25.2 Mbits/sec    0    267 KBytes
[  5]   3.00-4.00   sec  2.82 MBytes  23.6 Mbits/sec    0    267 KBytes
[  5]   4.00-5.00   sec  2.82 MBytes  23.6 Mbits/sec    0    267 KBytes
[  5]   5.00-6.00   sec  2.94 MBytes  24.7 Mbits/sec    0    267 KBytes
[  5]   6.00-7.00   sec  2.21 MBytes  18.5 Mbits/sec    0    267 KBytes
[  5]   7.00-8.00   sec  3.49 MBytes  29.3 Mbits/sec    0    267 KBytes
[  5]   8.00-9.00   sec  3.55 MBytes  29.8 Mbits/sec    0    267 KBytes
[  5]   9.00-10.00  sec  4.59 MBytes  38.5 Mbits/sec    0    267 KBytes
[  5]  10.00-11.00  sec  4.35 MBytes  36.5 Mbits/sec    0    267 KBytes
[  5]  11.00-12.00  sec  3.61 MBytes  30.3 Mbits/sec    0    267 KBytes
[  5]  12.00-13.00  sec  2.76 MBytes  23.1 Mbits/sec    0    267 KBytes
[  5]  13.00-14.00  sec  3.25 MBytes  27.2 Mbits/sec    0    267 KBytes
[  5]  14.00-15.00  sec  2.94 MBytes  24.7 Mbits/sec    0    267 KBytes
[  5]  15.00-16.00  sec  4.04 MBytes  33.9 Mbits/sec    2    267 KBytes
[  5]  16.00-17.00  sec  2.94 MBytes  24.7 Mbits/sec    0    267 KBytes
[  5]  17.00-18.00  sec  2.94 MBytes  24.7 Mbits/sec    0    267 KBytes
[  5]  18.00-19.00  sec  1.72 MBytes  14.4 Mbits/sec    1   1.43 KBytes
[  5]  19.00-20.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  20.00-21.00  sec  0.00 Bytes  0.00 bits/sec    0   1.43 KBytes
[  5]  21.00-22.00  sec  0.00 Bytes  0.00 bits/sec    0   51.3 KBytes
[  5]  22.00-23.00  sec  0.00 Bytes  0.00 bits/sec    0    115 KBytes
[  5]  23.00-24.00  sec  1.16 MBytes  9.77 Mbits/sec    0    157 KBytes
[  5]  24.00-25.00  sec  2.33 MBytes  19.5 Mbits/sec    0    271 KBytes
[  5]  25.00-26.00  sec  1.29 MBytes  10.8 Mbits/sec    0    271 KBytes
[  5]  26.00-27.00  sec   690 KBytes  5.65 Mbits/sec    1    204 KBytes
[  5]  27.00-28.00  sec  1.78 MBytes  14.9 Mbits/sec    0    245 KBytes
[  5]  28.00-29.00  sec  3.43 MBytes  28.8 Mbits/sec    0    258 KBytes
[  5]  29.00-30.00  sec  2.82 MBytes  23.6 Mbits/sec    0    258 KBytes
[  5]  30.00-30.18  sec   627 KBytes  28.6 Mbits/sec    0    258 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.18  sec  74.8 MBytes  20.8 Mbits/sec    9             sender
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

BT or ZigBee devices are introducing degradation to 2.4G Band.

No error/warning messages are shown during 2.4G band interrupt via BT devices.

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 62251
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 62252
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  5.01 MBytes  42.0 Mbits/sec    0    143 KBytes
[  5]   1.00-2.00   sec  4.53 MBytes  38.0 Mbits/sec    0    143 KBytes
[  5]   2.00-3.00   sec  4.32 MBytes  36.2 Mbits/sec    1    143 KBytes
[  5]   3.00-4.00   sec  4.53 MBytes  38.0 Mbits/sec    0    143 KBytes
[  5]   4.00-5.00   sec  4.59 MBytes  38.5 Mbits/sec    0    143 KBytes
[  5]   5.00-6.00   sec  4.53 MBytes  38.0 Mbits/sec    0    143 KBytes
[  5]   6.00-7.00   sec  4.35 MBytes  36.5 Mbits/sec    0    143 KBytes
[  5]   7.00-8.00   sec  4.29 MBytes  36.0 Mbits/sec    1    143 KBytes
[  5]   8.00-9.00   sec  4.17 MBytes  34.9 Mbits/sec    0    143 KBytes
[  5]   9.00-10.00  sec  4.23 MBytes  35.5 Mbits/sec    0    143 KBytes
[  5]  10.00-11.00  sec  4.56 MBytes  38.3 Mbits/sec    0    143 KBytes
[  5]  11.00-12.00  sec  4.01 MBytes  33.7 Mbits/sec    0    143 KBytes
[  5]  12.00-13.00  sec  3.95 MBytes  33.1 Mbits/sec    1    143 KBytes
[  5]  13.00-14.00  sec  3.16 MBytes  26.5 Mbits/sec   18   69.9 KBytes
[  5]  14.00-15.00  sec  3.03 MBytes  25.4 Mbits/sec   17   52.8 KBytes
[  5]  15.00-16.00  sec  2.76 MBytes  23.1 Mbits/sec   70   52.8 KBytes
[  5]  16.00-17.00  sec  2.85 MBytes  23.9 Mbits/sec   13   58.5 KBytes
[  5]  17.00-18.00  sec  2.82 MBytes  23.6 Mbits/sec    1   68.4 KBytes
[  5]  18.00-19.00  sec  3.77 MBytes  31.6 Mbits/sec    0   68.4 KBytes
[  5]  19.00-20.00  sec  3.49 MBytes  29.3 Mbits/sec    0   68.4 KBytes
[  5]  20.00-21.00  sec  4.96 MBytes  41.6 Mbits/sec    0   98.4 KBytes
[  5]  21.00-22.00  sec  5.21 MBytes  43.7 Mbits/sec    0    130 KBytes
[  5]  22.00-23.00  sec  4.96 MBytes  41.6 Mbits/sec    0    130 KBytes
[  5]  23.00-24.00  sec  5.58 MBytes  46.8 Mbits/sec    0    130 KBytes
[  5]  24.00-25.00  sec  5.39 MBytes  45.2 Mbits/sec    0    130 KBytes
[  5]  25.00-26.00  sec  5.94 MBytes  49.9 Mbits/sec    0    130 KBytes
[  5]  26.00-27.00  sec  5.70 MBytes  47.8 Mbits/sec    0    130 KBytes
[  5]  27.00-28.00  sec  7.05 MBytes  59.1 Mbits/sec    0    202 KBytes
[  5]  28.00-29.00  sec  6.86 MBytes  57.6 Mbits/sec    0    202 KBytes
[  5]  29.00-30.00  sec  6.68 MBytes  56.0 Mbits/sec    0    202 KBytes
[  5]  30.00-30.05  sec   502 KBytes  82.3 Mbits/sec    0    202 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.05  sec   138 MBytes  38.5 Mbits/sec  122             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 62258
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 62259
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  7.86 MBytes  65.9 Mbits/sec    0    148 KBytes
[  5]   1.00-2.00   sec  5.05 MBytes  42.4 Mbits/sec    0    148 KBytes
[  5]   2.00-3.00   sec  5.76 MBytes  48.3 Mbits/sec    1    148 KBytes
[  5]   3.00-4.00   sec  5.82 MBytes  48.8 Mbits/sec    0    148 KBytes
[  5]   4.00-5.00   sec  5.70 MBytes  47.8 Mbits/sec    0    148 KBytes
[  5]   5.00-6.00   sec  5.51 MBytes  46.3 Mbits/sec    0    148 KBytes
[  5]   6.00-7.00   sec  5.08 MBytes  42.6 Mbits/sec    0    148 KBytes
[  5]   7.00-8.00   sec  5.76 MBytes  48.3 Mbits/sec    0    148 KBytes
[  5]   8.00-9.00   sec  5.08 MBytes  42.7 Mbits/sec    0    148 KBytes
[  5]   9.00-10.00  sec  5.82 MBytes  48.8 Mbits/sec    0    148 KBytes
[  5]  10.00-11.00  sec  4.29 MBytes  36.0 Mbits/sec    0    148 KBytes
[  5]  11.00-12.00  sec  1.65 MBytes  13.9 Mbits/sec    1    148 KBytes
[  5]  12.00-13.00  sec   376 KBytes  3.08 Mbits/sec    1    148 KBytes
[  5]  13.00-14.00  sec  0.00 Bytes  0.00 bits/sec    0    148 KBytes
[  5]  14.00-15.00  sec   314 KBytes  2.57 Mbits/sec    0    148 KBytes
[  5]  15.00-16.00  sec  0.00 Bytes  0.00 bits/sec    0    148 KBytes
[  5]  16.00-17.00  sec   376 KBytes  3.08 Mbits/sec    0    148 KBytes
[  5]  17.00-18.00  sec   314 KBytes  2.57 Mbits/sec    0    148 KBytes
[  5]  18.00-19.00  sec   376 KBytes  3.08 Mbits/sec    0    148 KBytes
[  5]  19.00-20.00  sec  0.00 Bytes  0.00 bits/sec    0    148 KBytes
[  5]  20.00-21.00  sec   690 KBytes  5.66 Mbits/sec    0    148 KBytes
[  5]  21.00-22.00  sec  4.78 MBytes  40.1 Mbits/sec    0    148 KBytes
[  5]  22.00-23.00  sec  4.23 MBytes  35.5 Mbits/sec    0    148 KBytes
[  5]  23.00-24.00  sec  4.90 MBytes  41.1 Mbits/sec    0    148 KBytes
[  5]  24.00-25.00  sec  4.29 MBytes  36.0 Mbits/sec    0    148 KBytes
[  5]  25.00-26.00  sec  2.14 MBytes  18.0 Mbits/sec    1    124 KBytes
[  5]  26.00-27.00  sec   816 KBytes  6.68 Mbits/sec    2   89.8 KBytes
[  5]  27.00-28.00  sec  0.00 Bytes  0.00 bits/sec    2   75.6 KBytes
[  5]  28.00-29.00  sec   314 KBytes  2.57 Mbits/sec    0   82.7 KBytes
[  5]  29.00-30.00  sec   376 KBytes  3.08 Mbits/sec    0   85.5 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.10  sec  87.6 MBytes  24.4 Mbits/sec    8             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 62272
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 62273
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   893 KBytes  7.31 Mbits/sec    0   88.4 KBytes
[  5]   1.00-2.00   sec   408 KBytes  3.34 Mbits/sec    0   88.4 KBytes
[  5]   2.00-3.00   sec   596 KBytes  4.88 Mbits/sec    0   88.4 KBytes
[  5]   3.00-4.00   sec   565 KBytes  4.63 Mbits/sec    0   88.4 KBytes
[  5]   4.00-5.00   sec   376 KBytes  3.08 Mbits/sec    0   88.4 KBytes
[  5]   5.00-6.00   sec   565 KBytes  4.63 Mbits/sec    0   88.4 KBytes
[  5]   6.00-7.00   sec   376 KBytes  3.08 Mbits/sec    0   88.4 KBytes
[  5]   7.00-8.00   sec   376 KBytes  3.08 Mbits/sec    0   88.4 KBytes
[  5]   8.00-9.00   sec   565 KBytes  4.63 Mbits/sec    0   88.4 KBytes
[  5]   9.00-10.00  sec   376 KBytes  3.08 Mbits/sec    0   88.4 KBytes
[  5]  10.00-11.00  sec   408 KBytes  3.34 Mbits/sec    0   88.4 KBytes
[  5]  11.00-12.00  sec  2.57 MBytes  21.6 Mbits/sec    0   88.4 KBytes
[  5]  12.00-13.00  sec  5.73 MBytes  48.1 Mbits/sec    0    138 KBytes
[  5]  13.00-14.00  sec  6.49 MBytes  54.5 Mbits/sec    0    138 KBytes
[  5]  14.00-15.00  sec  6.19 MBytes  51.9 Mbits/sec    1    138 KBytes
[  5]  15.00-16.00  sec  5.21 MBytes  43.7 Mbits/sec    0    138 KBytes
[  5]  16.00-17.00  sec  5.64 MBytes  47.3 Mbits/sec    0    138 KBytes
[  5]  17.00-18.00  sec  7.11 MBytes  59.6 Mbits/sec    0    138 KBytes
[  5]  18.00-19.00  sec  6.62 MBytes  55.5 Mbits/sec    0    138 KBytes
[  5]  19.00-20.00  sec  6.25 MBytes  52.4 Mbits/sec    0    138 KBytes
[  5]  20.00-21.00  sec  6.07 MBytes  50.9 Mbits/sec    0    138 KBytes
[  5]  21.00-22.00  sec  3.12 MBytes  26.2 Mbits/sec    1    138 KBytes
[  5]  22.00-23.00  sec   627 KBytes  5.14 Mbits/sec    1    138 KBytes
[  5]  23.00-24.00  sec  0.00 Bytes  0.00 bits/sec    0    138 KBytes
[  5]  24.00-25.00  sec   314 KBytes  2.57 Mbits/sec    0    138 KBytes
[  5]  25.00-26.00  sec  0.00 Bytes  0.00 bits/sec    0    138 KBytes
[  5]  26.00-27.00  sec   376 KBytes  3.09 Mbits/sec    1   95.5 KBytes
[  5]  27.00-28.00  sec  0.00 Bytes  0.00 bits/sec    1   71.3 KBytes
[  5]  28.00-29.00  sec   314 KBytes  2.57 Mbits/sec    0   78.4 KBytes
[  5]  29.00-30.00  sec  0.00 Bytes  0.00 bits/sec    0   81.3 KBytes
[  5]  30.00-31.00  sec   314 KBytes  2.57 Mbits/sec    0   82.7 KBytes
[  5]  31.00-32.00  sec   314 KBytes  2.57 Mbits/sec    0   82.7 KBytes
[  5]  32.00-33.00  sec   314 KBytes  2.57 Mbits/sec    0   87.0 KBytes
[  5]  33.00-34.00  sec   376 KBytes  3.08 Mbits/sec    0   99.8 KBytes
[  5]  34.00-35.00  sec  2.08 MBytes  17.5 Mbits/sec    0    127 KBytes
[  5]  35.00-36.00  sec  2.88 MBytes  24.2 Mbits/sec    1    130 KBytes
[  5]  36.00-37.00  sec  1.53 MBytes  12.8 Mbits/sec    2    130 KBytes
[  5]  37.00-38.00  sec  1.41 MBytes  11.8 Mbits/sec    1    107 KBytes
[  5]  38.00-39.00  sec  1.04 MBytes  8.74 Mbits/sec    0    121 KBytes
[  5]  39.00-40.00  sec   376 KBytes  3.08 Mbits/sec    0   88.4 KBytes
[  5]  40.00-41.00  sec   314 KBytes  2.57 Mbits/sec    0    101 KBytes
[  5]  41.00-42.00  sec   314 KBytes  2.57 Mbits/sec    0    104 KBytes
[  5]  42.00-43.00  sec  0.00 Bytes  0.00 bits/sec    0    106 KBytes
[  5]  43.00-44.00  sec  0.00 Bytes  0.00 bits/sec    0    106 KBytes
[  5]  44.00-45.00  sec   314 KBytes  2.57 Mbits/sec    0    107 KBytes
[  5]  45.00-46.00  sec   314 KBytes  2.57 Mbits/sec    0    114 KBytes
[  5]  46.00-47.00  sec   376 KBytes  3.08 Mbits/sec    0    130 KBytes
[  5]  47.00-48.00  sec  0.00 Bytes  0.00 bits/sec    0    168 KBytes
[  5]  48.00-49.00  sec   439 KBytes  3.60 Mbits/sec    0    168 KBytes
[  5]  49.00-50.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  50.00-51.00  sec   753 KBytes  6.17 Mbits/sec    0    168 KBytes
[  5]  51.00-52.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  52.00-53.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  53.00-54.00  sec   753 KBytes  6.17 Mbits/sec    0    168 KBytes
[  5]  54.00-55.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  55.00-56.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  56.00-57.00  sec   753 KBytes  6.17 Mbits/sec    0    168 KBytes
[  5]  57.00-58.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  58.00-59.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  59.00-60.00  sec   376 KBytes  3.08 Mbits/sec    1    117 KBytes
[  5]  60.00-61.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  61.00-62.00  sec   753 KBytes  6.17 Mbits/sec    0    168 KBytes
[  5]  62.00-63.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  63.00-64.00  sec   376 KBytes  3.08 Mbits/sec    1    115 KBytes
[  5]  64.00-65.00  sec  2.21 MBytes  18.5 Mbits/sec    0    130 KBytes
[  5]  65.00-66.00  sec  3.43 MBytes  28.8 Mbits/sec    0    130 KBytes
[  5]  66.00-67.00  sec  5.33 MBytes  44.7 Mbits/sec    0    130 KBytes
[  5]  67.00-68.00  sec  6.00 MBytes  50.4 Mbits/sec    0    164 KBytes
[  5]  68.00-69.00  sec  5.82 MBytes  48.8 Mbits/sec    0    164 KBytes
[  5]  69.00-70.00  sec  5.51 MBytes  46.3 Mbits/sec    0    164 KBytes
[  5]  70.00-71.00  sec  3.92 MBytes  32.9 Mbits/sec    0    164 KBytes
[  5]  71.00-72.00  sec  4.47 MBytes  37.5 Mbits/sec    0    164 KBytes
[  5]  72.00-73.00  sec  4.53 MBytes  38.0 Mbits/sec    0    164 KBytes
[  5]  73.00-74.00  sec  4.96 MBytes  41.6 Mbits/sec    0    164 KBytes
[  5]  74.00-75.00  sec  4.41 MBytes  37.0 Mbits/sec    0    164 KBytes
[  5]  75.00-76.00  sec  3.43 MBytes  28.8 Mbits/sec    1    168 KBytes
[  5]  76.00-77.00  sec   376 KBytes  3.08 Mbits/sec    1    168 KBytes
[  5]  77.00-78.00  sec  0.00 Bytes  0.00 bits/sec    0    168 KBytes
[  5]  78.00-79.00  sec  0.00 Bytes  0.00 bits/sec    0    168 KBytes
[  5]  79.00-80.00  sec   376 KBytes  3.08 Mbits/sec    0    168 KBytes
[  5]  80.00-81.00  sec  0.00 Bytes  0.00 bits/sec    0    168 KBytes
[  5]  81.00-82.00  sec   376 KBytes  3.09 Mbits/sec    0    168 KBytes
[  5]  82.00-83.00  sec  0.00 Bytes  0.00 bits/sec    0    168 KBytes
[  5]  83.00-84.00  sec  0.00 Bytes  0.00 bits/sec    2    115 KBytes
[  5]  84.00-85.00  sec   439 KBytes  3.60 Mbits/sec    1   91.2 KBytes
[  5]  85.00-86.00  sec  0.00 Bytes  0.00 bits/sec    2   67.0 KBytes
[  5]  86.00-87.00  sec   376 KBytes  3.09 Mbits/sec    1   72.7 KBytes
[  5]  87.00-88.00  sec  0.00 Bytes  0.00 bits/sec    1   51.3 KBytes
[  5]  88.00-89.00  sec  0.00 Bytes  0.00 bits/sec    0   57.0 KBytes
[  5]  89.00-90.00  sec   376 KBytes  3.08 Mbits/sec    0   62.7 KBytes
[  5]  90.00-91.00  sec   376 KBytes  3.08 Mbits/sec    3   51.3 KBytes
[  5]  91.00-92.00  sec   376 KBytes  3.08 Mbits/sec    5   54.2 KBytes
[  5]  91.00-92.00  sec   376 KBytes  3.08 Mbits/sec    5   54.2 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-92.00  sec   145 MBytes  13.2 Mbits/sec   28             sender
iperf3: the client has terminated
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
```

</details>
