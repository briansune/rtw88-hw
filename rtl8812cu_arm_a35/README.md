# RTL8812CU USB Dongle Testing

### Test Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="https://github.com/user-attachments/assets/05936576-5042-4a26-8e06-9bc724a1b6dc" height="400"/>|<img src="https://github.com/user-attachments/assets/a5126d9b-2cbf-4e88-9802-225e5afcb6e3" height="400"/>|

```
uname -a
Linux briansune 6.1.111-rt42

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
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Vendor Specific Class, Driver=rtw_8822cu, 480M
```

<details>

<summary>USB Details</summary>

```
lsusb -v -s 001:002

Bus 001 Device 002: ID 0bda:c812 Realtek Semiconductor Corp. 802.11ac NIC
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xc812
  bcdDevice            0.00
  iManufacturer           1 Realtek
  iProduct                2 802.11ac NIC
  iSerial                 3 123456
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength       0x0035
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
[   92.283197] rtw_core: loading out-of-tree module taints kernel.
[  150.081257] rtw_8822cu 1-1:1.0: WOW Firmware version 9.9.4, H2C version 15
[  150.091174] rtw_8822cu 1-1:1.0: Firmware version 9.9.15, H2C version 15
[  150.274472] usbcore: registered new interface driver rtw_8822cu

Module                  Size  Used by
rtw_8822cu             16384  0
rtw_8822c             471040  1 rtw_8822cu
rtw_usb                24576  1 rtw_8822cu
rtw_core              217088  2 rtw_usb,rtw_8822c
```
### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.16  netmask 255.255.252.0  broadcast 192.168.3.255
        inet6   prefixlen 64  scopeid 0x20<link>
        ether   txqueuelen 1000  (Ethernet)
        RX packets 99  bytes 14963 (14.9 KB)
        RX errors 0  dropped 22  overruns 0  frame 0
        TX packets 70  bytes 11274 (11.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Network Speed Test via Ookla

```
#2G Band
Idle Latency:     4.30 ms   (jitter: 1.76ms, low: 3.56ms, high: 5.72ms)
    Download:    67.74 Mbps (data used: 73.7 MB)
                 41.22 ms   (jitter: 16.69ms, low: 7.85ms, high: 109.91ms)
      Upload:    46.57 Mbps (data used: 72.8 MB)
                231.91 ms   (jitter: 65.79ms, low: 19.32ms, high: 1132.96ms)

#5G band
   Speedtest by Ookla

Idle Latency:     4.71 ms   (jitter: 41.28ms, low: 4.50ms, high: 87.08ms)
    Download:   268.32 Mbps (data used: 352.3 MB)
                 28.23 ms   (jitter: 7.55ms, low: 4.61ms, high: 61.37ms)
      Upload:    99.51 Mbps (data used: 132.6 MB)
                115.96 ms   (jitter: 47.88ms, low: 6.62ms, high: 365.65ms)
 Packet Loss:     0.0%
```

### Network Ping Tests

#### DNS-Ping

```
# 2G band
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=12.6 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=4.07 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=6.51 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=9.31 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=4.72 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=5.00 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=4.08 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=4.66 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=8.29 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=15.3 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=7.91 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=3.90 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=8.44 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=3.96 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=5.95 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=8.18 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=4.05 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=6.01 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=3.95 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 3.900/6.537/15.250/3.051 ms

# 5G Band

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=4.15 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=3.80 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=7.16 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=3.81 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=3.93 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=4.04 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=3.77 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=4.18 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=3.86 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=3.91 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=3.80 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=10.4 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=4.54 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=4.18 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=3.75 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=8.16 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=3.79 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=3.88 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=4.25 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=10.1 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19032ms
rtt min/avg/max/mdev = 3.750/4.969/10.376/2.081 ms
```

#### Self-Ping 

```
# 2G band
PING 192.168.1.16 (192.168.1.16) 10000(10028) bytes of data.
10008 bytes from 192.168.1.16: icmp_seq=1 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.16: icmp_seq=2 ttl=64 time=0.139 ms
10008 bytes from 192.168.1.16: icmp_seq=3 ttl=64 time=0.110 ms
10008 bytes from 192.168.1.16: icmp_seq=4 ttl=64 time=0.086 ms
10008 bytes from 192.168.1.16: icmp_seq=5 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.16: icmp_seq=6 ttl=64 time=0.148 ms
10008 bytes from 192.168.1.16: icmp_seq=7 ttl=64 time=0.144 ms
10008 bytes from 192.168.1.16: icmp_seq=8 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.16: icmp_seq=9 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.16: icmp_seq=10 ttl=64 time=0.086 ms
10008 bytes from 192.168.1.16: icmp_seq=11 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.16: icmp_seq=12 ttl=64 time=0.083 ms
10008 bytes from 192.168.1.16: icmp_seq=13 ttl=64 time=0.143 ms
10008 bytes from 192.168.1.16: icmp_seq=14 ttl=64 time=0.140 ms
10008 bytes from 192.168.1.16: icmp_seq=15 ttl=64 time=0.090 ms
10008 bytes from 192.168.1.16: icmp_seq=16 ttl=64 time=0.084 ms
10008 bytes from 192.168.1.16: icmp_seq=17 ttl=64 time=0.113 ms
10008 bytes from 192.168.1.16: icmp_seq=18 ttl=64 time=0.104 ms
10008 bytes from 192.168.1.16: icmp_seq=19 ttl=64 time=0.147 ms
10008 bytes from 192.168.1.16: icmp_seq=20 ttl=64 time=0.143 ms

--- 192.168.1.16 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19458ms
rtt min/avg/max/mdev = 0.083/0.118/0.148/0.023 ms
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
          Bit Rate=162 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=58/70  Signal level=-52 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:16   Missed beacon:0
```

### Server & Client Test via iperf3 (PC-Router-DUT)

Any BT or 2.4G-based devices are degrading the TRX performance.

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.18, port 50359
[  5] local 192.168.1.16 port 5201 connected to 192.168.1.18 port 50360
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  5.37 MBytes  45.1 Mbits/sec    4    133 KBytes
[  5]   1.00-2.00   sec  4.84 MBytes  40.6 Mbits/sec    1    133 KBytes
[  5]   2.00-3.00   sec  4.23 MBytes  35.5 Mbits/sec    0    133 KBytes
[  5]   3.00-4.00   sec  4.78 MBytes  40.1 Mbits/sec    0    257 KBytes
[  5]   4.00-5.00   sec  4.84 MBytes  40.6 Mbits/sec    0    259 KBytes
[  5]   5.00-6.00   sec  5.58 MBytes  46.8 Mbits/sec    0    259 KBytes
[  5]   6.00-7.00   sec  5.64 MBytes  47.3 Mbits/sec    0    259 KBytes
[  5]   7.00-8.00   sec  4.29 MBytes  36.0 Mbits/sec    0    259 KBytes
[  5]   8.00-9.00   sec  5.21 MBytes  43.7 Mbits/sec    1    259 KBytes
[  5]   9.00-10.00  sec  5.45 MBytes  45.7 Mbits/sec    0    259 KBytes
[  5]  10.00-11.00  sec  5.02 MBytes  42.1 Mbits/sec    0    259 KBytes
[  5]  11.00-12.00  sec  4.96 MBytes  41.6 Mbits/sec    0    259 KBytes
[  5]  12.00-13.00  sec  2.63 MBytes  22.1 Mbits/sec    0    259 KBytes
[  5]  13.00-14.00  sec  4.29 MBytes  36.0 Mbits/sec    0    259 KBytes
[  5]  14.00-15.00  sec  5.51 MBytes  46.3 Mbits/sec    0    259 KBytes
[  5]  15.00-16.00  sec  6.07 MBytes  50.9 Mbits/sec    0    259 KBytes
[  5]  16.00-17.00  sec  4.23 MBytes  35.5 Mbits/sec    0    259 KBytes
[  5]  17.00-18.00  sec  5.70 MBytes  47.8 Mbits/sec    0    259 KBytes
[  5]  18.00-19.00  sec  6.31 MBytes  52.9 Mbits/sec    0    259 KBytes
[  5]  19.00-20.00  sec  6.25 MBytes  52.4 Mbits/sec    0    259 KBytes
[  5]  20.00-21.00  sec  6.86 MBytes  57.6 Mbits/sec    1    528 KBytes
[  5]  21.00-22.00  sec  6.56 MBytes  55.0 Mbits/sec    0    528 KBytes
[  5]  22.00-23.00  sec  5.51 MBytes  46.3 Mbits/sec    0    528 KBytes
[  5]  23.00-24.00  sec  3.54 MBytes  29.7 Mbits/sec    0   1024 KBytes
[  5]  24.00-25.00  sec  5.00 MBytes  42.0 Mbits/sec    0   1024 KBytes
[  5]  25.00-26.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  26.00-27.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  27.00-28.00  sec  3.75 MBytes  31.5 Mbits/sec    0   1024 KBytes
[  5]  28.00-29.00  sec  5.00 MBytes  42.0 Mbits/sec    0   1024 KBytes
[  5]  29.00-30.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  30.00-31.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  31.00-32.00  sec  3.75 MBytes  31.5 Mbits/sec    0   1024 KBytes
[  5]  32.00-33.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  33.00-34.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  34.00-35.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  35.00-36.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  36.00-37.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  37.00-38.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  38.00-39.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  39.00-40.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  40.00-41.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  41.00-42.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1024 KBytes
[  5]  42.00-43.00  sec  4.98 MBytes  41.7 Mbits/sec    0   1024 KBytes
[  5]  43.00-44.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  44.00-45.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  45.00-46.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1024 KBytes
[  5]  46.00-47.00  sec  6.23 MBytes  52.3 Mbits/sec    0   1024 KBytes
[  5]  47.00-48.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1024 KBytes
[  5]  48.00-49.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1024 KBytes
[  5]  49.00-50.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1.00 MBytes
[  5]  50.00-51.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.00 MBytes
[  5]  51.00-52.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1.00 MBytes
[  5]  52.00-53.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.00 MBytes
[  5]  53.00-54.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1.00 MBytes
[  5]  54.00-55.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.00 MBytes
[  5]  55.00-56.00  sec  7.50 MBytes  62.9 Mbits/sec    0   1.00 MBytes
[  5]  56.00-57.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1.00 MBytes
[  5]  57.00-58.00  sec  6.25 MBytes  52.4 Mbits/sec    0   1.00 MBytes
[  5]  58.00-59.00  sec  5.00 MBytes  41.9 Mbits/sec    0   1.00 MBytes
[  5]  59.00-60.00  sec  0.00 Bytes  0.00 bits/sec    1    254 KBytes
[  5]  60.00-61.00  sec  1.25 MBytes  10.5 Mbits/sec    2   94.1 KBytes
[  5]  61.00-62.00  sec  0.00 Bytes  0.00 bits/sec    0    101 KBytes
[  5]  62.00-63.00  sec  0.00 Bytes  0.00 bits/sec    1   69.9 KBytes
[  5]  63.00-64.00  sec  0.00 Bytes  0.00 bits/sec    1   51.3 KBytes
[  5]  64.00-65.00  sec  1.25 MBytes  10.5 Mbits/sec    0   69.9 KBytes
[  5]  65.00-66.00  sec  2.50 MBytes  21.0 Mbits/sec    1   64.2 KBytes
[  5]  66.00-67.00  sec  3.74 MBytes  31.3 Mbits/sec    0   99.8 KBytes
[  5]  67.00-68.00  sec  3.75 MBytes  31.5 Mbits/sec    0    125 KBytes
[  5]  68.00-69.00  sec  3.75 MBytes  31.5 Mbits/sec    0    145 KBytes
[  5]  69.00-70.00  sec  3.75 MBytes  31.4 Mbits/sec    0    163 KBytes
[  5]  70.00-71.00  sec  3.75 MBytes  31.5 Mbits/sec    0    184 KBytes
[  5]  71.00-72.00  sec  2.50 MBytes  21.0 Mbits/sec    0    194 KBytes
[  5]  72.00-73.00  sec  2.50 MBytes  21.0 Mbits/sec    0    201 KBytes
[  5]  73.00-74.00  sec  2.50 MBytes  21.0 Mbits/sec    0    210 KBytes
[  5]  74.00-75.00  sec  2.50 MBytes  21.0 Mbits/sec    0    220 KBytes
[  5]  75.00-76.00  sec  2.50 MBytes  21.0 Mbits/sec    0    238 KBytes
[  5]  76.00-77.00  sec  5.00 MBytes  42.0 Mbits/sec    0    321 KBytes
[  5]  77.00-78.00  sec  5.00 MBytes  41.9 Mbits/sec    0    429 KBytes
[  5]  78.00-79.00  sec  6.25 MBytes  52.4 Mbits/sec    0    518 KBytes
[  5]  79.00-80.00  sec  7.50 MBytes  62.9 Mbits/sec    0    518 KBytes
[  5]  80.00-81.00  sec  5.00 MBytes  41.9 Mbits/sec    0    518 KBytes
[  5]  81.00-82.00  sec  5.00 MBytes  41.9 Mbits/sec    0    518 KBytes
[  5]  82.00-83.00  sec  6.25 MBytes  52.4 Mbits/sec    0    518 KBytes
[  5]  83.00-84.00  sec  6.25 MBytes  52.4 Mbits/sec    0    518 KBytes
[  5]  84.00-85.00  sec  5.00 MBytes  41.9 Mbits/sec    0    518 KBytes
[  5]  85.00-86.00  sec  6.25 MBytes  52.4 Mbits/sec    0    518 KBytes
[  5]  86.00-87.00  sec  5.00 MBytes  41.9 Mbits/sec    0    518 KBytes
[  5]  87.00-88.00  sec  6.25 MBytes  52.4 Mbits/sec    0    518 KBytes
[  5]  88.00-89.00  sec  6.25 MBytes  52.4 Mbits/sec    0    518 KBytes
[  5]  89.00-90.00  sec  1.25 MBytes  10.5 Mbits/sec    0    518 KBytes
[  5]  90.00-91.00  sec  2.50 MBytes  21.0 Mbits/sec    0    518 KBytes
[  5]  91.00-92.00  sec  3.75 MBytes  31.4 Mbits/sec  186   69.9 KBytes
[  5]  92.00-93.00  sec  2.50 MBytes  21.0 Mbits/sec   20   71.3 KBytes
[  5]  93.00-94.00  sec  3.75 MBytes  31.5 Mbits/sec    1   79.8 KBytes
[  5]  94.00-95.00  sec  2.50 MBytes  21.0 Mbits/sec    1   77.0 KBytes
[  5]  95.00-96.00  sec  5.00 MBytes  42.0 Mbits/sec    2   85.5 KBytes
[  5]  96.00-97.00  sec  3.75 MBytes  31.5 Mbits/sec    0    117 KBytes
[  5]  97.00-98.00  sec  5.00 MBytes  41.9 Mbits/sec    0    145 KBytes
[  5]  97.00-98.00  sec  5.00 MBytes  41.9 Mbits/sec    0    145 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-98.00  sec   472 MBytes  40.4 Mbits/sec  223             sender
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
Accepted connection from 192.168.175.86, port 52786
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 52787
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  1.12 MBytes  9.36 Mbits/sec    0    130 KBytes
[  5]   1.00-2.00   sec   565 KBytes  4.63 Mbits/sec    0    130 KBytes
[  5]   2.00-3.00   sec   565 KBytes  4.63 Mbits/sec    0    130 KBytes
[  5]   3.00-4.00   sec   565 KBytes  4.62 Mbits/sec    0    130 KBytes
[  5]   4.00-5.00   sec   565 KBytes  4.63 Mbits/sec    0    130 KBytes
[  5]   5.00-6.00   sec   565 KBytes  4.62 Mbits/sec    0    130 KBytes
[  5]   6.00-7.00   sec   533 KBytes  4.37 Mbits/sec    0    130 KBytes
[  5]   7.00-8.00   sec   753 KBytes  6.17 Mbits/sec    0    130 KBytes
[  5]   8.00-9.00   sec   565 KBytes  4.62 Mbits/sec    0    130 KBytes
[  5]   9.00-10.00  sec   565 KBytes  4.63 Mbits/sec    0    130 KBytes
[  5]  10.00-11.00  sec   502 KBytes  4.11 Mbits/sec    0    130 KBytes
[  5]  11.00-12.00  sec   565 KBytes  4.62 Mbits/sec    0    130 KBytes
[  5]  12.00-13.00  sec   565 KBytes  4.62 Mbits/sec    0    130 KBytes
[  5]  13.00-14.00  sec   533 KBytes  4.37 Mbits/sec    0    130 KBytes
[  5]  14.00-15.00  sec  1.13 MBytes  9.51 Mbits/sec    0    130 KBytes
[  5]  15.00-16.00  sec  2.82 MBytes  23.6 Mbits/sec    0    130 KBytes
[  5]  16.00-17.00  sec  5.39 MBytes  45.2 Mbits/sec    0    130 KBytes
[  5]  17.00-18.00  sec  4.53 MBytes  38.0 Mbits/sec    0    130 KBytes
[  5]  18.00-19.00  sec  5.64 MBytes  47.3 Mbits/sec    0    130 KBytes
[  5]  19.00-20.00  sec  5.67 MBytes  47.5 Mbits/sec    0    130 KBytes
[  5]  20.00-21.00  sec  5.88 MBytes  49.3 Mbits/sec    0    130 KBytes
[  5]  21.00-22.00  sec  6.00 MBytes  50.4 Mbits/sec    0    130 KBytes
[  5]  22.00-23.00  sec  6.07 MBytes  50.9 Mbits/sec    0    130 KBytes
[  5]  23.00-24.00  sec  5.58 MBytes  46.8 Mbits/sec    0    130 KBytes
[  5]  24.00-25.00  sec  5.58 MBytes  46.8 Mbits/sec    0    130 KBytes
[  5]  25.00-26.00  sec  5.64 MBytes  47.3 Mbits/sec    0    130 KBytes
[  5]  26.00-27.00  sec  4.10 MBytes  34.4 Mbits/sec    0    130 KBytes
[  5]  27.00-28.00  sec   627 KBytes  5.14 Mbits/sec    0    130 KBytes
[  5]  28.00-29.00  sec   314 KBytes  2.57 Mbits/sec    0    130 KBytes
[  5]  29.00-30.00  sec   314 KBytes  2.57 Mbits/sec    0    130 KBytes
[  5]  30.00-31.00  sec   627 KBytes  5.14 Mbits/sec    0    130 KBytes
[  5]  31.00-32.00  sec   376 KBytes  3.08 Mbits/sec    0    130 KBytes
[  5]  32.00-33.00  sec   314 KBytes  2.57 Mbits/sec    0    130 KBytes
[  5]  33.00-34.00  sec  3.74 MBytes  31.4 Mbits/sec    0    130 KBytes
[  5]  34.00-35.00  sec  4.17 MBytes  34.9 Mbits/sec   58   52.8 KBytes
[  5]  35.00-36.00  sec   627 KBytes  5.14 Mbits/sec    8   52.8 KBytes
[  5]  36.00-37.00  sec   627 KBytes  5.14 Mbits/sec    0   52.8 KBytes
[  5]  37.00-38.00  sec   314 KBytes  2.57 Mbits/sec    0   57.0 KBytes
[  5]  38.00-39.00  sec   627 KBytes  5.14 Mbits/sec    0   64.2 KBytes
[  5]  39.00-40.00  sec   627 KBytes  5.14 Mbits/sec    0   71.3 KBytes
[  5]  40.00-41.00  sec   627 KBytes  5.14 Mbits/sec    0   78.4 KBytes
[  5]  41.00-42.00  sec   627 KBytes  5.14 Mbits/sec    0   85.5 KBytes
[  5]  42.00-43.00  sec   627 KBytes  5.14 Mbits/sec    0    123 KBytes
[  5]  43.00-44.00  sec   627 KBytes  5.14 Mbits/sec    0    135 KBytes
[  5]  44.00-45.00  sec   627 KBytes  5.14 Mbits/sec    0    135 KBytes
[  5]  45.00-46.00  sec   314 KBytes  2.57 Mbits/sec    0    135 KBytes
[  5]  46.00-47.00  sec   627 KBytes  5.14 Mbits/sec    0    135 KBytes
[  5]  47.00-48.00  sec   314 KBytes  2.57 Mbits/sec    0    135 KBytes
[  5]  48.00-49.00  sec   627 KBytes  5.14 Mbits/sec    0    135 KBytes
[  5]  48.00-49.00  sec   627 KBytes  5.14 Mbits/sec    0    135 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-49.00  sec  90.4 MBytes  15.5 Mbits/sec   66             sender
```

</details>
