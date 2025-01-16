# RTL8723DU USB Dongle Testing

### Test USB Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="../images/8723du/rtl8723du_arm_a35.png" height="400"/>|<img src="../images/8723du/rtl8723du_usb_pcba.png" height="400"/>|

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
    |__ Port 1: Dev 2, If 0, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 1, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 2, Class=Vendor Specific Class, Driver=, 480M

After driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=dwc2/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 1, Class=Wireless, Driver=btusb, 480M
    |__ Port 1: Dev 2, If 2, Class=Vendor Specific Class, Driver=rtw_8723du, 480M
```

<details>

<summary>USB Details</summary>

```

Bus 001 Device 002: ID 0bda:d723 Realtek Semiconductor Corp. 802.11n WLAN Adapter
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2 
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0xd723 
  bcdDevice            2.00
  iManufacturer           1 Realtek
  iProduct                2 802.11n WLAN Adapter
  iSerial                 3 00e04c000001
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength       0x00ec
    bNumInterfaces          3
    bConfigurationValue     1
    iConfiguration          0 
    bmAttributes         0xe0
      Self Powered
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
  bDeviceClass            0 
  bDeviceSubClass         0 
  bDeviceProtocol         0 
  bMaxPacketSize0        64
  bNumConfigurations      1
Device Status:     0x0001
  Self Powered
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8723du             16384  0
rtw_8723d              45056  1 rtw_8723du
rtw_8723x              20480  1 rtw_8723d
rtw_usb                24576  1 rtw_8723du
rtw_core              217088  3 rtw_8723d,rtw_usb,rtw_8723x
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy1
	max # scan SSIDs: 4
	max scan IEs length: 2257 bytes
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
			* 2484 MHz [14] (20.0 dBm) (no IR)
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

### Network Manager

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.24  netmask 255.255.252.0  broadcast 192.168.3.255
        inet6   prefixlen 64  scopeid 0x20<link>
        ether   txqueuelen 1000  (Ethernet)
        RX packets 12  bytes 1717 (1.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 25  bytes 4528 (4.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

### Network Speed Test via Ookla

```
Retrieving speedtest.net configuration...
Testing from Netvigator Home Broadband ...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Hosted by [4.85 km]: 16.182 ms
Testing download speed................................................................................
Download: 26.25 Mbit/s
Testing upload speed......................................................................................................
Upload: 15.43 Mbit/s
```

### Network Ping Tests

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=7.66 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=16.0 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=10.9 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=4.02 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=4.89 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=3.99 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=4.28 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=15.3 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=8.10 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=5.65 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=10.1 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=5.48 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=3.85 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=19.3 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=6.40 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=9.07 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=6.80 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=8.84 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=6.92 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=3.91 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19026ms
rtt min/avg/max/mdev = 3.852/8.078/19.342/4.287 ms
```

#### Self-Ping 

```
PING 192.168.1.24 (192.168.1.24) 10000(10028) bytes of data.
10008 bytes from 192.168.1.24: icmp_seq=1 ttl=64 time=0.131 ms
10008 bytes from 192.168.1.24: icmp_seq=2 ttl=64 time=0.117 ms
10008 bytes from 192.168.1.24: icmp_seq=3 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.24: icmp_seq=4 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.24: icmp_seq=5 ttl=64 time=0.128 ms
10008 bytes from 192.168.1.24: icmp_seq=6 ttl=64 time=0.145 ms
10008 bytes from 192.168.1.24: icmp_seq=7 ttl=64 time=0.132 ms
10008 bytes from 192.168.1.24: icmp_seq=8 ttl=64 time=0.136 ms
10008 bytes from 192.168.1.24: icmp_seq=9 ttl=64 time=0.111 ms
10008 bytes from 192.168.1.24: icmp_seq=10 ttl=64 time=0.144 ms
10008 bytes from 192.168.1.24: icmp_seq=11 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.24: icmp_seq=12 ttl=64 time=0.133 ms
10008 bytes from 192.168.1.24: icmp_seq=13 ttl=64 time=0.116 ms
10008 bytes from 192.168.1.24: icmp_seq=14 ttl=64 time=0.102 ms
10008 bytes from 192.168.1.24: icmp_seq=15 ttl=64 time=0.094 ms
10008 bytes from 192.168.1.24: icmp_seq=16 ttl=64 time=0.153 ms
10008 bytes from 192.168.1.24: icmp_seq=17 ttl=64 time=0.143 ms
10008 bytes from 192.168.1.24: icmp_seq=18 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.24: icmp_seq=19 ttl=64 time=0.093 ms
10008 bytes from 192.168.1.24: icmp_seq=20 ttl=64 time=0.096 ms

--- 192.168.1.24 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19459ms
rtt min/avg/max/mdev = 0.093/0.127/0.153/0.019 ms
```

### iwconfig

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.437 GHz  Access Point: 
          Bit Rate=135 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:58   Missed beacon:0

```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.26, port 59590
[  5] local 192.168.1.24 port 5201 connected to 192.168.1.26 port 59591
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  3.81 MBytes  32.0 Mbits/sec    1    133 KBytes       
[  5]   1.00-2.00   sec  3.06 MBytes  25.7 Mbits/sec    0    133 KBytes       
[  5]   2.00-3.00   sec  3.03 MBytes  25.4 Mbits/sec    0    133 KBytes       
[  5]   3.00-4.00   sec  2.24 MBytes  18.8 Mbits/sec    0    133 KBytes       
[  5]   4.00-5.00   sec  1.93 MBytes  16.2 Mbits/sec    0    133 KBytes       
[  5]   5.00-6.00   sec  1.65 MBytes  13.9 Mbits/sec    0    133 KBytes       
[  5]   6.00-7.00   sec  1.65 MBytes  13.9 Mbits/sec    0    133 KBytes       
[  5]   7.00-8.00   sec  1.65 MBytes  13.9 Mbits/sec    0    133 KBytes       
[  5]   8.00-9.00   sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]   9.00-10.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  10.00-11.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  11.00-12.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  12.00-13.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  13.00-14.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  14.00-15.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  15.00-16.00  sec   847 KBytes  6.94 Mbits/sec    0    133 KBytes       
[  5]  16.00-17.00  sec  1.65 MBytes  13.9 Mbits/sec    0    133 KBytes       
[  5]  17.00-18.00  sec  1.10 MBytes  9.25 Mbits/sec    0    133 KBytes       
[  5]  18.00-19.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  19.00-20.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  20.00-21.00  sec  1.10 MBytes  9.25 Mbits/sec    0    133 KBytes       
[  5]  21.00-22.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  22.00-23.00  sec   847 KBytes  6.94 Mbits/sec    0    133 KBytes       
[  5]  23.00-24.00  sec  1.65 MBytes  13.9 Mbits/sec    0    133 KBytes       
[  5]  24.00-25.00  sec  1.41 MBytes  11.8 Mbits/sec    0    133 KBytes       
[  5]  25.00-26.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  26.00-27.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  27.00-28.00  sec  1.13 MBytes  9.51 Mbits/sec    0    133 KBytes       
[  5]  28.00-29.00  sec  1.38 MBytes  11.6 Mbits/sec    0    133 KBytes       
[  5]  29.00-30.00  sec  1.65 MBytes  13.9 Mbits/sec    0    133 KBytes       
[  5]  30.00-30.06  sec   282 KBytes  36.8 Mbits/sec    0    133 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.06  sec  48.6 MBytes  13.6 Mbits/sec    1             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
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

Start AP @ WLAN1
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED 
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 59624
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 59625
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec  3.11 MBytes  26.1 Mbits/sec    0   92.7 KBytes       
[  5]   1.00-2.00   sec  2.85 MBytes  23.9 Mbits/sec    0   92.7 KBytes       
[  5]   2.00-3.00   sec  2.48 MBytes  20.8 Mbits/sec    0   92.7 KBytes       
[  5]   3.00-4.00   sec  2.57 MBytes  21.6 Mbits/sec    1   92.7 KBytes       
[  5]   4.00-5.00   sec  2.54 MBytes  21.3 Mbits/sec    0   92.7 KBytes       
[  5]   5.00-6.00   sec  2.51 MBytes  21.1 Mbits/sec    0   92.7 KBytes       
[  5]   6.00-7.00   sec  2.73 MBytes  22.9 Mbits/sec    0   92.7 KBytes       
[  5]   7.00-8.00   sec  1.84 MBytes  15.4 Mbits/sec    1   92.7 KBytes       
[  5]   8.00-9.00   sec  2.17 MBytes  18.2 Mbits/sec    1   92.7 KBytes       
[  5]   9.00-10.00  sec  2.27 MBytes  19.0 Mbits/sec    0   92.7 KBytes       
[  5]  10.00-11.00  sec  2.54 MBytes  21.3 Mbits/sec    0   92.7 KBytes       
[  5]  11.00-12.00  sec  2.24 MBytes  18.8 Mbits/sec    1   92.7 KBytes       
[  5]  12.00-13.00  sec  2.54 MBytes  21.3 Mbits/sec    1   92.7 KBytes       
[  5]  13.00-14.00  sec  2.70 MBytes  22.6 Mbits/sec    0   92.7 KBytes       
[  5]  14.00-15.00  sec  2.76 MBytes  23.1 Mbits/sec    0   92.7 KBytes       
[  5]  15.00-16.00  sec  2.36 MBytes  19.8 Mbits/sec    1   92.7 KBytes       
[  5]  16.00-17.00  sec  2.76 MBytes  23.1 Mbits/sec    0   92.7 KBytes       
[  5]  17.00-18.00  sec  2.66 MBytes  22.4 Mbits/sec    0   92.7 KBytes       
[  5]  18.00-19.00  sec  2.42 MBytes  20.3 Mbits/sec    0   92.7 KBytes       
[  5]  19.00-20.00  sec  2.73 MBytes  22.9 Mbits/sec    0   92.7 KBytes       
[  5]  20.00-21.00  sec  2.60 MBytes  21.8 Mbits/sec    0   92.7 KBytes       
[  5]  21.00-22.00  sec  2.24 MBytes  18.8 Mbits/sec    1   92.7 KBytes       
[  5]  22.00-23.00  sec  2.33 MBytes  19.5 Mbits/sec    2   92.7 KBytes       
[  5]  23.00-24.00  sec  2.57 MBytes  21.6 Mbits/sec    0   92.7 KBytes       
[  5]  24.00-25.00  sec  2.76 MBytes  23.1 Mbits/sec    0   92.7 KBytes       
[  5]  25.00-26.00  sec  2.60 MBytes  21.8 Mbits/sec    0   92.7 KBytes       
[  5]  26.00-27.00  sec  2.73 MBytes  22.9 Mbits/sec    1   92.7 KBytes       
[  5]  27.00-28.00  sec  2.60 MBytes  21.8 Mbits/sec    1   92.7 KBytes       
[  5]  28.00-29.00  sec  2.70 MBytes  22.6 Mbits/sec    0   92.7 KBytes       
[  5]  29.00-30.00  sec  2.51 MBytes  21.1 Mbits/sec    0   92.7 KBytes       
[  5]  30.00-30.06  sec   220 KBytes  27.9 Mbits/sec    0   92.7 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.06  sec  76.6 MBytes  21.4 Mbits/sec   11             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  817.019355] rtw_core: loading out-of-tree module taints kernel.
[  817.497116] rtw_8723du 1-1:1.2: Firmware version 48.0.0, H2C version 0
[  818.603272] usbcore: registered new interface driver rtw_8723du
[  875.948361] usbcore: deregistering interface driver rtw_8723du
[  897.040478] rtw_8723du 1-1:1.2: Firmware version 48.0.0, H2C version 0
[  898.137630] usbcore: registered new interface driver rtw_8723du
[ 1215.618767] rtw_8723du 1-1:1.2: error beacon valid
[ 1215.619218] rtw_8723du 1-1:1.2: failed to download drv rsvd page
[ 1215.619228] rtw_8723du 1-1:1.2: failed to download beacon
[ 1217.362580] rtw_8723du 1-1:1.2: error beacon valid
[ 1217.362929] rtw_8723du 1-1:1.2: failed to download drv rsvd page
[ 1221.051686] rtw_8723du 1-1:1.2: error beacon valid
[ 1221.052189] rtw_8723du 1-1:1.2: failed to download drv rsvd page
[ 1221.052202] rtw_8723du 1-1:1.2: failed to download beacon
[ 1225.042939] rtw_8723du 1-1:1.2: error beacon valid
[ 1225.043211] rtw_8723du 1-1:1.2: failed to download drv rsvd page
[ 1239.892046] rtw_8723du 1-1:1.2: error beacon valid
[ 1239.892303] rtw_8723du 1-1:1.2: failed to download drv rsvd page
[ 1240.200194] rtw_8723du 1-1:1.2: error beacon valid
[ 1240.200611] rtw_8723du 1-1:1.2: failed to download drv rsvd page
```

</details>

### End of Report
