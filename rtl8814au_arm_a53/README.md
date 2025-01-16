# RTL8814AU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="./image/8814au/rtl8814au_arm_a53.png" height="400"/>|<img src="./image/8814au/rtl8814au_pcba.png" height="400"/>|

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
Before driver load
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=, 480M

After driver load
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 4, If 0, Class=Vendor Specific Class, Driver=rtw_8814au, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 004: ID 0bda:8813 Realtek Semiconductor Corp.
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.10
  bDeviceClass            0 (Defined at Interface level)
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0x8813
  bcdDevice            0.00
  iManufacturer           1
  iProduct                2
  iSerial                 3
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength           53
    bNumInterfaces          1
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0xa0
      (Bus Powered)
      Remote Wakeup
    MaxPower              500mA
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           5
      bInterfaceClass       255 Vendor Specific Class
      bInterfaceSubClass    255 Vendor Specific Subclass
      bInterfaceProtocol    255 Vendor Specific Protocol
      iInterface              0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x81  EP 1 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
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
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x04  EP 4 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0200  1x 512 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x85  EP 5 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               1
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[  102.983132] rtw_core: loading out-of-tree module taints kernel.
[  121.134787] rtw_8814au 1-1.1:1.0: Firmware version 33.6.0, H2C version 6
[  121.239482] usbcore: registered new interface driver rtw_8814au
[  121.274083] usb 1-1.1: USB disconnect, device number 3
[  121.626242] usb 1-1.1: new high-speed USB device number 4 using xhci-hcd
[  121.750607] usb 1-1.1: New USB device found, idVendor=0bda, idProduct=8813, bcdDevice= 0.00
[  121.750614] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[  121.750618] usb 1-1.1: Product: 802.11ac NIC
[  121.750623] usb 1-1.1: Manufacturer: Realtek
[  121.750627] usb 1-1.1: SerialNumber: 123456
[  121.785997] rtw_8814au 1-1.1:1.0: Firmware version 33.6.0, H2C version 6

Module                  Size  Used by
rtw_8814au             16384  0
rtw_8814a             233472  1 rtw_8814au
rtw_usb                24576  1 rtw_8814au
rtw_core              208896  2 rtw_usb,rtw_8814a
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.31  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 24  bytes 3541 (3.5 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 37  bytes 5583 (5.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     3.41 ms   (jitter: 0.32ms, low: 3.29ms, high: 4.47ms)
    Download:   233.50 Mbps (data used: 411.6 MB)
                 39.83 ms   (jitter: 10.89ms, low: 5.77ms, high: 138.56ms)
      Upload:   157.76 Mbps (data used: 157.9 MB)
                 80.10 ms   (jitter: 35.85ms, low: 7.46ms, high: 530.04ms)
```
### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=3.97 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=6.49 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.79 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=3.62 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=4.63 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=5.02 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=5.12 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=3.48 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=3.61 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=3.96 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=3.69 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=3.67 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=3.80 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=3.80 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=4.03 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=3.77 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=4.01 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=3.75 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=3.75 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=4.88 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19030ms
rtt min/avg/max/mdev = 3.488/4.147/6.496/0.719 ms
```

#### Self-Ping 

```
PING 192.168.1.31 (192.168.1.31) 10000(10028) bytes of data.
10008 bytes from 192.168.1.31: icmp_seq=1 ttl=64 time=0.104 ms
10008 bytes from 192.168.1.31: icmp_seq=2 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.31: icmp_seq=3 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=4 ttl=64 time=0.077 ms
10008 bytes from 192.168.1.31: icmp_seq=5 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.31: icmp_seq=6 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.31: icmp_seq=7 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.31: icmp_seq=8 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=9 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=10 ttl=64 time=0.073 ms
10008 bytes from 192.168.1.31: icmp_seq=11 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.31: icmp_seq=12 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=13 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.31: icmp_seq=14 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=15 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=16 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=17 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.31: icmp_seq=18 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=19 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.31: icmp_seq=20 ttl=64 time=0.059 ms

--- 192.168.1.31 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19437ms
rtt min/avg/max/mdev = 0.059/0.063/0.104/0.013 ms
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
          Mode:Managed  Frequency:5.745 GHz  Access Point: F8:6F:B0:0E:AE:E6
          Bit Rate=263.3 Mb/s   Tx-Power=33 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=32/70  Signal level=-78 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:3   Missed beacon:0
```
### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 55664
[  5] local 192.168.1.31 port 5201 connected to 192.168.1.3 port 55665
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  10.1 MBytes  84.4 Mbits/sec  133    281 KBytes
[  5]   1.00-2.00   sec  9.50 MBytes  79.7 Mbits/sec    0    321 KBytes
[  5]   2.00-3.00   sec  7.66 MBytes  64.2 Mbits/sec    0    345 KBytes
[  5]   3.00-4.00   sec  6.74 MBytes  56.5 Mbits/sec    0    359 KBytes
[  5]   4.00-5.00   sec  7.84 MBytes  65.8 Mbits/sec    0    366 KBytes
[  5]   5.00-6.00   sec  6.13 MBytes  51.4 Mbits/sec    0    366 KBytes
[  5]   6.00-7.00   sec  10.8 MBytes  91.0 Mbits/sec    0    369 KBytes
[  5]   7.00-8.00   sec  9.19 MBytes  77.1 Mbits/sec    0    386 KBytes
[  5]   8.00-9.00   sec  11.6 MBytes  97.1 Mbits/sec    0    409 KBytes
[  5]   9.00-10.00  sec  11.7 MBytes  98.2 Mbits/sec    0    431 KBytes
[  5]  10.00-10.05  sec  0.00 Bytes  0.00 bits/sec    0    431 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-10.05  sec  91.2 MBytes  76.2 Mbits/sec  133             sender
[  5]   0.00-10.05  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 53564
[  5] local 192.168.1.31 port 5201 connected to 192.168.1.3 port 53565
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  10.2 MBytes  85.4 Mbits/sec    0    269 KBytes
[  5]   1.00-2.00   sec  8.33 MBytes  69.9 Mbits/sec    0    308 KBytes
[  5]   2.00-3.00   sec  12.1 MBytes   101 Mbits/sec    0    529 KBytes
[  5]   3.00-4.00   sec  6.56 MBytes  55.0 Mbits/sec    0    529 KBytes
[  5]   4.00-5.00   sec  9.99 MBytes  83.7 Mbits/sec    0    529 KBytes
[  5]   5.00-6.00   sec  7.54 MBytes  63.2 Mbits/sec    0    529 KBytes
[  5]   6.00-7.00   sec  11.4 MBytes  95.6 Mbits/sec    0    529 KBytes
[  5]   7.00-8.00   sec  8.82 MBytes  74.0 Mbits/sec    0    529 KBytes
[  5]   8.00-9.00   sec  5.70 MBytes  47.8 Mbits/sec    0    529 KBytes
[  5]   9.00-10.00  sec  5.76 MBytes  48.3 Mbits/sec    0    529 KBytes
[  5]  10.00-10.07  sec  1.10 MBytes   129 Mbits/sec    0    529 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-10.07  sec  87.4 MBytes  72.8 Mbits/sec    0             sender
[  5]   0.00-10.07  sec  0.00 Bytes  0.00 bits/sec                  receiver
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
Accepted connection from 192.168.175.18, port 53650
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.18 port 53651
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.04 MBytes  17.1 Mbits/sec    0    154 KBytes
[  5]   1.00-2.00   sec  2.94 MBytes  24.7 Mbits/sec    0    154 KBytes
[  5]   2.00-3.00   sec  2.76 MBytes  23.1 Mbits/sec    0    154 KBytes
[  5]   3.00-4.00   sec  3.61 MBytes  30.3 Mbits/sec    0    120 KBytes
[  5]   4.00-5.00   sec  3.55 MBytes  29.8 Mbits/sec    0    130 KBytes
[  5]   5.00-6.00   sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]   6.00-7.00   sec  2.88 MBytes  24.2 Mbits/sec    0    130 KBytes
[  5]   7.00-8.00   sec  3.31 MBytes  27.8 Mbits/sec    0    130 KBytes
[  5]   8.00-9.00   sec  4.23 MBytes  35.5 Mbits/sec    0    130 KBytes
[  5]   9.00-10.00  sec  6.13 MBytes  51.4 Mbits/sec    0    130 KBytes
[  5]  10.00-11.00  sec  7.11 MBytes  59.6 Mbits/sec    0    130 KBytes
[  5]  11.00-12.00  sec  7.60 MBytes  63.7 Mbits/sec    1    130 KBytes
[  5]  12.00-13.00  sec  7.35 MBytes  61.7 Mbits/sec    0    130 KBytes
[  5]  13.00-14.00  sec  6.92 MBytes  58.1 Mbits/sec    0    130 KBytes
[  5]  14.00-15.00  sec  7.05 MBytes  59.1 Mbits/sec    0    130 KBytes
[  5]  15.00-16.00  sec  7.72 MBytes  64.8 Mbits/sec    0    130 KBytes
[  5]  16.00-17.00  sec  7.41 MBytes  62.2 Mbits/sec    0    130 KBytes
[  5]  17.00-18.00  sec  7.47 MBytes  62.7 Mbits/sec    0    130 KBytes
[  5]  18.00-19.00  sec  8.27 MBytes  69.4 Mbits/sec    0    258 KBytes
[  5]  19.00-20.00  sec  9.25 MBytes  77.6 Mbits/sec    0    258 KBytes
[  5]  20.00-21.00  sec  9.50 MBytes  79.7 Mbits/sec    0    258 KBytes
[  5]  21.00-22.00  sec  9.43 MBytes  79.1 Mbits/sec    0    258 KBytes
[  5]  22.00-23.00  sec  9.37 MBytes  78.6 Mbits/sec    0    258 KBytes
[  5]  23.00-24.00  sec  8.82 MBytes  74.0 Mbits/sec    0    258 KBytes
[  5]  24.00-25.00  sec  9.50 MBytes  79.7 Mbits/sec    0    258 KBytes
[  5]  25.00-26.00  sec  9.37 MBytes  78.6 Mbits/sec    0    258 KBytes
[  5]  26.00-27.00  sec  9.37 MBytes  78.6 Mbits/sec    0    258 KBytes
[  5]  27.00-28.00  sec  8.76 MBytes  73.5 Mbits/sec    0    258 KBytes
[  5]  28.00-29.00  sec  9.19 MBytes  77.1 Mbits/sec    0    258 KBytes
[  5]  29.00-30.00  sec  7.84 MBytes  65.8 Mbits/sec    0    258 KBytes
[  5]  30.00-31.00  sec  8.64 MBytes  72.5 Mbits/sec    0    258 KBytes
[  5]  31.00-32.00  sec  9.01 MBytes  75.5 Mbits/sec    0    258 KBytes
[  5]  32.00-33.00  sec  9.86 MBytes  82.7 Mbits/sec    0    258 KBytes
[  5]  33.00-34.00  sec  7.96 MBytes  66.8 Mbits/sec    0    258 KBytes
[  5]  34.00-35.00  sec  8.76 MBytes  73.5 Mbits/sec    0    258 KBytes
[  5]  35.00-36.00  sec  8.45 MBytes  70.9 Mbits/sec    0    258 KBytes
[  5]  36.00-37.00  sec  7.96 MBytes  66.8 Mbits/sec    0    258 KBytes
[  5]  37.00-38.00  sec  8.52 MBytes  71.4 Mbits/sec    0    258 KBytes
[  5]  38.00-39.00  sec  9.25 MBytes  77.6 Mbits/sec    0    258 KBytes
[  5]  39.00-40.00  sec  9.68 MBytes  81.2 Mbits/sec    0    258 KBytes
[  5]  40.00-41.00  sec  8.39 MBytes  70.4 Mbits/sec    0    258 KBytes
[  5]  41.00-42.00  sec  8.58 MBytes  71.9 Mbits/sec    0    258 KBytes
[  5]  42.00-43.00  sec  9.31 MBytes  78.1 Mbits/sec    0    258 KBytes
[  5]  43.00-44.00  sec  8.39 MBytes  70.4 Mbits/sec    0    258 KBytes
[  5]  44.00-45.00  sec  6.25 MBytes  52.4 Mbits/sec    0    258 KBytes
[  5]  45.00-46.00  sec  7.84 MBytes  65.8 Mbits/sec    0    258 KBytes
[  5]  46.00-47.00  sec  6.49 MBytes  54.5 Mbits/sec    0    258 KBytes
[  5]  46.00-47.00  sec  6.49 MBytes  54.5 Mbits/sec    0    258 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-47.00  sec   345 MBytes  61.6 Mbits/sec    1             sender
[  5]   0.00-47.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
