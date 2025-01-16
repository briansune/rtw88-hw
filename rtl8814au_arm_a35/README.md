# RTL8814AU USB Dongle Testing

### Test USB Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="./image/8814au/rtl8814au_arm_a35.JPG" height="400"/>|<img src="./image/8814au/rtl8814au_pcba.png" height="400"/>|

```
6.1.111-rt42

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

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
Flags:                                fp asimd evtstrm aes pmull sha1 sha2 crc32 cpuid
```

### USB Tree

```
Before driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=, 480M

After driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=rtw_8814au, 480M
```

<details>

<summary>USB Details</summary>

```

Bus 001 Device 003: ID 0bda:8813 Realtek Semiconductor Corp. RTL8814AU 802.11a/b/g/n/ac Wireless Adapter
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.10
  bDeviceClass            0 
  bDeviceSubClass         0 
  bDeviceProtocol         0 
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0x8813 RTL8814AU 802.11a/b/g/n/ac Wireless Adapter
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
Binary Object Store Descriptor:
  bLength                 5
  bDescriptorType        15
  wTotalLength       0x0016
  bNumDeviceCaps          2
  USB 2.0 Extension Device Capability:
    bLength                 7
    bDescriptorType        16
    bDevCapabilityType      2
    bmAttributes   0x00000002
      HIRD Link Power Management (LPM) Supported
  SuperSpeed USB Device Capability:
    bLength                10
    bDescriptorType        16
    bDevCapabilityType      3
    bmAttributes         0x00
    wSpeedsSupported   0x000e
      Device can operate at Full Speed (12Mbps)
      Device can operate at High Speed (480Mbps)
      Device can operate at SuperSpeed (5Gbps)
    bFunctionalitySupport   1
      Lowest fully-functional device speed is Full Speed (12Mbps)
    bU1DevExitLat          10 micro seconds
    bU2DevExitLat        1023 micro seconds
Device Status:     0x0002
  (Bus Powered)
  Remote Wakeup Enabled
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8814au             16384  0
rtw_8814a             245760  1 rtw_8814au
rtw_usb                24576  1 rtw_8814au
rtw_core              217088  2 rtw_usb,rtw_8814a
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy3
	max # scan SSIDs: 4
	max scan IEs length: 2243 bytes
	max # sched scan SSIDs: 0
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
			* 2467 MHz [12] (20.0 dBm) (no IR)
			* 2472 MHz [13] (20.0 dBm) (no IR)
			* 2484 MHz [14] (20.0 dBm) (no IR)
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
			* 5180 MHz [36] (20.0 dBm) (no IR)
			* 5200 MHz [40] (20.0 dBm) (no IR)
			* 5220 MHz [44] (20.0 dBm) (no IR)
			* 5240 MHz [48] (20.0 dBm) (no IR)
			* 5260 MHz [52] (20.0 dBm) (no IR, radar detection)
			* 5280 MHz [56] (20.0 dBm) (no IR, radar detection)
			* 5300 MHz [60] (20.0 dBm) (no IR, radar detection)
			* 5320 MHz [64] (20.0 dBm) (no IR, radar detection)
			* 5500 MHz [100] (20.0 dBm) (no IR, radar detection)
			* 5520 MHz [104] (20.0 dBm) (no IR, radar detection)
			* 5540 MHz [108] (20.0 dBm) (no IR, radar detection)
			* 5560 MHz [112] (20.0 dBm) (no IR, radar detection)
			* 5580 MHz [116] (20.0 dBm) (no IR, radar detection)
			* 5600 MHz [120] (20.0 dBm) (no IR, radar detection)
			* 5620 MHz [124] (20.0 dBm) (no IR, radar detection)
			* 5640 MHz [128] (20.0 dBm) (no IR, radar detection)
			* 5660 MHz [132] (20.0 dBm) (no IR, radar detection)
			* 5680 MHz [136] (20.0 dBm) (no IR, radar detection)
			* 5700 MHz [140] (20.0 dBm) (no IR, radar detection)
			* 5720 MHz [144] (20.0 dBm) (no IR, radar detection)
			* 5745 MHz [149] (20.0 dBm) (no IR)
			* 5765 MHz [153] (20.0 dBm) (no IR)
			* 5785 MHz [157] (20.0 dBm) (no IR)
			* 5805 MHz [161] (20.0 dBm) (no IR)
			* 5825 MHz [165] (20.0 dBm) (no IR)
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

### Network Manager - Band 2.4

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.25  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 19  bytes 2781 (2.7 KB)
        RX errors 0  dropped 1  overruns 0  frame 0
        TX packets 52  bytes 9124 (9.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.437 GHz  
          Bit Rate=108 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=62/70  Signal level=-48 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 17.59 Mbit/s
Testing upload speed......................................................................................................
Upload: 31.48 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=161 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=6.42 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=5.92 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=4.22 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=9.05 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=4.00 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=4.70 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=4.73 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=3.68 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=3.97 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=4.26 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=6.66 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=3.93 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=6.11 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=14.1 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=10.9 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=4.66 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=10.8 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=8.99 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=8.24 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19028ms
rtt min/avg/max/mdev = 3.679/14.293/160.545/33.670 ms
```

#### Self-Ping 

```
PING 192.168.1.25 (192.168.1.25) 10000(10028) bytes of data.
10008 bytes from 192.168.1.25: icmp_seq=1 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.25: icmp_seq=2 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.25: icmp_seq=3 ttl=64 time=0.152 ms
10008 bytes from 192.168.1.25: icmp_seq=4 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.25: icmp_seq=5 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.25: icmp_seq=6 ttl=64 time=0.141 ms
10008 bytes from 192.168.1.25: icmp_seq=7 ttl=64 time=0.092 ms
10008 bytes from 192.168.1.25: icmp_seq=8 ttl=64 time=0.082 ms
10008 bytes from 192.168.1.25: icmp_seq=9 ttl=64 time=0.147 ms
10008 bytes from 192.168.1.25: icmp_seq=10 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.25: icmp_seq=11 ttl=64 time=0.118 ms
10008 bytes from 192.168.1.25: icmp_seq=12 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.25: icmp_seq=13 ttl=64 time=0.101 ms
10008 bytes from 192.168.1.25: icmp_seq=14 ttl=64 time=0.098 ms
10008 bytes from 192.168.1.25: icmp_seq=15 ttl=64 time=0.090 ms
10008 bytes from 192.168.1.25: icmp_seq=16 ttl=64 time=0.150 ms
10008 bytes from 192.168.1.25: icmp_seq=17 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.25: icmp_seq=18 ttl=64 time=0.122 ms
10008 bytes from 192.168.1.25: icmp_seq=19 ttl=64 time=0.097 ms
10008 bytes from 192.168.1.25: icmp_seq=20 ttl=64 time=0.104 ms

--- 192.168.1.25 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19442ms
rtt min/avg/max/mdev = 0.082/0.120/0.152/0.022 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.29, port 58754
[  5] local 192.168.1.25 port 5201 connected to 192.168.1.29 port 58755
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  4.30 MBytes  36.1 Mbits/sec    1    143 KBytes       
[  5]   1.00-2.00   sec  4.66 MBytes  39.1 Mbits/sec    0    143 KBytes       
[  5]   2.00-3.00   sec  2.70 MBytes  22.6 Mbits/sec    0    143 KBytes       
[  5]   3.00-4.00   sec  3.55 MBytes  29.8 Mbits/sec    1    143 KBytes       
[  5]   4.00-5.00   sec  3.68 MBytes  30.8 Mbits/sec    1    143 KBytes       
[  5]   5.00-6.00   sec  4.41 MBytes  37.0 Mbits/sec    0    261 KBytes       
[  5]   6.00-7.00   sec  3.43 MBytes  28.8 Mbits/sec    0    269 KBytes       
[  5]   7.00-8.00   sec  2.88 MBytes  24.2 Mbits/sec    0    269 KBytes       
[  5]   8.00-9.00   sec  2.57 MBytes  21.6 Mbits/sec    0    269 KBytes       
[  5]   9.00-10.00  sec  3.86 MBytes  32.4 Mbits/sec    0    269 KBytes       
[  5]  10.00-11.00  sec  2.63 MBytes  22.1 Mbits/sec    0    269 KBytes       
[  5]  11.00-12.00  sec  2.88 MBytes  24.2 Mbits/sec    0    269 KBytes       
[  5]  12.00-13.00  sec  3.68 MBytes  30.8 Mbits/sec    0    269 KBytes       
[  5]  13.00-14.00  sec  2.33 MBytes  19.5 Mbits/sec    0    269 KBytes       
[  5]  14.00-15.00  sec  2.21 MBytes  18.5 Mbits/sec    0    269 KBytes       
[  5]  15.00-16.00  sec  2.94 MBytes  24.7 Mbits/sec    0    269 KBytes       
[  5]  16.00-17.00  sec  3.00 MBytes  25.2 Mbits/sec    0    269 KBytes       
[  5]  17.00-18.00  sec   565 KBytes  4.62 Mbits/sec    0    269 KBytes       
[  5]  18.00-19.00  sec  0.00 Bytes  0.00 bits/sec    0    235 KBytes       
[  5]  19.00-20.00  sec  0.00 Bytes  0.00 bits/sec    1    188 KBytes       
[  5]  20.00-21.00  sec  0.00 Bytes  0.00 bits/sec    1    188 KBytes       
[  5]  21.00-22.00  sec  0.00 Bytes  0.00 bits/sec    0    190 KBytes       
[  5]  22.00-23.00  sec  0.00 Bytes  0.00 bits/sec    0    195 KBytes       
[  5]  23.00-24.00  sec  0.00 Bytes  0.00 bits/sec    0    195 KBytes       
[  5]  24.00-25.00  sec   565 KBytes  4.63 Mbits/sec    0    231 KBytes       
[  5]  25.00-26.00  sec   565 KBytes  4.62 Mbits/sec    0    265 KBytes       
[  5]  26.00-27.00  sec  1.10 MBytes  9.25 Mbits/sec    0    244 KBytes       
[  5]  27.00-28.00  sec   565 KBytes  4.63 Mbits/sec    1    195 KBytes       
[  5]  28.00-29.00  sec  1.16 MBytes  9.76 Mbits/sec    0    215 KBytes       
[  5]  29.00-30.00  sec  4.10 MBytes  34.4 Mbits/sec    0    224 KBytes       
[  5]  30.00-30.06  sec   565 KBytes  80.4 Mbits/sec    0    224 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.06  sec  64.8 MBytes  18.1 Mbits/sec    6             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  146.055028] rtw_core: loading out-of-tree module taints kernel.
[  146.353093] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  146.476656] usbcore: registered new interface driver rtw_8814au
[  147.169407] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  462.066417] rtw_8814au 1-1:1.0: firmware failed to leave lps state
[  489.454363] rtw_8814au 1-1:1.0: failed to get tx report from firmware
[  708.709362] usbcore: deregistering interface driver rtw_8814au
[  715.067467] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  715.240726] usbcore: registered new interface driver rtw_8814au
[  940.208345] usbcore: deregistering interface driver rtw_8814au
[  946.303076] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  946.472606] usbcore: registered new interface driver rtw_8814au
```

</details>

### Network Manager - Band 5G

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.25  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 45287  bytes 25432771 (25.4 MB)
        RX errors 0  dropped 22  overruns 0  frame 0
        TX packets 82191  bytes 113752062 (113.7 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 5G

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:5.805 GHz  
          Bit Rate=468 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=40/70  Signal level=-70 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 5G

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 206.38 Mbit/s
Testing upload speed......................................................................................................
Upload: 99.66 Mbit/s
```

### Network Ping Tests - Band 5G

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=25.7 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=4.86 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=6.42 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=3.71 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=4.41 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=8.60 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=4.39 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=5.36 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=4.80 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=3.78 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=5.86 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=4.95 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=107 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=5.20 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=4.46 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=4.03 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=5.86 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=4.43 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=6.31 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19028ms
rtt min/avg/max/mdev = 3.709/11.210/107.181/22.495 ms
```

#### Self-Ping 

```
PING 192.168.1.25 (192.168.1.25) 10000(10028) bytes of data.
10008 bytes from 192.168.1.25: icmp_seq=1 ttl=64 time=0.134 ms
10008 bytes from 192.168.1.25: icmp_seq=2 ttl=64 time=0.148 ms
10008 bytes from 192.168.1.25: icmp_seq=3 ttl=64 time=0.150 ms
10008 bytes from 192.168.1.25: icmp_seq=4 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.25: icmp_seq=5 ttl=64 time=0.128 ms
10008 bytes from 192.168.1.25: icmp_seq=6 ttl=64 time=0.126 ms
10008 bytes from 192.168.1.25: icmp_seq=7 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.25: icmp_seq=8 ttl=64 time=0.082 ms
10008 bytes from 192.168.1.25: icmp_seq=9 ttl=64 time=0.148 ms
10008 bytes from 192.168.1.25: icmp_seq=10 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.25: icmp_seq=11 ttl=64 time=0.114 ms
10008 bytes from 192.168.1.25: icmp_seq=12 ttl=64 time=0.083 ms
10008 bytes from 192.168.1.25: icmp_seq=13 ttl=64 time=0.082 ms
10008 bytes from 192.168.1.25: icmp_seq=14 ttl=64 time=0.195 ms
10008 bytes from 192.168.1.25: icmp_seq=15 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.25: icmp_seq=16 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.25: icmp_seq=17 ttl=64 time=0.086 ms
10008 bytes from 192.168.1.25: icmp_seq=18 ttl=64 time=0.100 ms
10008 bytes from 192.168.1.25: icmp_seq=19 ttl=64 time=0.120 ms
10008 bytes from 192.168.1.25: icmp_seq=20 ttl=64 time=0.117 ms

--- 192.168.1.25 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19449ms
rtt min/avg/max/mdev = 0.082/0.124/0.195/0.028 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.01   sec  9.88 MBytes  82.0 Mbits/sec
[  5]   1.01-2.01   sec  12.1 MBytes   102 Mbits/sec
[  5]   2.01-3.01   sec  13.2 MBytes   111 Mbits/sec
[  5]   3.01-4.01   sec  13.6 MBytes   114 Mbits/sec
[  5]   4.01-5.01   sec  14.5 MBytes   122 Mbits/sec
[  5]   5.01-6.01   sec  13.8 MBytes   116 Mbits/sec
[  5]   6.01-7.01   sec  13.1 MBytes   110 Mbits/sec
[  5]   7.01-8.01   sec  15.6 MBytes   131 Mbits/sec
[  5]   8.01-9.00   sec  15.2 MBytes   128 Mbits/sec
[  5]   9.00-10.01  sec  15.8 MBytes   132 Mbits/sec
[  5]  10.01-11.01  sec  13.0 MBytes   109 Mbits/sec
[  5]  11.01-12.00  sec  13.6 MBytes   115 Mbits/sec
[  5]  12.00-13.01  sec  15.6 MBytes   131 Mbits/sec
[  5]  13.01-14.00  sec  16.2 MBytes   137 Mbits/sec
[  5]  14.00-15.00  sec  16.2 MBytes   136 Mbits/sec
[  5]  15.00-16.00  sec  17.2 MBytes   145 Mbits/sec
[  5]  16.00-17.01  sec  17.2 MBytes   144 Mbits/sec
[  5]  17.01-18.00  sec  16.5 MBytes   139 Mbits/sec
[  5]  18.00-19.00  sec  16.8 MBytes   141 Mbits/sec
[  5]  19.00-20.00  sec  16.9 MBytes   141 Mbits/sec
[  5]  20.00-21.01  sec  12.2 MBytes   102 Mbits/sec
[  5]  21.01-22.01  sec  12.0 MBytes   101 Mbits/sec
[  5]  22.01-23.01  sec  9.75 MBytes  81.9 Mbits/sec
[  5]  23.01-24.01  sec  9.88 MBytes  82.3 Mbits/sec
[  5]  24.01-25.01  sec  11.5 MBytes  96.5 Mbits/sec
[  5]  25.01-26.01  sec  10.9 MBytes  91.3 Mbits/sec
[  5]  26.01-27.01  sec  10.1 MBytes  85.3 Mbits/sec
[  5]  27.01-28.01  sec  11.1 MBytes  92.9 Mbits/sec
[  5]  28.01-29.01  sec  15.9 MBytes   133 Mbits/sec
[  5]  29.01-30.00  sec  16.6 MBytes   140 Mbits/sec
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  146.055028] rtw_core: loading out-of-tree module taints kernel.
[  146.353093] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  146.476656] usbcore: registered new interface driver rtw_8814au
[  147.169407] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  462.066417] rtw_8814au 1-1:1.0: firmware failed to leave lps state
[  489.454363] rtw_8814au 1-1:1.0: failed to get tx report from firmware
[  708.709362] usbcore: deregistering interface driver rtw_8814au
[  715.067467] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  715.240726] usbcore: registered new interface driver rtw_8814au
[  940.208345] usbcore: deregistering interface driver rtw_8814au
[  946.303076] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  946.472606] usbcore: registered new interface driver rtw_8814au
[ 1522.098312] rtw_8814au 1-1:1.0: firmware failed to leave lps state
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
Using interface wlan0 with hwaddr and ssid "AP-NAME"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
```

#### Server & Client Test via iperf3 (PC-DUT)

<details>

<summary>iperf3</summary>

```
Wlan0 Not Ready.
Start AP @ WLAN0
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr  and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED 
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 53327
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 53328
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   830 KBytes  6.80 Mbits/sec    0   87.0 KBytes       
[  5]   1.00-2.00   sec   753 KBytes  6.17 Mbits/sec    2   87.0 KBytes       
[  5]   2.00-3.00   sec  1.50 MBytes  12.6 Mbits/sec    1   65.6 KBytes       
[  5]   3.00-4.00   sec  2.70 MBytes  22.6 Mbits/sec    0   65.6 KBytes       
[  5]   4.00-5.00   sec  2.60 MBytes  21.8 Mbits/sec   41   58.5 KBytes       
[  5]   5.00-6.00   sec  2.17 MBytes  18.2 Mbits/sec   32   39.9 KBytes       
[  5]   6.00-7.00   sec  2.73 MBytes  22.9 Mbits/sec    1   52.8 KBytes       
[  5]   7.00-8.00   sec  2.33 MBytes  19.5 Mbits/sec    1   65.6 KBytes       
[  5]   8.00-9.00   sec  5.12 MBytes  42.9 Mbits/sec    0   82.7 KBytes       
[  5]   9.00-10.00  sec  6.37 MBytes  53.4 Mbits/sec    0    128 KBytes       
[  5]  10.00-11.00  sec  6.19 MBytes  51.9 Mbits/sec    0    130 KBytes       
[  5]  11.00-12.00  sec  7.35 MBytes  61.7 Mbits/sec    0    130 KBytes       
[  5]  12.00-13.00  sec  7.05 MBytes  59.1 Mbits/sec    0    130 KBytes       
[  5]  13.00-14.00  sec  7.23 MBytes  60.6 Mbits/sec    0    130 KBytes       
[  5]  14.00-15.00  sec  7.60 MBytes  63.7 Mbits/sec    0    130 KBytes       
[  5]  15.00-16.00  sec  7.54 MBytes  63.2 Mbits/sec    0    200 KBytes       
[  5]  16.00-17.00  sec  5.82 MBytes  48.8 Mbits/sec    0    259 KBytes       
[  5]  17.00-18.00  sec  0.00 Bytes  0.00 bits/sec    0    259 KBytes       
[  5]  18.00-19.00  sec   565 KBytes  4.63 Mbits/sec    0    259 KBytes       
[  5]  19.00-20.00  sec  2.21 MBytes  18.5 Mbits/sec    0    259 KBytes       
[  5]  20.00-21.00  sec  2.82 MBytes  23.6 Mbits/sec    0    259 KBytes       
[  5]  21.00-22.00  sec  2.14 MBytes  18.0 Mbits/sec    0    259 KBytes       
[  5]  22.00-23.00  sec  1.90 MBytes  15.9 Mbits/sec   24    259 KBytes       
[  5]  23.00-24.00  sec  1.84 MBytes  15.4 Mbits/sec    5    259 KBytes       
[  5]  24.00-25.00  sec  2.39 MBytes  20.0 Mbits/sec   36    195 KBytes       
[  5]  25.00-26.00  sec   565 KBytes  4.62 Mbits/sec    0    195 KBytes       
[  5]  26.00-27.00  sec  4.96 MBytes  41.7 Mbits/sec    0    195 KBytes       
[  5]  27.00-28.00  sec  7.35 MBytes  61.7 Mbits/sec    0    195 KBytes       
[  5]  28.00-29.00  sec  6.74 MBytes  56.5 Mbits/sec    0    215 KBytes       
[  5]  29.00-30.00  sec  5.70 MBytes  47.8 Mbits/sec    0    235 KBytes       
[  5]  30.00-30.24  sec  1.72 MBytes  60.1 Mbits/sec    0    241 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.24  sec   117 MBytes  32.4 Mbits/sec  143             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  146.055028] rtw_core: loading out-of-tree module taints kernel.
[  146.353093] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  146.476656] usbcore: registered new interface driver rtw_8814au
[  147.169407] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  462.066417] rtw_8814au 1-1:1.0: firmware failed to leave lps state
[  489.454363] rtw_8814au 1-1:1.0: failed to get tx report from firmware
[  708.709362] usbcore: deregistering interface driver rtw_8814au
[  715.067467] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  715.240726] usbcore: registered new interface driver rtw_8814au
[  940.208345] usbcore: deregistering interface driver rtw_8814au
[  946.303076] rtw_8814au 1-1:1.0: Firmware version 33.6.0, H2C version 6
[  946.472606] usbcore: registered new interface driver rtw_8814au
[ 1522.098312] rtw_8814au 1-1:1.0: firmware failed to leave lps state
[ 1585.016465] rtw_8814au 1-1:1.0: error beacon valid
[ 1585.016671] rtw_8814au 1-1:1.0: failed to download drv rsvd page
[ 1585.016682] rtw_8814au 1-1:1.0: failed to download beacon
[ 1588.195225] rtw_8814au 1-1:1.0: error beacon valid
[ 1588.195408] rtw_8814au 1-1:1.0: failed to download drv rsvd page
[ 1588.195419] rtw_8814au 1-1:1.0: failed to download beacon
```

</details>

### End of Report
