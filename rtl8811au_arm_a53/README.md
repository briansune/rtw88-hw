# RTL8811AU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/78dff286-a0cd-4dcb-8d18-ff5c59ae64e0" height="400"/>|<img src="https://github.com/user-attachments/assets/e33d820c-4b2a-42e0-8a23-474676784b78" height="400"/>|

```
uname -r
5.4.0

cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.5 LTS"

lscpu
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
Before driver loaded
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=, 480M

After driver loaded
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=rtw_8821au, 480M
```

<details>

<summary>USB Details</summary>



```
lsusb -v -s 001:003

Bus 001 Device 003: ID 0bda:0811 Realtek Semiconductor Corp.
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0 (Defined at Interface level)
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0x0811
  bcdDevice            2.00
  iManufacturer           1 Realtek
  iProduct                2 802.11n WLAN Adapter
  iSerial                 3 00E04C000001
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength           60
    bNumInterfaces          1
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0x80
      (Bus Powered)
    MaxPower              500mA
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           6
      bInterfaceClass       255 Vendor Specific Class
      bInterfaceSubClass    255 Vendor Specific Subclass
      bInterfaceProtocol    255 Vendor Specific Protocol
      iInterface              2 802.11n WLAN Adapter
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
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x09  EP 9 OUT
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
  bDeviceClass            0 (Defined at Interface level)
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  bNumConfigurations      1
Device Status:     0x0000
  (Bus Powered)
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[  325.117372] rtw_core: loading out-of-tree module taints kernel.
[  347.038122] rtw_8821au 1-1.1:1.0: Firmware version 42.4.0, H2C version 0
[  347.473538] rtw_8821au 1-1.1:1.0: efuse MAC invalid, using random
[  347.477075] usbcore: registered new interface driver rtw_8821au

Module                  Size  Used by
rtw_8821au             16384  0
rtw_8821a              36864  1 rtw_8821au
rtw_88xxa              32768  1 rtw_8821a
rtw_usb                24576  1 rtw_8821au
rtw_core              208896  3 rtw_88xxa,rtw_usb,rtw_8821a
```

### Network Manager

When connecting to the router (STA), nmtui will stuck and need to remove and reconnect to achieve connection.

```
[  519.898379] efuse thermal meter is 0xff

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.17  netmask 255.255.252.0  broadcast 192.168.3.255
        inet6   prefixlen 64  scopeid 0x20<link>
        ether   txqueuelen 1000  (Ethernet)
        RX packets 25  bytes 3213 (3.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 35  bytes 4870 (4.8 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

speedtest ookla is completely dead and cannot complete.

speedtest-cli is used instead, with a very bad Mbps.

2G and 5G WIFI band is used to test RTW88, and 2G TRX is problematic.

```
speedtest-cli --secure

# On 2.4G Band
Testing download speed................................................................................
Download: 0.81 Mbit/s
Testing upload speed......................................................................................................
Upload: 1.82 Mbit/s

# On 5G Band
Testing download speed................................................................................
Download: 19.82 Mbit/s
Testing upload speed......................................................................................................
Upload: 3.97 Mbit/s
```

### Network Ping Tests

#### DNS-Ping

Using 2.4G Band on ping shown a unstable behavior and connection drop!

5G Band no issue found.

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=3.99 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=5.07 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=4.20 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=3.89 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=5.88 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=3.88 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=3.77 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=3.76 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=6.24 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=4.52 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=111 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=3.87 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=3.89 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=7.39 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=4.53 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=4.16 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=8.40 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=4.41 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=4.03 ms
64 bytes from 8.8.8.8: icmp_seq=21 ttl=59 time=4.02 ms
64 bytes from 8.8.8.8: icmp_seq=22 ttl=59 time=9.28 ms
64 bytes from 8.8.8.8: icmp_seq=23 ttl=59 time=12.8 ms
64 bytes from 8.8.8.8: icmp_seq=24 ttl=59 time=67.0 ms
64 bytes from 8.8.8.8: icmp_seq=25 ttl=59 time=7.55 ms
64 bytes from 8.8.8.8: icmp_seq=26 ttl=59 time=50.1 ms
64 bytes from 8.8.8.8: icmp_seq=27 ttl=59 time=7.72 ms
64 bytes from 8.8.8.8: icmp_seq=28 ttl=59 time=10.6 ms
64 bytes from 8.8.8.8: icmp_seq=29 ttl=59 time=4.31 ms
64 bytes from 8.8.8.8: icmp_seq=30 ttl=59 time=22.4 ms
64 bytes from 8.8.8.8: icmp_seq=31 ttl=59 time=5.44 ms
64 bytes from 8.8.8.8: icmp_seq=32 ttl=59 time=7.25 ms
64 bytes from 8.8.8.8: icmp_seq=37 ttl=59 time=119 ms
64 bytes from 8.8.8.8: icmp_seq=38 ttl=59 time=4.97 ms
64 bytes from 8.8.8.8: icmp_seq=40 ttl=59 time=119 ms
64 bytes from 8.8.8.8: icmp_seq=42 ttl=59 time=111 ms
64 bytes from 8.8.8.8: icmp_seq=43 ttl=59 time=4.40 ms
64 bytes from 8.8.8.8: icmp_seq=44 ttl=59 time=7.17 ms
64 bytes from 8.8.8.8: icmp_seq=45 ttl=59 time=3.93 ms
64 bytes from 8.8.8.8: icmp_seq=46 ttl=59 time=5.06 ms
64 bytes from 8.8.8.8: icmp_seq=47 ttl=59 time=3.82 ms
64 bytes from 8.8.8.8: icmp_seq=49 ttl=59 time=107 ms
64 bytes from 8.8.8.8: icmp_seq=50 ttl=59 time=3.64 ms
64 bytes from 8.8.8.8: icmp_seq=51 ttl=59 time=3.94 ms
64 bytes from 8.8.8.8: icmp_seq=52 ttl=59 time=3.94 ms
64 bytes from 8.8.8.8: icmp_seq=53 ttl=59 time=6.70 ms
64 bytes from 8.8.8.8: icmp_seq=54 ttl=59 time=4.32 ms
64 bytes from 8.8.8.8: icmp_seq=55 ttl=59 time=4.33 ms
64 bytes from 8.8.8.8: icmp_seq=58 ttl=59 time=111 ms
64 bytes from 8.8.8.8: icmp_seq=59 ttl=59 time=4.25 ms
64 bytes from 8.8.8.8: icmp_seq=60 ttl=59 time=68.0 ms
64 bytes from 8.8.8.8: icmp_seq=61 ttl=59 time=7.61 ms
64 bytes from 8.8.8.8: icmp_seq=62 ttl=59 time=63.5 ms
64 bytes from 8.8.8.8: icmp_seq=63 ttl=59 time=3.89 ms
64 bytes from 8.8.8.8: icmp_seq=64 ttl=59 time=10.2 ms
64 bytes from 8.8.8.8: icmp_seq=65 ttl=59 time=107 ms
64 bytes from 8.8.8.8: icmp_seq=66 ttl=59 time=79.1 ms
64 bytes from 8.8.8.8: icmp_seq=67 ttl=59 time=47.9 ms
64 bytes from 8.8.8.8: icmp_seq=68 ttl=59 time=7.40 ms
64 bytes from 8.8.8.8: icmp_seq=69 ttl=59 time=5.68 ms
64 bytes from 8.8.8.8: icmp_seq=70 ttl=59 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=71 ttl=59 time=3.96 ms
64 bytes from 8.8.8.8: icmp_seq=72 ttl=59 time=6.21 ms
64 bytes from 8.8.8.8: icmp_seq=73 ttl=59 time=4.22 ms
64 bytes from 8.8.8.8: icmp_seq=74 ttl=59 time=3.93 ms
64 bytes from 8.8.8.8: icmp_seq=75 ttl=59 time=10.9 ms
64 bytes from 8.8.8.8: icmp_seq=76 ttl=59 time=3.72 ms
64 bytes from 8.8.8.8: icmp_seq=77 ttl=59 time=3.71 ms
64 bytes from 8.8.8.8: icmp_seq=78 ttl=59 time=3.72 ms
64 bytes from 8.8.8.8: icmp_seq=79 ttl=59 time=4.97 ms
64 bytes from 8.8.8.8: icmp_seq=80 ttl=59 time=3.71 ms
64 bytes from 8.8.8.8: icmp_seq=81 ttl=59 time=3.72 ms
64 bytes from 8.8.8.8: icmp_seq=82 ttl=59 time=3.72 ms
64 bytes from 8.8.8.8: icmp_seq=83 ttl=59 time=4.09 ms
64 bytes from 8.8.8.8: icmp_seq=84 ttl=59 time=6.60 ms
64 bytes from 8.8.8.8: icmp_seq=85 ttl=59 time=3.85 ms
64 bytes from 8.8.8.8: icmp_seq=86 ttl=59 time=3.84 ms
64 bytes from 8.8.8.8: icmp_seq=87 ttl=59 time=5.47 ms
64 bytes from 8.8.8.8: icmp_seq=88 ttl=59 time=4.84 ms
64 bytes from 8.8.8.8: icmp_seq=89 ttl=59 time=3.85 ms
64 bytes from 8.8.8.8: icmp_seq=90 ttl=59 time=3.85 ms
64 bytes from 8.8.8.8: icmp_seq=91 ttl=59 time=4.47 ms
64 bytes from 8.8.8.8: icmp_seq=92 ttl=59 time=8.10 ms
64 bytes from 8.8.8.8: icmp_seq=93 ttl=59 time=4.10 ms
64 bytes from 8.8.8.8: icmp_seq=94 ttl=59 time=4.11 ms
64 bytes from 8.8.8.8: icmp_seq=95 ttl=59 time=4.85 ms
64 bytes from 8.8.8.8: icmp_seq=96 ttl=59 time=5.60 ms
64 bytes from 8.8.8.8: icmp_seq=97 ttl=59 time=81.3 ms
64 bytes from 8.8.8.8: icmp_seq=98 ttl=59 time=4.14 ms
64 bytes from 8.8.8.8: icmp_seq=99 ttl=59 time=79.3 ms
64 bytes from 8.8.8.8: icmp_seq=100 ttl=59 time=6.93 ms
64 bytes from 8.8.8.8: icmp_seq=101 ttl=59 time=5.22 ms
64 bytes from 8.8.8.8: icmp_seq=102 ttl=59 time=3.87 ms
64 bytes from 8.8.8.8: icmp_seq=103 ttl=59 time=96.0 ms
64 bytes from 8.8.8.8: icmp_seq=104 ttl=59 time=73.4 ms
64 bytes from 8.8.8.8: icmp_seq=105 ttl=59 time=4.72 ms
64 bytes from 8.8.8.8: icmp_seq=106 ttl=59 time=3.72 ms
64 bytes from 8.8.8.8: icmp_seq=107 ttl=59 time=4.47 ms
64 bytes from 8.8.8.8: icmp_seq=108 ttl=59 time=3.86 ms
64 bytes from 8.8.8.8: icmp_seq=109 ttl=59 time=4.85 ms
64 bytes from 8.8.8.8: icmp_seq=110 ttl=59 time=3.83 ms
64 bytes from 8.8.8.8: icmp_seq=111 ttl=59 time=6.11 ms
64 bytes from 8.8.8.8: icmp_seq=112 ttl=59 time=3.78 ms
64 bytes from 8.8.8.8: icmp_seq=113 ttl=59 time=3.86 ms
64 bytes from 8.8.8.8: icmp_seq=114 ttl=59 time=3.61 ms
64 bytes from 8.8.8.8: icmp_seq=115 ttl=59 time=3.63 ms
64 bytes from 8.8.8.8: icmp_seq=116 ttl=59 time=7.28 ms
64 bytes from 8.8.8.8: icmp_seq=117 ttl=59 time=3.57 ms
64 bytes from 8.8.8.8: icmp_seq=118 ttl=59 time=5.34 ms
64 bytes from 8.8.8.8: icmp_seq=119 ttl=59 time=3.93 ms
64 bytes from 8.8.8.8: icmp_seq=120 ttl=59 time=3.82 ms
64 bytes from 8.8.8.8: icmp_seq=121 ttl=59 time=4.36 ms
64 bytes from 8.8.8.8: icmp_seq=122 ttl=59 time=3.86 ms
64 bytes from 8.8.8.8: icmp_seq=123 ttl=59 time=6.01 ms
--- 8.8.8.8 ping statistics ---
123 packets transmitted, 113 received, 8% packet loss, time 122327ms
rtt min/avg/max/mdev = 3.571/17.727/119.995/31.076 ms
```

#### Self-Ping 

Using 2.4G Band on ping shown a unstable behavior and connection drop!

5G Band no issue found.

```
PING 192.168.1.17 (192.168.1.17) 10000(10028) bytes of data.
10008 bytes from 192.168.1.17: icmp_seq=1 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.17: icmp_seq=2 ttl=64 time=0.066 ms
10008 bytes from 192.168.1.17: icmp_seq=3 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.17: icmp_seq=4 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.17: icmp_seq=5 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.17: icmp_seq=6 ttl=64 time=0.072 ms
10008 bytes from 192.168.1.17: icmp_seq=7 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.17: icmp_seq=8 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.17: icmp_seq=9 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.17: icmp_seq=10 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.17: icmp_seq=11 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.17: icmp_seq=12 ttl=64 time=0.075 ms
10008 bytes from 192.168.1.17: icmp_seq=13 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.17: icmp_seq=14 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.17: icmp_seq=15 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.17: icmp_seq=16 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.17: icmp_seq=17 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.17: icmp_seq=18 ttl=64 time=0.079 ms
10008 bytes from 192.168.1.17: icmp_seq=19 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.17: icmp_seq=20 ttl=64 time=0.059 ms

--- 192.168.1.17 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19433ms
rtt min/avg/max/mdev = 0.059/0.067/0.108/0.016 ms
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy0
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
        Available Antennas: TX 0x1 RX 0x1
        Configured Antennas: TX 0x1 RX 0x1
        Supported interface modes:
                 * IBSS
                 * managed
                 * AP
                 * AP/VLAN
                 * monitor
                 * P2P-client
                 * P2P-GO
        Band 1:
                Capabilities: 0x196e
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        RX STBC 1-stream
                        Max AMSDU length: 7935 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 16 usec (0x07)
                HT Max RX data rate: 150 Mbps
                HT TX/RX MCS rate indexes supported: 0-7, 32
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
                Capabilities: 0x196e
                        HT20/HT40
                        SM Power Save disabled
                        RX HT20 SGI
                        RX HT40 SGI
                        RX STBC 1-stream
                        Max AMSDU length: 7935 bytes
                        DSSS/CCK HT40
                Maximum RX AMPDU length 65535 bytes (exponent: 0x003)
                Minimum RX AMPDU time spacing: 16 usec (0x07)
                HT Max RX data rate: 150 Mbps
                HT TX/RX MCS rate indexes supported: 0-7, 32
                VHT Capabilities (0x03d07122):
                        Max MPDU length: 11454
                        Supported Channel Width: neither 160 nor 80+80
                        short GI (80 MHz)
                        SU Beamformee
                        MU Beamformee
                        +HTC-VHT
                VHT RX MCS set:
                        1 streams: MCS 0-9
                        2 streams: not supported
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT RX highest supported: 390 Mbps
                VHT TX MCS set:
                        1 streams: MCS 0-9
                        2 streams: not supported
                        3 streams: not supported
                        4 streams: not supported
                        5 streams: not supported
                        6 streams: not supported
                        7 streams: not supported
                        8 streams: not supported
                VHT TX highest supported: 390 Mbps
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
          Mode:Managed  Frequency:5.805 GHz  Access Point:
          Bit Rate=433.3 Mb/s   Tx-Power=33 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=28/70  Signal level=-82 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:3   Missed beacon:0
```

### Server & Client Test via iperf3 (PC-Router-DUT)

iperf3 cannot work, dead!

<details>

<summary>iperf3</summary>

```
# 5G Band
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 49449
[  5] local 192.168.1.17 port 5201 connected to 192.168.1.3 port 49450
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  5.43 MBytes  45.5 Mbits/sec    1    131 KBytes
[  5]   1.00-2.00   sec  3.16 MBytes  26.5 Mbits/sec    2    131 KBytes
[  5]   2.00-3.00   sec  3.58 MBytes  30.1 Mbits/sec    1    134 KBytes
[  5]   3.00-4.00   sec  3.68 MBytes  30.8 Mbits/sec    2    134 KBytes
[  5]   4.00-5.00   sec  4.23 MBytes  35.5 Mbits/sec    2    134 KBytes
[  5]   5.00-6.00   sec  3.06 MBytes  25.7 Mbits/sec    2    134 KBytes
[  5]   6.00-7.00   sec  2.08 MBytes  17.5 Mbits/sec    5    134 KBytes
[  5]   7.00-8.00   sec  1.84 MBytes  15.4 Mbits/sec    4    134 KBytes
[  5]   8.00-9.00   sec  1.41 MBytes  11.8 Mbits/sec    4    134 KBytes
[  5]   9.00-10.00  sec  3.98 MBytes  33.4 Mbits/sec    2    134 KBytes
[  5]  10.00-11.00  sec  5.70 MBytes  47.8 Mbits/sec    1    134 KBytes
[  5]  11.00-12.00  sec  4.17 MBytes  34.9 Mbits/sec    3    134 KBytes
[  5]  12.00-13.00  sec  7.11 MBytes  59.6 Mbits/sec    0    134 KBytes
[  5]  13.00-14.00  sec  4.10 MBytes  34.4 Mbits/sec    1    134 KBytes
[  5]  14.00-15.00  sec  6.49 MBytes  54.5 Mbits/sec    0    134 KBytes
[  5]  15.00-16.00  sec  6.31 MBytes  52.9 Mbits/sec    0    134 KBytes
[  5]  16.00-17.00  sec  5.51 MBytes  46.2 Mbits/sec    1    134 KBytes
[  5]  17.00-18.00  sec  4.66 MBytes  39.1 Mbits/sec    2    134 KBytes
[  5]  18.00-19.00  sec  7.60 MBytes  63.7 Mbits/sec    0    134 KBytes
[  5]  19.00-20.00  sec  7.23 MBytes  60.6 Mbits/sec    1    134 KBytes
[  5]  20.00-21.00  sec  7.11 MBytes  59.6 Mbits/sec    1    134 KBytes
[  5]  21.00-22.00  sec  8.39 MBytes  70.4 Mbits/sec    0    258 KBytes
[  5]  22.00-23.00  sec  4.66 MBytes  39.1 Mbits/sec    1    258 KBytes
[  5]  23.00-24.00  sec  7.05 MBytes  59.1 Mbits/sec    1    338 KBytes
[  5]  24.00-25.00  sec  6.37 MBytes  53.4 Mbits/sec    0    495 KBytes
[  5]  25.00-26.00  sec  6.62 MBytes  55.5 Mbits/sec    0    513 KBytes
[  5]  26.00-27.00  sec  6.56 MBytes  55.0 Mbits/sec    0    513 KBytes
[  5]  27.00-28.00  sec  4.41 MBytes  37.0 Mbits/sec    0    539 KBytes
[  5]  27.00-28.00  sec  4.41 MBytes  37.0 Mbits/sec    0    539 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-28.00  sec   148 MBytes  44.4 Mbits/sec   37             sender
[  5]   0.00-28.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
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
sudo hostapd /etc/hostapd/hostapd.conf -B
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr  and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

Both ping and iperf3 cannot work due to NO AP WIFI can be found!

Possible gain settings are wrong or missing.

<details>

<summary>dmesg</summary>

```
```

</details>

<details>

<summary>iperf3</summary>

```
```

</details>
