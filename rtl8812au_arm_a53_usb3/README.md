# RTL8812AU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/65f23a76-3be4-4ce6-b039-b402b552f01e" height="400"/>|<img src="https://github.com/user-attachments/assets/1b9c88ce-0f52-404f-971f-ba6be1a0d40c" height="400"/>|

```
uname -r
5.4.0

cat /etc/os-release
NAME="Ubuntu"
VERSION="18.04.5 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.5 LTS"
VERSION_ID="18.04"

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
Before driver is loaded

/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=, 480M

After driver is loaded.
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 5000M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=rtw_8812au, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 002 Device 003: ID 0bda:8812 Realtek Semiconductor Corp. RTL8812AU 802.11a/b/g/n/ac WLAN Adapter
Couldn't open device, some information will be missing
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               3.00
  bDeviceClass            0 (Defined at Interface level)
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0         9
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
    wTotalLength           83
    bNumInterfaces          1
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0x80
      (Bus Powered)
    MaxPower              200mA
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
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               4
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
        bMaxBurst               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x03  EP 3 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x04  EP 4 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0400  1x 1024 bytes
        bInterval               0
        bMaxBurst               4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x85  EP 5 IN
        bmAttributes           19
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Feedback
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               1
        bMaxBurst               0
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
[  127.609093] usbcore: registered new interface driver rtw_8812au
[  127.670036] usb 1-1.1: USB disconnect, device number 3
[  127.878184] usb 2-1.1: new SuperSpeed Gen 1 USB device number 3 using xhci-hcd
[  127.898437] usb 2-1.1: Int endpoint with wBytesPerInterval of 512 in config 1 interface 0 altsetting 0 ep 133: setting to 64
[  127.898602] usb 2-1.1: New USB device found, idVendor=0bda, idProduct=8812, bcdDevice= 0.00
[  127.898607] usb 2-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[  127.898612] usb 2-1.1: Product: 802.11n NIC
[  127.898616] usb 2-1.1: Manufacturer: Realtek
[  127.898620] usb 2-1.1: SerialNumber: 123456
[  127.926197] rtw_8812au 2-1.1:1.0: Firmware version 52.14.0, H2C version 0

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
        RX packets 11  bytes 1705 (1.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 17  bytes 2419 (2.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
   Speedtest by Ookla

Idle Latency:    21.62 ms   (jitter: 39.12ms, low: 5.90ms, high: 51.11ms)
    Download:    34.72 Mbps (data used: 56.0 MB)
                168.88 ms   (jitter: 52.05ms, low: 8.79ms, high: 577.33ms)
      Upload:    34.07 Mbps (data used: 28.2 MB)
                 86.29 ms   (jitter: 17.70ms, low: 5.38ms, high: 182.47ms)
```
### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=6.20 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=12.2 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.77 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=3.73 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=10.3 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=6.64 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=5.55 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=4.07 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=7.85 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=4.46 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=9.51 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=3.62 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=4.12 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=5.53 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=5.93 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=6.45 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=3.87 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=11.0 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=4.26 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 3.620/6.164/12.292/2.622 ms
```

#### Self-Ping 

```
PING 192.168.1.25 (192.168.1.25) 10000(10028) bytes of data.
10008 bytes from 192.168.1.25: icmp_seq=1 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.25: icmp_seq=2 ttl=64 time=0.064 ms
10008 bytes from 192.168.1.25: icmp_seq=3 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=4 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=5 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=6 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=7 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=8 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=9 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=10 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=11 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=12 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.25: icmp_seq=13 ttl=64 time=0.073 ms
10008 bytes from 192.168.1.25: icmp_seq=14 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.25: icmp_seq=15 ttl=64 time=0.063 ms
10008 bytes from 192.168.1.25: icmp_seq=16 ttl=64 time=0.062 ms
10008 bytes from 192.168.1.25: icmp_seq=17 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.25: icmp_seq=18 ttl=64 time=0.058 ms
10008 bytes from 192.168.1.25: icmp_seq=19 ttl=64 time=0.071 ms
10008 bytes from 192.168.1.25: icmp_seq=20 ttl=64 time=0.060 ms

--- 192.168.1.25 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19453ms
rtt min/avg/max/mdev = 0.058/0.063/0.103/0.012 ms
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
          Bit Rate=81 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=54/70  Signal level=-56 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:21   Missed beacon:0
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 63061
[  5] local 192.168.1.25 port 5201 connected to 192.168.1.3 port 63062
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.65 MBytes  22.2 Mbits/sec    0    133 KBytes
[  5]   1.00-2.00   sec  2.76 MBytes  23.1 Mbits/sec    0    133 KBytes
[  5]   2.00-3.00   sec  2.45 MBytes  20.6 Mbits/sec    0    133 KBytes
[  5]   3.00-4.00   sec  3.12 MBytes  26.2 Mbits/sec    0    153 KBytes
[  5]   4.00-5.00   sec  3.61 MBytes  30.3 Mbits/sec    0    257 KBytes
[  5]   5.00-6.00   sec  3.92 MBytes  32.9 Mbits/sec    0    258 KBytes
[  5]   6.00-7.00   sec  4.41 MBytes  37.0 Mbits/sec    0    258 KBytes
[  5]   7.00-8.00   sec  4.41 MBytes  37.0 Mbits/sec    0    258 KBytes
[  5]   8.00-9.00   sec  3.92 MBytes  32.9 Mbits/sec    0    258 KBytes
[  5]   9.00-10.00  sec  3.86 MBytes  32.4 Mbits/sec    0    258 KBytes
[  5]  10.00-11.00  sec  3.92 MBytes  32.9 Mbits/sec    0    258 KBytes
[  5]  11.00-12.00  sec  2.76 MBytes  23.1 Mbits/sec    0    258 KBytes
[  5]  12.00-13.00  sec  3.92 MBytes  32.9 Mbits/sec    0    258 KBytes
[  5]  13.00-14.00  sec  4.41 MBytes  37.0 Mbits/sec    0    258 KBytes
[  5]  14.00-15.00  sec  5.02 MBytes  42.1 Mbits/sec    0    258 KBytes
[  5]  15.00-16.00  sec  4.41 MBytes  37.0 Mbits/sec    0    258 KBytes
[  5]  16.00-17.00  sec  4.47 MBytes  37.5 Mbits/sec    0    258 KBytes
[  5]  17.00-18.00  sec  4.53 MBytes  38.0 Mbits/sec    0    258 KBytes
[  5]  18.00-19.00  sec  2.76 MBytes  23.1 Mbits/sec    0    258 KBytes
[  5]  19.00-20.00  sec  3.06 MBytes  25.7 Mbits/sec    0    376 KBytes
[  5]  20.00-21.00  sec  2.33 MBytes  19.5 Mbits/sec    0    376 KBytes
[  5]  21.00-22.00  sec  3.00 MBytes  25.2 Mbits/sec    0    376 KBytes
[  5]  22.00-23.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  23.00-24.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  24.00-25.00  sec  2.94 MBytes  24.7 Mbits/sec    0    376 KBytes
[  5]  25.00-26.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  26.00-27.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  27.00-28.00  sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5]  28.00-29.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  29.00-30.00  sec  2.94 MBytes  24.7 Mbits/sec    0    376 KBytes
[  5]  30.00-31.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  31.00-32.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  32.00-33.00  sec  2.33 MBytes  19.5 Mbits/sec    0    376 KBytes
[  5]  33.00-34.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  34.00-35.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  35.00-36.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  36.00-37.00  sec  2.33 MBytes  19.5 Mbits/sec    0    376 KBytes
[  5]  37.00-38.00  sec  3.06 MBytes  25.7 Mbits/sec    0    376 KBytes
[  5]  38.00-39.00  sec  2.94 MBytes  24.7 Mbits/sec    0    376 KBytes
[  5]  39.00-40.00  sec  3.68 MBytes  30.8 Mbits/sec    0    376 KBytes
[  5]  40.00-41.00  sec  3.68 MBytes  30.8 Mbits/sec    0    376 KBytes
[  5]  41.00-42.00  sec  3.19 MBytes  26.7 Mbits/sec    0    376 KBytes
[  5]  42.00-43.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  43.00-44.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  44.00-45.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  45.00-46.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  46.00-47.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  47.00-48.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  48.00-49.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  49.00-50.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  50.00-51.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  51.00-52.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  52.00-53.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  53.00-54.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  54.00-55.00  sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5]  55.00-56.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  56.00-57.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  57.00-58.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  58.00-59.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  59.00-60.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  60.00-61.00  sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5]  61.00-62.00  sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5]  62.00-63.00  sec  3.00 MBytes  25.2 Mbits/sec    0    376 KBytes
[  5]  63.00-64.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  64.00-65.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  65.00-66.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  66.00-67.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  67.00-68.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  68.00-69.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  69.00-70.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  70.00-71.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  71.00-72.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  72.00-73.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  73.00-74.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  74.00-75.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  75.00-76.00  sec  1.53 MBytes  12.8 Mbits/sec    0    376 KBytes
[  5]  76.00-77.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  77.00-78.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  78.00-79.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  79.00-80.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  80.00-81.00  sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5]  81.00-82.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  82.00-83.00  sec  1.53 MBytes  12.8 Mbits/sec    0    376 KBytes
[  5]  83.00-84.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  84.00-85.00  sec  1.59 MBytes  13.4 Mbits/sec    0    376 KBytes
[  5]  85.00-86.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  86.00-87.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  87.00-88.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  88.00-89.00  sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5]  89.00-90.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  90.00-91.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  91.00-92.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  92.00-93.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  93.00-94.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  94.00-95.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  95.00-96.00  sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5]  96.00-97.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  97.00-98.00  sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5]  98.00-99.00  sec  1.53 MBytes  12.8 Mbits/sec    0    376 KBytes
[  5]  99.00-100.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 100.00-101.00 sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5] 101.00-102.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 102.00-103.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 103.00-104.00 sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5] 104.00-105.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 105.00-106.00 sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5] 106.00-107.00 sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5] 107.00-108.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 108.00-109.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 109.00-110.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 110.00-111.00 sec  1.47 MBytes  12.3 Mbits/sec    0    376 KBytes
[  5] 111.00-112.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 112.00-113.00 sec  1.53 MBytes  12.8 Mbits/sec    0    376 KBytes
[  5] 113.00-114.00 sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5] 114.00-115.00 sec  2.21 MBytes  18.5 Mbits/sec    0    376 KBytes
[  5] 115.00-116.00 sec  1.53 MBytes  12.8 Mbits/sec    0    376 KBytes
[  5] 116.00-117.00 sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5] 117.00-118.00 sec  2.27 MBytes  19.0 Mbits/sec    0    376 KBytes
[  5] 118.00-119.00 sec   753 KBytes  6.16 Mbits/sec    1    262 KBytes
[  5] 119.00-120.00 sec  1.47 MBytes  12.3 Mbits/sec    0    121 KBytes
[  5] 120.00-121.00 sec   816 KBytes  6.68 Mbits/sec    1    218 KBytes
[  5] 121.00-122.00 sec  2.21 MBytes  18.5 Mbits/sec    0    218 KBytes
[  5] 122.00-123.00 sec  1.59 MBytes  13.4 Mbits/sec    0    240 KBytes
[  5] 123.00-124.00 sec  2.21 MBytes  18.5 Mbits/sec    0    240 KBytes
[  5] 124.00-125.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 125.00-126.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 126.00-127.00 sec  1.53 MBytes  12.8 Mbits/sec    0    240 KBytes
[  5] 127.00-128.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 128.00-129.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 129.00-130.00 sec  2.21 MBytes  18.5 Mbits/sec    0    240 KBytes
[  5] 130.00-131.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 131.00-132.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 132.00-133.00 sec  2.21 MBytes  18.5 Mbits/sec    0    240 KBytes
[  5] 133.00-134.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 134.00-135.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 135.00-136.00 sec  2.33 MBytes  19.5 Mbits/sec    0    240 KBytes
[  5] 136.00-137.00 sec  1.47 MBytes  12.3 Mbits/sec    0    240 KBytes
[  5] 137.00-138.00 sec  2.21 MBytes  18.5 Mbits/sec    0    240 KBytes
[  5] 138.00-139.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 139.00-140.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 140.00-141.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 141.00-142.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 142.00-143.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 143.00-144.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 144.00-145.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 145.00-146.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 146.00-147.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 147.00-148.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 148.00-149.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 149.00-150.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 150.00-151.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 151.00-152.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 152.00-153.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 153.00-154.00 sec  2.94 MBytes  24.7 Mbits/sec    0    379 KBytes
[  5] 154.00-155.00 sec  2.33 MBytes  19.5 Mbits/sec    0    379 KBytes
[  5] 155.00-156.00 sec  2.94 MBytes  24.7 Mbits/sec    0    379 KBytes
[  5] 156.00-157.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 157.00-158.00 sec  2.45 MBytes  20.6 Mbits/sec    0    379 KBytes
[  5] 158.00-159.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 159.00-160.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 160.00-161.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 161.00-162.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 162.00-163.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 163.00-164.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 164.00-165.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 165.00-166.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 166.00-167.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 167.00-168.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 168.00-169.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 169.00-170.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 170.00-171.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 171.00-172.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 172.00-173.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 173.00-174.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 174.00-175.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 175.00-176.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 176.00-177.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 177.00-178.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 178.00-179.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 179.00-180.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 180.00-181.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 181.00-182.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 182.00-183.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 183.00-184.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 184.00-185.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 185.00-186.00 sec  1.47 MBytes  12.3 Mbits/sec    0    379 KBytes
[  5] 186.00-187.00 sec  2.21 MBytes  18.5 Mbits/sec    0    379 KBytes
[  5] 187.00-188.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 188.00-189.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 189.00-190.00 sec  1.59 MBytes  13.4 Mbits/sec    0    379 KBytes
[  5] 190.00-191.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 191.00-192.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 192.00-193.00 sec  3.00 MBytes  25.2 Mbits/sec    0    379 KBytes
[  5] 193.00-194.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 194.00-195.00 sec  3.00 MBytes  25.2 Mbits/sec    0    379 KBytes
[  5] 195.00-196.00 sec  1.53 MBytes  12.8 Mbits/sec    0    379 KBytes
[  5] 196.00-197.00 sec  3.00 MBytes  25.2 Mbits/sec    0    379 KBytes
[  5] 197.00-198.00 sec  2.27 MBytes  19.0 Mbits/sec    0    379 KBytes
[  5] 198.00-199.00 sec  2.94 MBytes  24.7 Mbits/sec    0    379 KBytes
[  5] 199.00-200.00 sec  3.00 MBytes  25.2 Mbits/sec    0    379 KBytes
[  5] 200.00-201.00 sec  3.49 MBytes  29.3 Mbits/sec    0    543 KBytes
[  5] 201.00-202.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 202.00-203.00 sec  3.12 MBytes  26.2 Mbits/sec    0    543 KBytes
[  5] 203.00-204.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 204.00-205.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 205.00-206.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 206.00-207.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 207.00-208.00 sec  3.12 MBytes  26.2 Mbits/sec    0    543 KBytes
[  5] 208.00-209.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 209.00-210.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 210.00-211.00 sec  3.25 MBytes  27.2 Mbits/sec    0    543 KBytes
[  5] 211.00-212.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 212.00-213.00 sec  3.25 MBytes  27.2 Mbits/sec    0    543 KBytes
[  5] 213.00-214.00 sec  3.31 MBytes  27.8 Mbits/sec    0    543 KBytes
[  5] 214.00-215.00 sec  3.31 MBytes  27.8 Mbits/sec    0    543 KBytes
[  5] 215.00-216.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 216.00-217.00 sec  3.25 MBytes  27.2 Mbits/sec    0    543 KBytes
[  5] 217.00-218.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 218.00-219.00 sec  2.21 MBytes  18.5 Mbits/sec    0    543 KBytes
[  5] 219.00-220.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 220.00-221.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 221.00-222.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 222.00-223.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 223.00-224.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 224.00-225.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 225.00-226.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 226.00-227.00 sec  3.19 MBytes  26.7 Mbits/sec    0    543 KBytes
[  5] 227.00-228.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 228.00-229.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 229.00-230.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 230.00-231.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 231.00-232.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 232.00-233.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 233.00-234.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 234.00-235.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 235.00-236.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 236.00-237.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 237.00-238.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 238.00-239.00 sec  3.19 MBytes  26.7 Mbits/sec    0    543 KBytes
[  5] 239.00-240.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 240.00-241.00 sec  3.12 MBytes  26.2 Mbits/sec    0    543 KBytes
[  5] 241.00-242.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 242.00-243.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 243.00-244.00 sec  2.21 MBytes  18.5 Mbits/sec    0    543 KBytes
[  5] 244.00-245.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 245.00-246.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 246.00-247.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 247.00-248.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 248.00-249.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 249.00-250.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 250.00-251.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 251.00-252.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 252.00-253.00 sec  3.12 MBytes  26.2 Mbits/sec    0    543 KBytes
[  5] 253.00-254.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 254.00-255.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 255.00-256.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 256.00-257.00 sec  4.29 MBytes  36.0 Mbits/sec    0    543 KBytes
[  5] 257.00-258.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 258.00-259.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 259.00-260.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 260.00-261.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 261.00-262.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 262.00-263.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 263.00-264.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 264.00-265.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 265.00-266.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 266.00-267.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 267.00-268.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 268.00-269.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 269.00-270.00 sec  1.04 MBytes  8.74 Mbits/sec    0    543 KBytes
[  5] 270.00-271.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 271.00-272.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 272.00-273.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 273.00-274.00 sec  3.19 MBytes  26.7 Mbits/sec    0    543 KBytes
[  5] 274.00-275.00 sec  3.25 MBytes  27.2 Mbits/sec    0    543 KBytes
[  5] 275.00-276.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 276.00-277.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 277.00-278.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 278.00-279.00 sec  1.04 MBytes  8.74 Mbits/sec    0    543 KBytes
[  5] 279.00-280.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 280.00-281.00 sec  2.21 MBytes  18.5 Mbits/sec    0    543 KBytes
[  5] 281.00-282.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 282.00-283.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 283.00-284.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 284.00-285.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 285.00-286.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 286.00-287.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 287.00-288.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 288.00-289.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 289.00-290.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 290.00-291.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 291.00-292.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 292.00-293.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 293.00-294.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 294.00-295.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 295.00-296.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 296.00-297.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 297.00-298.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 298.00-299.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 299.00-300.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 300.00-301.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 301.00-302.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 302.00-303.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 303.00-304.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 304.00-305.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 305.00-306.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 306.00-307.00 sec  2.21 MBytes  18.5 Mbits/sec    0    543 KBytes
[  5] 307.00-308.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 308.00-309.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 309.00-310.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 310.00-311.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 311.00-312.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 312.00-313.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 313.00-314.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 314.00-315.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 315.00-316.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 316.00-317.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 317.00-318.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 318.00-319.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 319.00-320.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 320.00-321.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 321.00-322.00 sec  1.04 MBytes  8.73 Mbits/sec    0    543 KBytes
[  5] 322.00-323.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 323.00-324.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 324.00-325.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 325.00-326.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 326.00-327.00 sec  1.10 MBytes  9.25 Mbits/sec    0    543 KBytes
[  5] 327.00-328.00 sec  2.14 MBytes  18.0 Mbits/sec    0    543 KBytes
[  5] 328.00-329.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 329.00-330.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 330.00-331.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
[  5] 330.00-331.00 sec  2.08 MBytes  17.5 Mbits/sec    0    543 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-331.00 sec   693 MBytes  17.6 Mbits/sec    2             sender
[  5]   0.00-331.00 sec  0.00 Bytes  0.00 bits/sec                  receiver
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
