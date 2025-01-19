# RTL8723DS SDIO PCBA Testing

### Test SDIO Gear

|Test Board|SDIO Dongle HW|
|-|-|
|<img src="../images/8723ds/rtl8723ds_arm_a35_cus.JPG" height="400"/>|<img src="../images/8723ds/rtl8723ds_pcba_cus.JPG" height="400"/>|

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

### SDIO Tree

```
MMC_TYPE=SDIO
SDIO_ID=024C:D723
SDIO_REVISION=0.0
clock:		50000000 Hz
actual clock:	50000000 Hz
vdd:		21 (3.3 ~ 3.4 V)
bus mode:	2 (push-pull)
chip select:	0 (don't care)
power mode:	2 (on)
bus width:	2 (4 bits)
timing spec:	2 (sd high-speed)
signal voltage:	0 (3.30 V)
driver type:	0 (driver type B)
```

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8723ds             16384  0
rtw_8723d              45056  1 rtw_8723ds
rtw_8723x              20480  1 rtw_8723d
rtw_sdio               20480  1 rtw_8723ds
rtw_core              217088  3 rtw_8723d,rtw_sdio,rtw_8723x
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
			* 2484 MHz [14] (disabled)
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
        inet 192.168.1.18  netmask 255.255.252.0  broadcast 192.168.3.255
        RX packets 6  bytes 1138 (1.1 KB)
        RX errors 0  dropped 1  overruns 0  frame 0
        TX packets 21  bytes 3935 (3.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.412 GHz  Access Point: 
          Bit Rate=6 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=42/70  Signal level=-68 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 9.96 Mbit/s
Testing upload speed......................................................................................................
Upload: 4.85 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=192 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=198 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=5.32 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=118 time=11.2 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=118 time=6.04 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=118 time=18.7 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=118 time=6.79 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=118 time=6.28 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=118 time=4.81 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=118 time=10.1 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=118 time=4.91 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=118 time=6.29 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=118 time=5.06 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=118 time=5.64 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=118 time=18.0 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=118 time=6.30 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=118 time=10.4 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=118 time=4.35 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=118 time=11.5 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=118 time=7.64 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19028ms
rtt min/avg/max/mdev = 4.345/27.016/198.469/56.299 ms
```

#### Self-Ping 

```
PING 192.168.1.18 (192.168.1.18) 10000(10028) bytes of data.
10008 bytes from 192.168.1.18: icmp_seq=1 ttl=64 time=0.123 ms
10008 bytes from 192.168.1.18: icmp_seq=2 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.18: icmp_seq=3 ttl=64 time=0.122 ms
10008 bytes from 192.168.1.18: icmp_seq=4 ttl=64 time=0.144 ms
10008 bytes from 192.168.1.18: icmp_seq=5 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.18: icmp_seq=6 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.18: icmp_seq=7 ttl=64 time=0.137 ms
10008 bytes from 192.168.1.18: icmp_seq=8 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.18: icmp_seq=9 ttl=64 time=0.107 ms
10008 bytes from 192.168.1.18: icmp_seq=10 ttl=64 time=0.100 ms
10008 bytes from 192.168.1.18: icmp_seq=11 ttl=64 time=0.146 ms
10008 bytes from 192.168.1.18: icmp_seq=12 ttl=64 time=0.142 ms
10008 bytes from 192.168.1.18: icmp_seq=13 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.18: icmp_seq=14 ttl=64 time=0.099 ms
10008 bytes from 192.168.1.18: icmp_seq=15 ttl=64 time=0.095 ms
10008 bytes from 192.168.1.18: icmp_seq=16 ttl=64 time=0.105 ms
10008 bytes from 192.168.1.18: icmp_seq=17 ttl=64 time=0.138 ms
10008 bytes from 192.168.1.18: icmp_seq=18 ttl=64 time=0.147 ms
10008 bytes from 192.168.1.18: icmp_seq=19 ttl=64 time=0.141 ms
10008 bytes from 192.168.1.18: icmp_seq=20 ttl=64 time=0.091 ms

--- 192.168.1.18 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19450ms
rtt min/avg/max/mdev = 0.091/0.124/0.147/0.020 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.3, port 53705
[  5] local 192.168.1.18 port 5201 connected to 192.168.1.3 port 53706
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  5]   0.00-1.00   sec   767 KBytes  6.28 Mbits/sec    0    123 KBytes       
[  5]   1.00-2.00   sec  0.00 Bytes  0.00 bits/sec    0    123 KBytes       
[  5]   2.00-3.00   sec   251 KBytes  2.06 Mbits/sec    0    123 KBytes       
[  5]   3.00-4.00   sec  0.00 Bytes  0.00 bits/sec    1    123 KBytes       
[  5]   4.00-5.00   sec  0.00 Bytes  0.00 bits/sec    1    123 KBytes       
[  5]   5.00-6.00   sec  0.00 Bytes  0.00 bits/sec    0    123 KBytes       
[  5]   6.00-7.00   sec  0.00 Bytes  0.00 bits/sec    0    123 KBytes       
[  5]   7.00-8.00   sec   502 KBytes  4.11 Mbits/sec    0    123 KBytes       
[  5]   8.00-9.00   sec  0.00 Bytes  0.00 bits/sec    1    123 KBytes       
[  5]   9.00-10.00  sec  0.00 Bytes  0.00 bits/sec    0    124 KBytes       
[  5]  10.00-11.00  sec  0.00 Bytes  0.00 bits/sec    0    124 KBytes       
[  5]  11.00-12.00  sec  0.00 Bytes  0.00 bits/sec    1    124 KBytes       
[  5]  12.00-13.00  sec  0.00 Bytes  0.00 bits/sec    0    125 KBytes       
[  5]  13.00-14.00  sec  0.00 Bytes  0.00 bits/sec    0    125 KBytes       
[  5]  14.00-15.00  sec  0.00 Bytes  0.00 bits/sec    0    125 KBytes       
[  5]  15.00-16.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  16.00-17.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  17.00-18.00  sec   251 KBytes  2.06 Mbits/sec    1    125 KBytes       
[  5]  18.00-19.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  19.00-20.00  sec  0.00 Bytes  0.00 bits/sec    1    125 KBytes       
[  5]  20.00-21.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  21.00-22.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  22.00-23.00  sec   282 KBytes  2.31 Mbits/sec    0    125 KBytes       
[  5]  23.00-24.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  24.00-25.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  25.00-26.00  sec   251 KBytes  2.06 Mbits/sec    1    125 KBytes       
[  5]  26.00-27.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  27.00-28.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  28.00-29.00  sec   251 KBytes  2.06 Mbits/sec    1    125 KBytes       
[  5]  29.00-30.00  sec   251 KBytes  2.06 Mbits/sec    0    125 KBytes       
[  5]  30.00-30.12  sec  0.00 Bytes  0.00 bits/sec    0    125 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-30.12  sec  4.95 MBytes  1.38 Mbits/sec    8             sender
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  117.284109] rtw_core: loading out-of-tree module taints kernel.
[  118.194724] rtw_8723ds mmc1:0001:1: Firmware version 48.0.0, H2C version 0
[  213.692724] rtw_8723ds mmc1:0001:1: Firmware version 48.0.0, H2C version 0
[  361.033343] rtw_8723ds mmc1:0001:1: failed to get tx report from firmware
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

Host unable to connect to AP!

<details>

<summary>iperf3</summary>

```
Wlan0 Not Ready.
Start AP @ WLAN0
Configuration file: /etc/hostapd/hostapd.conf
Using interface wlan0 with hwaddr a8:96:09:9e:05:fd and ssid "AP-TEST"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED 
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
[  117.284109] rtw_core: loading out-of-tree module taints kernel.
[  118.194724] rtw_8723ds mmc1:0001:1: Firmware version 48.0.0, H2C version 0
[  213.692724] rtw_8723ds mmc1:0001:1: Firmware version 48.0.0, H2C version 0
[  361.033343] rtw_8723ds mmc1:0001:1: failed to get tx report from firmware
```

</details>

### End of Report
