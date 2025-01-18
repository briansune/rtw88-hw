# RTL8821AU USB Dongle Testing

### Test USB Gear

|Test Board|USB Dongle HW|
|-|-|
|<img src="../images/rtl8821au_arm_a9.JPG" height="400"/>|<img src="../images/rtl8821au_usb_pcba.JPG" height="400"/>|

```
5.4.0-xilinx

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.5 LTS"

Architecture:        armv7l
Byte Order:          Little Endian
CPU(s):              2
On-line CPU(s) list: 0,1
Thread(s) per core:  1
Core(s) per socket:  2
Socket(s):           1
Vendor ID:           ARM
Model:               0
Model name:          Cortex-A9
Stepping:            r3p0
BogoMIPS:            666.66
Flags:               half thumb fastmult vfp edsp neon vfpv3 tls vfpd32
```

### USB Tree

```
Before driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/2p, 480M
        |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=, 480M

After driver is inserted.
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ci_hdrc/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/2p, 480M
        |__ Port 1: Dev 3, If 0, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 1, Class=Wireless, Driver=btusb, 480M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=rtw_8821au, 480M
```

<details>

<summary>USB Details</summary>

```
Bus 001 Device 003: ID 0bda:0823 Realtek Semiconductor Corp. 
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.10
  bDeviceClass          239 Miscellaneous Device
  bDeviceSubClass         2 ?
  bDeviceProtocol         1 Interface Association
  bMaxPacketSize0        64
  idVendor           0x0bda Realtek Semiconductor Corp.
  idProduct          0x0823 
  bcdDevice            2.00
  iManufacturer           1 Realtek 
  iProduct                2 802.11ac WLAN Adapter 
  iSerial                 3 00e04c000001
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength          236
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
      iInterface              2 802.11ac WLAN Adapter 
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
Binary Object Store Descriptor:
  bLength                 5
  bDescriptorType        15
  wTotalLength           12
  bNumDeviceCaps          1
  USB 2.0 Extension Device Capability:
    bLength                 7
    bDescriptorType        16
    bDevCapabilityType      2
    bmAttributes   0x00000002
      Link Power Management (LPM) Supported
Device Status:     0x0001
  Self Powered
```

</details>

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8821au             16384  0
rtw_8821a              36864  1 rtw_8821au
rtw_88xxa              32768  1 rtw_8821a
rtw_usb                24576  1 rtw_8821au
rtw_core              172032  3 rtw_usb,rtw_88xxa,rtw_8821a
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
			* 2472 MHz [13] (20.0 dBm) (no IR)
			* 2484 MHz [14] (20.0 dBm) (no IR)
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
			* 5180 MHz [36] (20.0 dBm)
			* 5200 MHz [40] (20.0 dBm)
			* 5220 MHz [44] (20.0 dBm)
			* 5240 MHz [48] (20.0 dBm)
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
			* 5785 MHz [157] (20.0 dBm)
			* 5805 MHz [161] (20.0 dBm)
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

### Network Manager - Band 2.4

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.9  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 43  bytes 6828 (6.8 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 57  bytes 9631 (9.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.412 GHz  Access Point:    
          Bit Rate=108 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          Link Quality=60/70  Signal level=-50 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:1   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 25.96 Mbit/s
Testing upload speed......................................................................................................
Upload: 3.84 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=6.60 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=5.21 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=3.90 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=13.0 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=4.65 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=4.42 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=13.9 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=4.65 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=10.5 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=8.67 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=3.86 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.02 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=4.58 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=3.75 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=4.64 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=4.01 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=7.91 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=7.48 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=8.72 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=8.65 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19031ms
rtt min/avg/max/mdev = 3.752/6.663/13.907/3.032 ms
```

#### Self-Ping 

```
PING 192.168.1.9 (192.168.1.9) 10000(10028) bytes of data.
10008 bytes from 192.168.1.9: icmp_seq=1 ttl=64 time=0.139 ms
10008 bytes from 192.168.1.9: icmp_seq=2 ttl=64 time=0.135 ms
10008 bytes from 192.168.1.9: icmp_seq=3 ttl=64 time=0.114 ms
10008 bytes from 192.168.1.9: icmp_seq=4 ttl=64 time=0.111 ms
10008 bytes from 192.168.1.9: icmp_seq=5 ttl=64 time=0.110 ms
10008 bytes from 192.168.1.9: icmp_seq=6 ttl=64 time=0.122 ms
10008 bytes from 192.168.1.9: icmp_seq=7 ttl=64 time=0.115 ms
10008 bytes from 192.168.1.9: icmp_seq=8 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.9: icmp_seq=9 ttl=64 time=0.117 ms
10008 bytes from 192.168.1.9: icmp_seq=10 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.9: icmp_seq=11 ttl=64 time=0.107 ms
10008 bytes from 192.168.1.9: icmp_seq=12 ttl=64 time=0.119 ms
10008 bytes from 192.168.1.9: icmp_seq=13 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.9: icmp_seq=14 ttl=64 time=0.130 ms
10008 bytes from 192.168.1.9: icmp_seq=15 ttl=64 time=0.112 ms
10008 bytes from 192.168.1.9: icmp_seq=16 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.9: icmp_seq=17 ttl=64 time=0.115 ms
10008 bytes from 192.168.1.9: icmp_seq=18 ttl=64 time=0.118 ms
10008 bytes from 192.168.1.9: icmp_seq=19 ttl=64 time=0.108 ms
10008 bytes from 192.168.1.9: icmp_seq=20 ttl=64 time=0.131 ms

--- 192.168.1.9 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19777ms
rtt min/avg/max/mdev = 0.107/0.118/0.139/0.012 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 49962
[  5] local 192.168.1.9 port 5201 connected to 192.168.1.3 port 49963
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  3.62 MBytes  30.4 Mbits/sec    0    135 KBytes       
[  5]   1.00-2.00   sec  2.02 MBytes  17.0 Mbits/sec    0    135 KBytes       
[  5]   2.00-3.00   sec  2.02 MBytes  17.0 Mbits/sec    0    135 KBytes       
[  5]   3.00-4.00   sec  2.14 MBytes  18.0 Mbits/sec    0    135 KBytes       
[  5]   4.00-5.00   sec  1.96 MBytes  16.4 Mbits/sec    0    135 KBytes       
[  5]   5.00-6.00   sec  1.72 MBytes  14.4 Mbits/sec    0    135 KBytes       
[  5]   6.00-7.00   sec  2.02 MBytes  17.0 Mbits/sec    1   97.0 KBytes       
[  5]   7.00-8.00   sec  2.33 MBytes  19.5 Mbits/sec    0    120 KBytes       
[  5]   8.00-9.00   sec  2.88 MBytes  24.2 Mbits/sec    0    130 KBytes       
[  5]   9.00-10.00  sec  2.51 MBytes  21.1 Mbits/sec    0    130 KBytes       
[  5]  10.00-11.00  sec  2.51 MBytes  21.1 Mbits/sec    0    134 KBytes       
[  5]  11.00-12.00  sec  2.39 MBytes  20.0 Mbits/sec    0    134 KBytes       
[  5]  12.00-13.00  sec  2.45 MBytes  20.6 Mbits/sec    0    134 KBytes       
[  5]  13.00-14.00  sec  1.84 MBytes  15.4 Mbits/sec    0    134 KBytes       
[  5]  14.00-15.00  sec  2.21 MBytes  18.5 Mbits/sec    1    135 KBytes       
[  5]  15.00-16.00  sec  1.72 MBytes  14.4 Mbits/sec    1   1.43 KBytes       
[  5]  16.00-17.00  sec   188 KBytes  1.54 Mbits/sec   24   18.5 KBytes       
[  5]  17.00-18.00  sec  0.00 Bytes  0.00 bits/sec    1   1.43 KBytes       
[  5]  18.00-19.00  sec  0.00 Bytes  0.00 bits/sec    0   8.55 KBytes       
[  5]  19.00-20.00  sec  0.00 Bytes  0.00 bits/sec    0   8.55 KBytes       
[  5]  20.00-21.00  sec  0.00 Bytes  0.00 bits/sec    0   8.55 KBytes       
[  5]  21.00-22.00  sec   941 KBytes  7.72 Mbits/sec   13   38.5 KBytes       
[  5]  22.00-23.00  sec  1.29 MBytes  10.8 Mbits/sec    1   79.8 KBytes       
[  5]  23.00-24.00  sec   816 KBytes  6.68 Mbits/sec    0    121 KBytes       
[  5]  24.00-25.00  sec  1.16 MBytes  9.76 Mbits/sec    0    131 KBytes       
[  5]  25.00-26.00  sec  2.70 MBytes  22.6 Mbits/sec    1    131 KBytes       
[  5]  26.00-27.00  sec  3.06 MBytes  25.7 Mbits/sec    0    131 KBytes       
[  5]  27.00-28.00  sec  2.70 MBytes  22.6 Mbits/sec    0    131 KBytes       
[  5]  28.00-29.00  sec  3.12 MBytes  26.2 Mbits/sec    0    190 KBytes       
[  5]  29.00-30.00  sec  1.78 MBytes  14.9 Mbits/sec    0    230 KBytes       
[  5]  30.00-30.02  sec  0.00 Bytes  0.00 bits/sec    0    230 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.02  sec  54.0 MBytes  15.1 Mbits/sec   43             sender
[  5]   0.00-30.02  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   64.787623] rtw_core: loading out-of-tree module taints kernel.
[   65.351956] rtw_8821au 1-1.1:1.2: Firmware version 42.4.0, H2C version 0
[   66.563357] usbcore: registered new interface driver rtw_8821au
[   90.990511] usbcore: deregistering interface driver rtw_8821au
[   97.485196] rtw_8821au 1-1.1:1.2: Firmware version 42.4.0, H2C version 0
[   98.724061] usbcore: registered new interface driver rtw_8821au
```

</details>

### Network Manager - Band 5G

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.9  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 40806  bytes 35935913 (35.9 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 55112  bytes 66469138 (66.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 5G

```
wlan0     IEEE 802.11  ESSID:"xellossfong"  
          Mode:Managed  Frequency:5.805 GHz  Access Point:    
          Bit Rate=175.5 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          Link Quality=44/70  Signal level=-66 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 5G

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 54.24 Mbit/s
Testing upload speed......................................................................................................
Upload: 3.84 Mbit/s
```

### Network Ping Tests - Band 5G

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=4.52 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=4.16 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=8.28 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=7.93 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=7.28 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=3.95 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=4.14 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=4.03 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=7.56 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=7.80 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=4.51 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=4.96 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=4.14 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=3.71 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=3.84 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=9.73 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=3.94 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=3.96 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=4.46 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 3.716/5.347/9.732/1.873 ms
```

#### Self-Ping 

```
PING 192.168.1.9 (192.168.1.9) 10000(10028) bytes of data.
10008 bytes from 192.168.1.9: icmp_seq=1 ttl=64 time=0.140 ms
10008 bytes from 192.168.1.9: icmp_seq=2 ttl=64 time=0.115 ms
10008 bytes from 192.168.1.9: icmp_seq=3 ttl=64 time=0.110 ms
10008 bytes from 192.168.1.9: icmp_seq=4 ttl=64 time=0.124 ms
10008 bytes from 192.168.1.9: icmp_seq=5 ttl=64 time=0.116 ms
10008 bytes from 192.168.1.9: icmp_seq=6 ttl=64 time=0.116 ms
10008 bytes from 192.168.1.9: icmp_seq=7 ttl=64 time=0.114 ms
10008 bytes from 192.168.1.9: icmp_seq=8 ttl=64 time=0.106 ms
10008 bytes from 192.168.1.9: icmp_seq=9 ttl=64 time=0.109 ms
10008 bytes from 192.168.1.9: icmp_seq=10 ttl=64 time=0.124 ms
10008 bytes from 192.168.1.9: icmp_seq=11 ttl=64 time=0.115 ms
10008 bytes from 192.168.1.9: icmp_seq=12 ttl=64 time=0.113 ms
10008 bytes from 192.168.1.9: icmp_seq=13 ttl=64 time=0.115 ms
10008 bytes from 192.168.1.9: icmp_seq=14 ttl=64 time=0.111 ms
10008 bytes from 192.168.1.9: icmp_seq=15 ttl=64 time=0.159 ms
10008 bytes from 192.168.1.9: icmp_seq=16 ttl=64 time=0.124 ms
10008 bytes from 192.168.1.9: icmp_seq=17 ttl=64 time=0.120 ms
10008 bytes from 192.168.1.9: icmp_seq=18 ttl=64 time=0.128 ms
10008 bytes from 192.168.1.9: icmp_seq=19 ttl=64 time=0.118 ms
10008 bytes from 192.168.1.9: icmp_seq=20 ttl=64 time=0.122 ms

--- 192.168.1.9 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19745ms
rtt min/avg/max/mdev = 0.106/0.119/0.159/0.019 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 50007
[  5] local 192.168.1.9 port 5201 connected to 192.168.1.3 port 50008
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  2.69 MBytes  22.6 Mbits/sec    0    191 KBytes       
[  5]   1.00-2.00   sec  2.21 MBytes  18.5 Mbits/sec    0    254 KBytes       
[  5]   2.00-3.00   sec  2.76 MBytes  23.1 Mbits/sec   16    106 KBytes       
[  5]   3.00-4.00   sec  4.23 MBytes  35.5 Mbits/sec   13    220 KBytes       
[  5]   4.00-5.00   sec  4.59 MBytes  38.5 Mbits/sec    0    247 KBytes       
[  5]   5.00-6.00   sec  5.70 MBytes  47.8 Mbits/sec    0    261 KBytes       
[  5]   6.00-7.00   sec  4.53 MBytes  38.0 Mbits/sec    0    265 KBytes       
[  5]   7.00-8.00   sec  4.66 MBytes  39.1 Mbits/sec    0    265 KBytes       
[  5]   8.00-9.00   sec  5.45 MBytes  45.7 Mbits/sec    0    265 KBytes       
[  5]   9.00-10.00  sec  2.82 MBytes  23.6 Mbits/sec    0    268 KBytes       
[  5]  10.00-11.00  sec  4.66 MBytes  39.1 Mbits/sec    0    279 KBytes       
[  5]  11.00-12.00  sec  5.02 MBytes  42.1 Mbits/sec    0    294 KBytes       
[  5]  12.00-13.00  sec  5.70 MBytes  47.8 Mbits/sec    0    324 KBytes       
[  5]  13.00-14.00  sec  4.59 MBytes  38.5 Mbits/sec    0    362 KBytes       
[  5]  14.00-15.00  sec  4.90 MBytes  41.1 Mbits/sec    0    432 KBytes       
[  5]  15.00-16.00  sec  4.90 MBytes  41.1 Mbits/sec    0    519 KBytes       
[  5]  16.00-17.00  sec  3.37 MBytes  28.3 Mbits/sec    0    519 KBytes       
[  5]  17.00-18.00  sec  5.51 MBytes  46.3 Mbits/sec    1    519 KBytes       
[  5]  18.00-19.00  sec  4.23 MBytes  35.5 Mbits/sec    0    519 KBytes       
[  5]  19.00-20.00  sec  4.84 MBytes  40.6 Mbits/sec    0    519 KBytes       
[  5]  20.00-21.00  sec  4.35 MBytes  36.5 Mbits/sec    0    519 KBytes       
[  5]  21.00-22.00  sec  4.23 MBytes  35.5 Mbits/sec    0    519 KBytes       
[  5]  22.00-23.00  sec  4.23 MBytes  35.5 Mbits/sec    0    519 KBytes       
[  5]  23.00-24.00  sec  6.13 MBytes  51.4 Mbits/sec    0    519 KBytes       
[  5]  24.00-25.00  sec  4.96 MBytes  41.6 Mbits/sec    0    519 KBytes       
[  5]  25.00-26.00  sec  5.45 MBytes  45.7 Mbits/sec    0    519 KBytes       
[  5]  26.00-27.00  sec  6.37 MBytes  53.4 Mbits/sec    0    519 KBytes       
[  5]  27.00-28.00  sec  5.15 MBytes  43.2 Mbits/sec    0    519 KBytes       
[  5]  28.00-29.00  sec  4.35 MBytes  36.5 Mbits/sec    0    519 KBytes       
[  5]  29.00-30.00  sec  4.59 MBytes  38.5 Mbits/sec    0    519 KBytes       
[  5]  30.00-30.04  sec   753 KBytes   160 Mbits/sec    0    519 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.04  sec   138 MBytes  38.5 Mbits/sec   30             sender
[  5]   0.00-30.04  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   64.787623] rtw_core: loading out-of-tree module taints kernel.
[   65.351956] rtw_8821au 1-1.1:1.2: Firmware version 42.4.0, H2C version 0
[   66.563357] usbcore: registered new interface driver rtw_8821au
[   90.990511] usbcore: deregistering interface driver rtw_8821au
[   97.485196] rtw_8821au 1-1.1:1.2: Firmware version 42.4.0, H2C version 0
[   98.724061] usbcore: registered new interface driver rtw_8821au
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
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.175.86, port 50037
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 50038
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec   871 KBytes  7.13 Mbits/sec    4   68.4 KBytes       
[  5]   1.00-2.00   sec  2.05 MBytes  17.2 Mbits/sec    0   68.4 KBytes       
[  5]   2.00-3.00   sec  2.48 MBytes  20.8 Mbits/sec   23   68.4 KBytes       
[  5]   3.00-4.00   sec  2.48 MBytes  20.8 Mbits/sec    0   68.4 KBytes       
[  5]   4.00-5.00   sec  2.48 MBytes  20.8 Mbits/sec    0   68.4 KBytes       
[  5]   5.00-6.00   sec  3.03 MBytes  25.4 Mbits/sec    0   68.4 KBytes       
[  5]   6.00-7.00   sec  3.16 MBytes  26.5 Mbits/sec    0   68.4 KBytes       
[  5]   7.00-8.00   sec  2.54 MBytes  21.3 Mbits/sec    1   65.6 KBytes       
[  5]   8.00-9.00   sec  2.85 MBytes  23.9 Mbits/sec    0   65.6 KBytes       
[  5]   9.00-10.00  sec  3.68 MBytes  30.8 Mbits/sec    0   65.6 KBytes       
[  5]  10.00-11.00  sec  3.97 MBytes  33.3 Mbits/sec    0   65.6 KBytes       
[  5]  11.00-12.00  sec  3.77 MBytes  31.6 Mbits/sec    0   65.6 KBytes       
[  5]  12.00-13.00  sec  4.04 MBytes  33.9 Mbits/sec    0   71.3 KBytes       
[  5]  13.00-14.00  sec  3.68 MBytes  30.8 Mbits/sec    0   71.3 KBytes       
[  5]  14.00-15.00  sec  3.25 MBytes  27.2 Mbits/sec    0   71.3 KBytes       
[  5]  15.00-16.00  sec  2.30 MBytes  19.3 Mbits/sec    1   71.3 KBytes       
[  5]  16.00-17.00  sec  3.80 MBytes  31.9 Mbits/sec    0   71.3 KBytes       
[  5]  17.00-18.00  sec  3.65 MBytes  30.6 Mbits/sec    0   71.3 KBytes       
[  5]  18.00-19.00  sec  3.40 MBytes  28.5 Mbits/sec    0   71.3 KBytes       
[  5]  19.00-20.00  sec  3.37 MBytes  28.3 Mbits/sec    0   71.3 KBytes       
[  5]  20.00-21.00  sec  1.65 MBytes  13.9 Mbits/sec    1   67.0 KBytes       
[  5]  21.00-22.00  sec  3.12 MBytes  26.2 Mbits/sec    1   54.2 KBytes       
[  5]  22.00-23.00  sec  3.50 MBytes  29.3 Mbits/sec    0   65.6 KBytes       
[  5]  23.00-24.00  sec  1.59 MBytes  13.4 Mbits/sec   10   58.5 KBytes       
[  5]  24.00-25.00  sec  1.68 MBytes  14.1 Mbits/sec   11   62.7 KBytes       
[  5]  25.00-26.00  sec  2.91 MBytes  24.4 Mbits/sec    0   65.6 KBytes       
[  5]  26.00-27.00  sec  3.22 MBytes  27.0 Mbits/sec    0   65.6 KBytes       
[  5]  27.00-28.00  sec  3.03 MBytes  25.4 Mbits/sec    0   65.6 KBytes       
[  5]  28.00-29.00  sec  2.89 MBytes  24.2 Mbits/sec    0   65.6 KBytes       
[  5]  29.00-30.00  sec  3.09 MBytes  26.0 Mbits/sec    0   65.6 KBytes       
[  5]  30.00-30.02  sec  0.00 Bytes  0.00 bits/sec    0   65.6 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.02  sec  87.5 MBytes  24.5 Mbits/sec   52             sender
[  5]   0.00-30.02  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   64.787623] rtw_core: loading out-of-tree module taints kernel.
[   65.351956] rtw_8821au 1-1.1:1.2: Firmware version 42.4.0, H2C version 0
[   66.563357] usbcore: registered new interface driver rtw_8821au
[   90.990511] usbcore: deregistering interface driver rtw_8821au
[   97.485196] rtw_8821au 1-1.1:1.2: Firmware version 42.4.0, H2C version 0
[   98.724061] usbcore: registered new interface driver rtw_8821au
[  547.047471] rtw_8821au 1-1.1:1.2: error beacon valid
[  547.051421] rtw_8821au 1-1.1:1.2: failed to download drv rsvd page
```

</details>

### End of Report
