# RTL8812BU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="../images/8812bu/rtl8812bu_arm_a53.JPG" height="400"/>|<img src="../images/8812bu/rtl8812bu_pcba.png" height="400"/>|

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
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 4: Dev 3, If 0, Class=Vendor Specific Class, Driver=rtw_8822bu, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 003: ID 0bda:b812 Realtek Semiconductor Corp.
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
  idProduct          0xb812
  bcdDevice            2.10
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
    bmAttributes         0x80
      (Bus Powered)
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

```
[  482.636575] rtw_core: loading out-of-tree module taints kernel.
[  496.857299] rtw_8822bu 1-1.4:1.0: Firmware version 30.20.0, H2C version 14
[  497.067965] usbcore: registered new interface driver rtw_8822bu

Module                  Size  Used by
rtw_8822bu             16384  0
rtw_8822b             221184  1 rtw_8822bu
rtw_usb                24576  1 rtw_8822bu
rtw_core              208896  2 rtw_usb,rtw_8822b
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.8  netmask 255.255.252.0  broadcast 192.168.3.255
        inet6 xxxx::xxxx:xxxx:xxxx:xxxx  prefixlen 64  scopeid 0x20<link>
        ether xx:xx:xx:xx:xx:xx  txqueuelen 1000  (Ethernet)
        RX packets 20  bytes 2781 (2.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 43  bytes 6151 (6.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     3.32 ms   (jitter: 103.24ms, low: 3.09ms, high: 209.72ms)
    Download:   184.09 Mbps (data used: 277.4 MB)
                 13.07 ms   (jitter: 17.44ms, low: 3.35ms, high: 312.91ms)
      Upload:   127.82 Mbps (data used: 206.6 MB)
                 11.03 ms   (jitter: 11.49ms, low: 2.88ms, high: 431.51ms)
```

### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=4.20 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=3.63 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=7.30 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=4.06 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=4.79 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=9.68 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=6.31 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=4.05 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=6.01 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=4.11 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=3.84 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=3.85 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=3.74 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=4.61 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=5.24 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=19.9 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=6.60 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=4.12 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=4.62 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=13.7 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19028ms
rtt min/avg/max/mdev = 3.633/6.229/19.997/3.964 ms
```

#### Self-Ping 

```
PING 192.168.1.8 (192.168.1.8) 10000(10028) bytes of data.
10008 bytes from 192.168.1.8: icmp_seq=1 ttl=64 time=0.107 ms
10008 bytes from 192.168.1.8: icmp_seq=2 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.8: icmp_seq=3 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.8: icmp_seq=4 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.8: icmp_seq=5 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.8: icmp_seq=6 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.8: icmp_seq=7 ttl=64 time=0.097 ms
10008 bytes from 192.168.1.8: icmp_seq=8 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.8: icmp_seq=9 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.8: icmp_seq=10 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.8: icmp_seq=11 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.8: icmp_seq=12 ttl=64 time=0.080 ms
10008 bytes from 192.168.1.8: icmp_seq=13 ttl=64 time=0.068 ms
10008 bytes from 192.168.1.8: icmp_seq=14 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.8: icmp_seq=15 ttl=64 time=0.067 ms
10008 bytes from 192.168.1.8: icmp_seq=16 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.8: icmp_seq=17 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.8: icmp_seq=18 ttl=64 time=0.075 ms
10008 bytes from 192.168.1.8: icmp_seq=19 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.8: icmp_seq=20 ttl=64 time=0.059 ms

--- 192.168.1.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19436ms
rtt min/avg/max/mdev = 0.059/0.067/0.107/0.013 ms
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
          Mode:Managed  Frequency:5.805 GHz  Access Point: xx:xx:xx:xx:xx:xx
          Bit Rate=390 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=43/70  Signal level=-67 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:10   Missed beacon:0
```

### Server & Client Test via iperf3 (PC-Router-DUT)

BT or 2.4G-based devices are not showing any degradation on the TRX performance.

RTW88 supported devices are most likey suffering 2.4G issues.

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.4, port 53790
[  5] local 192.168.1.8 port 5201 connected to 192.168.1.4 port 53793
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  4.98 MBytes  41.7 Mbits/sec    0    154 KBytes
[  5]   1.00-2.00   sec  7.60 MBytes  63.7 Mbits/sec   54    211 KBytes
[  5]   2.00-3.00   sec  6.92 MBytes  58.1 Mbits/sec    0    241 KBytes
[  5]   3.00-4.00   sec  5.82 MBytes  48.8 Mbits/sec    0    258 KBytes
[  5]   4.00-5.00   sec  7.29 MBytes  61.2 Mbits/sec    0    267 KBytes
[  5]   5.00-6.00   sec  8.33 MBytes  69.9 Mbits/sec    0    284 KBytes
[  5]   6.00-7.00   sec  8.09 MBytes  67.8 Mbits/sec    0    305 KBytes
[  5]   7.00-8.00   sec  9.62 MBytes  80.7 Mbits/sec    0    327 KBytes
[  5]   8.00-9.00   sec  9.92 MBytes  83.3 Mbits/sec    0    349 KBytes
[  5]   9.00-10.00  sec  10.1 MBytes  84.8 Mbits/sec    0    369 KBytes
[  5]  10.00-11.00  sec  9.01 MBytes  75.5 Mbits/sec    0    388 KBytes
[  5]  11.00-12.00  sec  9.56 MBytes  80.2 Mbits/sec    0    406 KBytes
[  5]  12.00-13.00  sec  9.92 MBytes  83.3 Mbits/sec    0    423 KBytes
[  5]  13.00-14.00  sec  9.56 MBytes  80.2 Mbits/sec    0    490 KBytes
[  5]  14.00-15.00  sec  8.45 MBytes  70.9 Mbits/sec    0    513 KBytes
[  5]  15.00-16.00  sec  9.50 MBytes  79.7 Mbits/sec    0    513 KBytes
[  5]  16.00-17.00  sec  7.35 MBytes  61.7 Mbits/sec    0    513 KBytes
[  5]  17.00-18.00  sec  6.31 MBytes  52.9 Mbits/sec    0    513 KBytes
[  5]  18.00-19.00  sec  7.35 MBytes  61.7 Mbits/sec    0    513 KBytes
[  5]  19.00-20.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  20.00-21.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  21.00-22.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  22.00-23.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  23.00-24.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  24.00-25.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  25.00-26.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  26.00-27.00  sec  8.75 MBytes  73.4 Mbits/sec    0    771 KBytes
[  5]  27.00-28.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  28.00-29.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  29.00-30.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  30.00-31.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  31.00-32.00  sec  8.75 MBytes  73.4 Mbits/sec    0    771 KBytes
[  5]  32.00-33.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  33.00-34.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  34.00-35.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  35.00-36.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  36.00-37.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  37.00-38.00  sec  13.8 MBytes   115 Mbits/sec    0    771 KBytes
[  5]  38.00-39.00  sec  16.2 MBytes   136 Mbits/sec    0    771 KBytes
[  5]  39.00-40.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  40.00-41.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  41.00-42.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  42.00-43.00  sec  13.8 MBytes   115 Mbits/sec    0    771 KBytes
[  5]  43.00-44.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  44.00-45.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  45.00-46.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  46.00-47.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  47.00-48.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  48.00-49.00  sec  13.8 MBytes   115 Mbits/sec    0    771 KBytes
[  5]  49.00-50.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  50.00-51.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  51.00-52.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  52.00-53.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  53.00-54.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  54.00-55.00  sec  10.0 MBytes  83.8 Mbits/sec    0    771 KBytes
[  5]  55.00-56.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  56.00-57.00  sec  10.0 MBytes  83.9 Mbits/sec    0    771 KBytes
[  5]  57.00-58.00  sec  12.5 MBytes   105 Mbits/sec    0    771 KBytes
[  5]  58.00-59.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  59.00-60.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  60.00-61.00  sec  8.75 MBytes  73.4 Mbits/sec    0    771 KBytes
[  5]  61.00-62.00  sec  11.2 MBytes  94.4 Mbits/sec    0    771 KBytes
[  5]  62.00-63.00  sec  10.0 MBytes  83.9 Mbits/sec   81    539 KBytes
[  5]  63.00-64.00  sec  7.50 MBytes  62.9 Mbits/sec    0    539 KBytes
[  5]  64.00-65.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  65.00-66.00  sec  5.00 MBytes  41.9 Mbits/sec    0    539 KBytes
[  5]  66.00-67.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  67.00-68.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  68.00-69.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  69.00-70.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  70.00-71.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  71.00-72.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  72.00-73.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  73.00-74.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  74.00-75.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  75.00-76.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  76.00-77.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  77.00-78.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  78.00-79.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  79.00-80.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  80.00-81.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  81.00-82.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  82.00-83.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  83.00-84.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  84.00-85.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  85.00-86.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  86.00-87.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  87.00-88.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  88.00-89.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  89.00-90.00  sec  8.75 MBytes  73.4 Mbits/sec    0    539 KBytes
[  5]  90.00-91.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  91.00-92.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  92.00-93.00  sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5]  93.00-94.00  sec  12.5 MBytes   105 Mbits/sec    0    539 KBytes
[  5]  94.00-95.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  95.00-96.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  96.00-97.00  sec  12.5 MBytes   105 Mbits/sec    0    539 KBytes
[  5]  97.00-98.00  sec  11.2 MBytes  94.4 Mbits/sec    0    539 KBytes
[  5]  98.00-99.00  sec  12.5 MBytes   105 Mbits/sec    0    539 KBytes
[  5]  99.00-100.00 sec  10.0 MBytes  83.9 Mbits/sec    0    539 KBytes
[  5] 100.00-100.04 sec  0.00 Bytes  0.00 bits/sec    0    539 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-100.04 sec  1.03 GBytes  88.2 Mbits/sec  135             sender
[  5]   0.00-100.04 sec  0.00 Bytes  0.00 bits/sec                  receiver
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
Using interface wlan0 with hwaddr xx:xx:xx:xx:xx:xx and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

Any BT or 2.4G-based devices are degrading the TRX performance.

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 54884
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 54885
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  1.55 MBytes  13.0 Mbits/sec    0    128 KBytes
[  5]   1.00-2.00   sec  2.27 MBytes  19.0 Mbits/sec    1    128 KBytes
[  5]   2.00-3.00   sec  1.68 MBytes  14.1 Mbits/sec    2    128 KBytes
[  5]   3.00-4.00   sec  2.17 MBytes  18.2 Mbits/sec    0    128 KBytes
[  5]   4.00-5.00   sec  2.02 MBytes  17.0 Mbits/sec    0    128 KBytes
[  5]   5.00-6.00   sec  1.96 MBytes  16.4 Mbits/sec    0    128 KBytes
[  5]   6.00-7.00   sec  2.02 MBytes  17.0 Mbits/sec    0    128 KBytes
[  5]   7.00-8.00   sec  1.10 MBytes  9.25 Mbits/sec    2    128 KBytes
[  5]   8.00-9.00   sec  1.93 MBytes  16.2 Mbits/sec    1    128 KBytes
[  5]   9.00-10.00  sec  2.05 MBytes  17.2 Mbits/sec    1    128 KBytes
[  5]  10.00-11.00  sec  1.96 MBytes  16.4 Mbits/sec    0    128 KBytes
[  5]  11.00-12.00  sec  2.17 MBytes  18.2 Mbits/sec    1    128 KBytes
[  5]  12.00-13.00  sec  1.10 MBytes  9.25 Mbits/sec    1    128 KBytes
[  5]  13.00-14.00  sec   282 KBytes  2.31 Mbits/sec    1    128 KBytes
[  5]  14.00-15.00  sec  1.44 MBytes  12.1 Mbits/sec    2    128 KBytes
[  5]  15.00-16.00  sec  1.87 MBytes  15.7 Mbits/sec    0    128 KBytes
[  5]  16.00-17.00  sec   847 KBytes  6.94 Mbits/sec    1    128 KBytes
[  5]  17.00-18.00  sec   282 KBytes  2.31 Mbits/sec    2    128 KBytes
[  5]  18.00-19.00  sec  1.07 MBytes  8.99 Mbits/sec    1    128 KBytes
[  5]  19.00-20.00  sec   627 KBytes  5.14 Mbits/sec    1    128 KBytes
[  5]  20.00-21.00  sec  1.16 MBytes  9.77 Mbits/sec    0    128 KBytes
[  5]  21.00-22.00  sec  1.96 MBytes  16.4 Mbits/sec    1   89.8 KBytes
[  5]  22.00-23.00  sec  1.62 MBytes  13.6 Mbits/sec    1   67.0 KBytes
[  5]  23.00-24.00  sec  1.72 MBytes  14.4 Mbits/sec    1   67.0 KBytes
[  5]  24.00-25.00  sec  1.93 MBytes  16.2 Mbits/sec    0   67.0 KBytes
[  5]  25.00-26.00  sec  3.31 MBytes  27.8 Mbits/sec    0   67.0 KBytes
[  5]  26.00-27.00  sec  3.83 MBytes  32.1 Mbits/sec    2   67.0 KBytes
[  5]  27.00-28.00  sec  3.61 MBytes  30.3 Mbits/sec    0   92.7 KBytes
[  5]  28.00-29.00  sec  4.35 MBytes  36.5 Mbits/sec    0    123 KBytes
[  5]  29.00-30.00  sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]  30.00-31.00  sec  4.35 MBytes  36.5 Mbits/sec    0    130 KBytes
[  5]  31.00-32.00  sec  4.17 MBytes  34.9 Mbits/sec    0    130 KBytes
[  5]  32.00-33.00  sec  5.21 MBytes  43.7 Mbits/sec    1    130 KBytes
[  5]  33.00-34.00  sec  5.94 MBytes  49.9 Mbits/sec    0    130 KBytes
[  5]  34.00-35.00  sec  5.02 MBytes  42.1 Mbits/sec    0    130 KBytes
[  5]  35.00-36.00  sec  4.84 MBytes  40.6 Mbits/sec    0    130 KBytes
[  5]  36.00-37.00  sec  4.72 MBytes  39.6 Mbits/sec    0    130 KBytes
[  5]  37.00-38.00  sec  3.43 MBytes  28.8 Mbits/sec    0    195 KBytes
[  5]  38.00-39.00  sec  1.84 MBytes  15.4 Mbits/sec    0    195 KBytes
[  5]  39.00-40.00  sec  2.27 MBytes  19.0 Mbits/sec    0    195 KBytes
[  5]  40.00-41.00  sec  3.06 MBytes  25.7 Mbits/sec    0    195 KBytes
[  5]  41.00-42.00  sec  3.00 MBytes  25.2 Mbits/sec    0    195 KBytes
[  5]  42.00-43.00  sec  2.63 MBytes  22.1 Mbits/sec    0    195 KBytes
[  5]  43.00-44.00  sec  3.43 MBytes  28.8 Mbits/sec    0    195 KBytes
[  5]  44.00-45.00  sec  3.92 MBytes  32.9 Mbits/sec    0    195 KBytes
[  5]  45.00-46.00  sec  3.86 MBytes  32.4 Mbits/sec    0    195 KBytes
[  5]  46.00-47.00  sec  2.14 MBytes  18.0 Mbits/sec    1    195 KBytes
[  5]  47.00-48.00  sec  3.49 MBytes  29.3 Mbits/sec    0    195 KBytes
[  5]  48.00-49.00  sec  2.63 MBytes  22.1 Mbits/sec    0    195 KBytes
[  5]  49.00-50.00  sec  3.12 MBytes  26.2 Mbits/sec    0    195 KBytes
[  5]  50.00-51.00  sec  2.70 MBytes  22.6 Mbits/sec    0    195 KBytes
[  5]  51.00-52.00  sec  2.63 MBytes  22.1 Mbits/sec    0    195 KBytes
[  5]  52.00-53.00  sec  2.70 MBytes  22.6 Mbits/sec    0    195 KBytes
[  5]  53.00-54.00  sec  3.49 MBytes  29.3 Mbits/sec    0    195 KBytes
[  5]  54.00-55.00  sec  3.12 MBytes  26.2 Mbits/sec    0    195 KBytes
[  5]  55.00-56.00  sec  3.98 MBytes  33.4 Mbits/sec    0    195 KBytes
[  5]  56.00-57.00  sec  3.86 MBytes  32.4 Mbits/sec    0    195 KBytes
[  5]  57.00-58.00  sec  3.00 MBytes  25.2 Mbits/sec    1    195 KBytes
[  5]  58.00-59.00  sec  2.27 MBytes  19.0 Mbits/sec    0    195 KBytes
[  5]  59.00-60.00  sec  4.41 MBytes  37.0 Mbits/sec    0    195 KBytes
[  5]  60.00-61.00  sec  5.15 MBytes  43.2 Mbits/sec    0    195 KBytes
[  5]  61.00-62.00  sec  6.19 MBytes  51.9 Mbits/sec    0    195 KBytes
[  5]  62.00-63.00  sec  5.76 MBytes  48.3 Mbits/sec    0    195 KBytes
[  5]  63.00-64.00  sec  6.07 MBytes  50.9 Mbits/sec    0    195 KBytes
[  5]  64.00-65.00  sec  4.90 MBytes  41.1 Mbits/sec    0    195 KBytes
[  5]  65.00-66.00  sec  4.78 MBytes  40.1 Mbits/sec    0    195 KBytes
[  5]  66.00-67.00  sec  3.61 MBytes  30.3 Mbits/sec    1    195 KBytes
[  5]  67.00-68.00  sec  3.92 MBytes  32.9 Mbits/sec    1    195 KBytes
[  5]  68.00-69.00  sec  4.41 MBytes  37.0 Mbits/sec    0    195 KBytes
[  5]  69.00-70.00  sec  3.98 MBytes  33.4 Mbits/sec    0    195 KBytes
[  5]  70.00-71.00  sec  6.86 MBytes  57.6 Mbits/sec    0    298 KBytes
[  5]  71.00-72.00  sec  5.21 MBytes  43.7 Mbits/sec    1    298 KBytes
[  5]  72.00-73.00  sec  6.13 MBytes  51.4 Mbits/sec    0    298 KBytes
[  5]  73.00-74.00  sec  5.15 MBytes  43.2 Mbits/sec    0    298 KBytes
[  5]  74.00-75.00  sec  4.47 MBytes  37.5 Mbits/sec    0    298 KBytes
[  5]  75.00-76.00  sec  2.63 MBytes  22.1 Mbits/sec    0    298 KBytes
[  5]  76.00-77.00  sec  3.31 MBytes  27.7 Mbits/sec    1    298 KBytes
[  5]  77.00-78.00  sec  3.92 MBytes  32.9 Mbits/sec    0    298 KBytes
[  5]  78.00-79.00  sec  4.41 MBytes  37.0 Mbits/sec    0    298 KBytes
[  5]  79.00-80.00  sec  4.04 MBytes  33.9 Mbits/sec    0    298 KBytes
[  5]  80.00-81.00  sec  5.39 MBytes  45.2 Mbits/sec    0    298 KBytes
[  5]  81.00-82.00  sec  5.21 MBytes  43.7 Mbits/sec    0    298 KBytes
[  5]  82.00-83.00  sec  5.70 MBytes  47.8 Mbits/sec    0    298 KBytes
[  5]  83.00-84.00  sec  5.64 MBytes  47.3 Mbits/sec    0    298 KBytes
[  5]  84.00-85.00  sec  4.47 MBytes  37.5 Mbits/sec    0    298 KBytes
[  5]  85.00-86.00  sec  4.59 MBytes  38.5 Mbits/sec    0    298 KBytes
[  5]  86.00-87.00  sec  4.35 MBytes  36.5 Mbits/sec    0    298 KBytes
[  5]  87.00-88.00  sec  3.68 MBytes  30.8 Mbits/sec    0    298 KBytes
[  5]  88.00-89.00  sec  3.98 MBytes  33.4 Mbits/sec    1    298 KBytes
[  5]  89.00-90.00  sec  5.64 MBytes  47.3 Mbits/sec    0    298 KBytes
[  5]  90.00-91.00  sec  7.05 MBytes  59.1 Mbits/sec    0    298 KBytes
[  5]  91.00-92.00  sec  5.58 MBytes  46.8 Mbits/sec    0    298 KBytes
[  5]  92.00-93.00  sec  6.37 MBytes  53.4 Mbits/sec    0    298 KBytes
[  5]  93.00-94.00  sec  4.47 MBytes  37.5 Mbits/sec    0    298 KBytes
[  5]  94.00-95.00  sec  4.29 MBytes  36.0 Mbits/sec    0    298 KBytes
[  5]  95.00-96.00  sec  5.21 MBytes  43.7 Mbits/sec    0    298 KBytes
[  5]  96.00-97.00  sec  4.96 MBytes  41.6 Mbits/sec    0    298 KBytes
[  5]  97.00-98.00  sec  3.74 MBytes  31.3 Mbits/sec    0    298 KBytes
[  5]  98.00-99.00  sec  1.96 MBytes  16.4 Mbits/sec    0    298 KBytes
[  5]  99.00-100.00 sec  3.31 MBytes  27.8 Mbits/sec    0    298 KBytes
[  5] 100.00-100.18 sec   878 KBytes  40.9 Mbits/sec    1    298 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-100.18 sec   354 MBytes  29.6 Mbits/sec   31             sender
[  5]   0.00-100.18 sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
