# RTL8812AU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/65f23a76-3be4-4ce6-b039-b402b552f01e" height="400"/>|<img src="https://github.com/user-attachments/assets/bd7b8813-3b1b-4868-8ca3-ae987c9269e9" height="400"/>|

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
        |__ Port 1: Dev 4, If 0, Class=Vendor Specific Class, Driver=rtw_8812au, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 004: ID 0bda:8812 Realtek Semiconductor Corp. RTL8812AU 802.11a/b/g/n/ac WLAN Adapter
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
  idProduct          0x8812 RTL8812AU 802.11a/b/g/n/ac WLAN Adapter
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
[   60.976458] rtw_core: loading out-of-tree module taints kernel.
[   74.252840] rtw_8812au 1-1.1:1.0: Firmware version 52.14.0, H2C version 0
[   74.524683] random: crng init done
[   74.524690] random: 7 urandom warning(s) missed due to ratelimiting
[   74.649155] usbcore: registered new interface driver rtw_8812au
[   74.681563] usb 1-1.1: USB disconnect, device number 3
[   75.030197] usb 1-1.1: new high-speed USB device number 4 using xhci-hcd
[   75.154562] usb 1-1.1: New USB device found, idVendor=0bda, idProduct=8812, bcdDevice= 0.00
[   75.154569] usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[   75.154573] usb 1-1.1: Product: 802.11n NIC
[   75.154577] usb 1-1.1: Manufacturer: Realtek
[   75.154582] usb 1-1.1: SerialNumber: 123456
[   75.193379] rtw_8812au 1-1.1:1.0: Firmware version 52.14.0, H2C version 0

Module                  Size  Used by
rtw_8812au             16384  0
rtw_8812a              45056  1 rtw_8812au
rtw_88xxa              32768  1 rtw_8812a
rtw_usb                24576  1 rtw_8812au
rtw_core              208896  3 rtw_88xxa,rtw_usb,rtw_8812a
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.25  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 13  bytes 1947 (1.9 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 18  bytes 2563 (2.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:     5.04 ms   (jitter: 0.98ms, low: 4.45ms, high: 5.97ms)
    Download:    47.19 Mbps (data used: 80.5 MB)
                 57.43 ms   (jitter: 20.04ms, low: 4.82ms, high: 324.78ms)
      Upload:    35.49 Mbps (data used: 46.0 MB)
                 85.44 ms   (jitter: 26.25ms, low: 6.57ms, high: 406.87ms)
```
### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=32.0 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=24.5 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=11.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=3.62 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=9.74 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=10.3 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=3.38 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=10.2 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=3.39 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=9.26 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=13.5 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.01 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=3.26 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=7.64 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=6.78 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=10.6 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=3.41 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=9.19 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=5.94 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=4.19 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 3.269/9.327/32.027/7.154 ms
```

#### Self-Ping 

```
PING 192.168.1.25 (192.168.1.25) 10000(10028) bytes of data.
10008 bytes from 192.168.1.25: icmp_seq=1 ttl=64 time=0.110 ms
10008 bytes from 192.168.1.25: icmp_seq=2 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.25: icmp_seq=3 ttl=64 time=0.075 ms
10008 bytes from 192.168.1.25: icmp_seq=4 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=5 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.25: icmp_seq=6 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=7 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=8 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=9 ttl=64 time=0.071 ms
10008 bytes from 192.168.1.25: icmp_seq=10 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.25: icmp_seq=11 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=12 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.25: icmp_seq=13 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=14 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=15 ttl=64 time=0.076 ms
10008 bytes from 192.168.1.25: icmp_seq=16 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.25: icmp_seq=17 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=18 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.25: icmp_seq=19 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=20 ttl=64 time=0.070 ms

--- 192.168.1.25 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19441ms
rtt min/avg/max/mdev = 0.059/0.065/0.110/0.013 ms
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
                HT Max RX data rate: 300 Mbps
                HT TX/RX MCS rate indexes supported: 0-15, 32
                VHT Capabilities (0x03d071a2):
                        Max MPDU length: 11454
                        Supported Channel Width: neither 160 nor 80+80
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
          Mode:Managed  Frequency:2.412 GHz  Access Point: F8:6F:B0:0E:AE:E5
          Bit Rate=40.5 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=48/70  Signal level=-62 dBm
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
Accepted connection from 192.168.1.3, port 58448
[  5] local 192.168.1.25 port 5201 connected to 192.168.1.3 port 58449
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.83 MBytes  23.8 Mbits/sec    0    130 KBytes
[  5]   1.00-2.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   2.00-3.00   sec  3.98 MBytes  33.4 Mbits/sec    0    130 KBytes
[  5]   3.00-4.00   sec  3.68 MBytes  30.8 Mbits/sec    0    130 KBytes
[  5]   4.00-5.00   sec  4.96 MBytes  41.6 Mbits/sec    0    282 KBytes
[  5]   5.00-6.00   sec  4.35 MBytes  36.5 Mbits/sec    0    322 KBytes
[  5]   6.00-7.00   sec  5.27 MBytes  44.2 Mbits/sec    0    378 KBytes
[  5]   7.00-8.00   sec  3.80 MBytes  31.9 Mbits/sec    0    378 KBytes
[  5]   8.00-9.00   sec  4.41 MBytes  37.0 Mbits/sec    0    448 KBytes
[  5]   9.00-10.00  sec  3.61 MBytes  30.3 Mbits/sec    0    448 KBytes
[  5]  10.00-11.00  sec  3.55 MBytes  29.8 Mbits/sec    0    448 KBytes
[  5]  11.00-12.00  sec  4.41 MBytes  37.0 Mbits/sec    0    448 KBytes
[  5]  12.00-13.00  sec  3.68 MBytes  30.8 Mbits/sec    0    448 KBytes
[  5]  13.00-14.00  sec  2.63 MBytes  22.1 Mbits/sec    0    448 KBytes
[  5]  14.00-15.00  sec  2.63 MBytes  22.1 Mbits/sec    0    448 KBytes
[  5]  15.00-16.00  sec  2.70 MBytes  22.6 Mbits/sec    0    448 KBytes
[  5]  16.00-17.00  sec  2.70 MBytes  22.6 Mbits/sec    0    448 KBytes
[  5]  17.00-18.00  sec  2.76 MBytes  23.1 Mbits/sec    0    448 KBytes
[  5]  18.00-19.00  sec  2.63 MBytes  22.1 Mbits/sec    0    448 KBytes
[  5]  19.00-20.00  sec  3.68 MBytes  30.8 Mbits/sec    0    448 KBytes
[  5]  20.00-21.00  sec  3.74 MBytes  31.4 Mbits/sec    0    448 KBytes
[  5]  21.00-22.00  sec  2.63 MBytes  22.1 Mbits/sec    0    448 KBytes
[  5]  22.00-23.00  sec  3.43 MBytes  28.8 Mbits/sec    0    448 KBytes
[  5]  23.00-24.00  sec  2.70 MBytes  22.6 Mbits/sec    0    448 KBytes
[  5]  24.00-25.00  sec  2.76 MBytes  23.1 Mbits/sec    0    448 KBytes
[  5]  25.00-26.00  sec  1.84 MBytes  15.4 Mbits/sec    0    448 KBytes
[  5]  26.00-27.00  sec  2.57 MBytes  21.6 Mbits/sec    0    448 KBytes
[  5]  27.00-28.00  sec  2.70 MBytes  22.6 Mbits/sec    0    448 KBytes
[  5]  28.00-29.00  sec  3.55 MBytes  29.8 Mbits/sec    0    448 KBytes
[  5]  29.00-30.00  sec  3.49 MBytes  29.3 Mbits/sec    0    448 KBytes
[  5]  30.00-31.00  sec  3.68 MBytes  30.8 Mbits/sec    0    448 KBytes
[  5]  31.00-32.00  sec  1.84 MBytes  15.4 Mbits/sec    0    448 KBytes
[  5]  32.00-33.00  sec  2.57 MBytes  21.6 Mbits/sec    0    448 KBytes
[  5]  33.00-34.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  34.00-35.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  35.00-36.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
[  5]  36.00-37.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  37.00-38.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  38.00-39.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  39.00-40.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  40.00-41.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  41.00-42.00  sec  1.84 MBytes  15.4 Mbits/sec    0    448 KBytes
[  5]  42.00-43.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  43.00-44.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
[  5]  44.00-45.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  45.00-46.00  sec  2.63 MBytes  22.1 Mbits/sec    0    448 KBytes
[  5]  46.00-47.00  sec   878 KBytes  7.19 Mbits/sec    0    448 KBytes
[  5]  47.00-48.00  sec  2.70 MBytes  22.6 Mbits/sec    0    448 KBytes
[  5]  48.00-49.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  49.00-50.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
[  5]  50.00-51.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  51.00-52.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
[  5]  52.00-53.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  53.00-54.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  54.00-55.00  sec  1.72 MBytes  14.4 Mbits/sec    0    448 KBytes
[  5]  55.00-56.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
[  5]  56.00-57.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
[  5]  56.00-57.00  sec  1.78 MBytes  14.9 Mbits/sec    0    448 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-57.00  sec   153 MBytes  22.6 Mbits/sec    0             sender
[  5]   0.00-57.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
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
Accepted connection from 192.168.175.86, port 58734
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 58735
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  3.38 MBytes  28.4 Mbits/sec    0    130 KBytes
[  5]   1.00-2.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   2.00-3.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   3.00-4.00   sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]   4.00-5.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   5.00-6.00   sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]   6.00-7.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   7.00-8.00   sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]   8.00-9.00   sec  3.43 MBytes  28.8 Mbits/sec    0    130 KBytes
[  5]   9.00-10.00  sec  2.76 MBytes  23.1 Mbits/sec    0    130 KBytes
[  5]  10.00-11.00  sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]  11.00-12.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  12.00-13.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  13.00-14.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  14.00-15.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  15.00-16.00  sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]  16.00-17.00  sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]  17.00-18.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  18.00-19.00  sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]  19.00-20.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  20.00-21.00  sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]  21.00-22.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  22.00-23.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  23.00-24.00  sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]  24.00-25.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  25.00-26.00  sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]  26.00-27.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  27.00-28.00  sec  2.82 MBytes  23.6 Mbits/sec    0    130 KBytes
[  5]  28.00-29.00  sec  3.12 MBytes  26.2 Mbits/sec    0    130 KBytes
[  5]  29.00-30.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  30.00-31.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  31.00-32.00  sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]  32.00-33.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  33.00-34.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  34.00-35.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  35.00-36.00  sec  3.43 MBytes  28.8 Mbits/sec    0    130 KBytes
[  5]  36.00-37.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  37.00-38.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  38.00-39.00  sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]  39.00-40.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  40.00-41.00  sec  3.37 MBytes  28.3 Mbits/sec    0    130 KBytes
[  5]  41.00-42.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  42.00-43.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  43.00-44.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  44.00-45.00  sec  3.06 MBytes  25.7 Mbits/sec    0    130 KBytes
[  5]  45.00-46.00  sec  2.14 MBytes  18.0 Mbits/sec    0    130 KBytes
[  5]  46.00-47.00  sec  2.45 MBytes  20.6 Mbits/sec    0    130 KBytes
[  5]  47.00-48.00  sec  2.45 MBytes  20.6 Mbits/sec    0    130 KBytes
[  5]  48.00-49.00  sec  2.14 MBytes  18.0 Mbits/sec    0    130 KBytes
[  5]  49.00-50.00  sec  2.14 MBytes  18.0 Mbits/sec    0    130 KBytes
[  5]  50.00-51.00  sec  2.21 MBytes  18.5 Mbits/sec    0    130 KBytes
[  5]  51.00-52.00  sec  2.51 MBytes  21.1 Mbits/sec    0    130 KBytes
[  5]  52.00-53.00  sec  2.14 MBytes  18.0 Mbits/sec    0    130 KBytes
[  5]  52.00-53.00  sec  2.14 MBytes  18.0 Mbits/sec    0    130 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-53.00  sec   160 MBytes  25.4 Mbits/sec    0             sender
[  5]   0.00-53.00  sec  0.00 Bytes  0.00 bits/sec                  receiver
```

</details>
