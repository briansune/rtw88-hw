# RTL8723DE PCIe Card Testing

### Test PCIe Gear

|Test Board|PCIe Card HW|
|-|-|
|<img src="../images/8723de/rtl8723de_arm53_2.JPG" height="400"/>|<img src="../images/8723de/rtl8723de_m2card_n2.JPG" height="400"/>|

```
5.4.0

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.6 LTS"

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

### PCIe Tree

```
01:00.0 Network controller: Realtek Semiconductor Co., Ltd. Device d723
	Subsystem: Hewlett-Packard Company Device 8319
	Control: I/O- Mem- BusMaster- SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx-
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Interrupt: pin A routed to IRQ 255
	Region 0: I/O ports at <unassigned> [disabled]
	Region 2: Memory at e0000000 (64-bit, non-prefetchable) [disabled] [size=64K]
	Capabilities: [40] Power Management version 3
		Flags: PMEClk- DSI- D1+ D2+ AuxCurrent=375mA PME(D0+,D1+,D2+,D3hot+,D3cold+)
		Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
	Capabilities: [50] MSI: Enable- Count=1/1 Maskable- 64bit+
		Address: 0000000000000000  Data: 0000
	Capabilities: [70] Express (v2) Endpoint, MSI 00
		DevCap:	MaxPayload 128 bytes, PhantFunc 0, Latency L0s <4us, L1 <64us
			ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset- SlotPowerLimit 0.000W
		DevCtl:	Report errors: Correctable- Non-Fatal- Fatal- Unsupported-
			RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr- UncorrErr- FatalErr- UnsuppReq- AuxPwr+ TransPend-
		LnkCap:	Port #0, Speed 2.5GT/s, Width x1, ASPM L0s L1, Exit Latency L0s <512ns, L1 <64us
			ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp-
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 2.5GT/s, Width x1, TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, LTR+, OBFF Via message/WAKE#
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis-, LTR-, OBFF Disabled
		LnkCtl2: Target Link Speed: 2.5GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -3.5dB, EqualizationComplete-, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [100 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr+
		AERCap:	First Error Pointer: 00, GenCap+ CGenEn- ChkCap+ ChkEn-
	Capabilities: [148 v1] Virtual Channel
		Caps:	LPEVC=0 RefClk=100ns PATEntryBits=1
		Arb:	Fixed- WRR32- WRR64- WRR128-
		Ctrl:	ArbSelect=Fixed
		Status:	InProgress-
		VC0:	Caps:	PATOffset=00 MaxTimeSlots=1 RejSnoopTrans-
			Arb:	Fixed- WRR32- WRR64- WRR128- TWRR128- WRR256-
			Ctrl:	Enable+ ID=0 ArbSelect=Fixed TC/VC=ff
			Status:	NegoPending- InProgress-
	Capabilities: [168 v1] Device Serial Number 00-e0-4c-00-00-00-00-00
	Capabilities: [178 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [180 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1- L1_PM_Substates-
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-

		L1SubCtl2:
	Kernel modules: rtw_8723de

```

### Driver Load

The driver is loaded via "insmod"

```
Module                  Size  Used by
rtw_8723de             16384  0
rtw_8723d              45056  1 rtw_8723de
rtw_8723x              20480  1 rtw_8723d
rtw_pci                32768  1 rtw_8723de
rtw_core              208896  3 rtw_8723d,rtw_8723x,rtw_pci

01:00.0 Network controller: Realtek Semiconductor Co., Ltd. Device d723
	Subsystem: Hewlett-Packard Company Device 8319
	Control: I/O- Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
	Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
	Latency: 0
	Interrupt: pin A routed to IRQ 50
	Region 0: I/O ports at <unassigned> [disabled]
	Region 2: Memory at e0000000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: [40] Power Management version 3
		Flags: PMEClk- DSI- D1+ D2+ AuxCurrent=375mA PME(D0+,D1+,D2+,D3hot+,D3cold+)
		Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
	Capabilities: [50] MSI: Enable+ Count=1/1 Maskable- 64bit+
		Address: 00000000fd480000  Data: 0000
	Capabilities: [70] Express (v2) Endpoint, MSI 00
		DevCap:	MaxPayload 128 bytes, PhantFunc 0, Latency L0s <4us, L1 <64us
			ExtTag- AttnBtn- AttnInd- PwrInd- RBE+ FLReset- SlotPowerLimit 0.000W
		DevCtl:	Report errors: Correctable- Non-Fatal- Fatal- Unsupported-
			RlxdOrd+ ExtTag- PhantFunc- AuxPwr- NoSnoop-
			MaxPayload 128 bytes, MaxReadReq 512 bytes
		DevSta:	CorrErr- UncorrErr- FatalErr- UnsuppReq- AuxPwr+ TransPend-
		LnkCap:	Port #0, Speed 2.5GT/s, Width x1, ASPM L0s L1, Exit Latency L0s <512ns, L1 <64us
			ClockPM+ Surprise- LLActRep- BwNot- ASPMOptComp-
		LnkCtl:	ASPM Disabled; RCB 64 bytes Disabled- CommClk-
			ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
		LnkSta:	Speed 2.5GT/s, Width x1, TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
		DevCap2: Completion Timeout: Not Supported, TimeoutDis+, LTR+, OBFF Via message/WAKE#
		DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis-, LTR-, OBFF Disabled
		LnkCtl2: Target Link Speed: 2.5GT/s, EnterCompliance- SpeedDis-
			 Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
			 Compliance De-emphasis: -6dB
		LnkSta2: Current De-emphasis Level: -3.5dB, EqualizationComplete-, EqualizationPhase1-
			 EqualizationPhase2-, EqualizationPhase3-, LinkEqualizationRequest-
	Capabilities: [100 v2] Advanced Error Reporting
		UESta:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UEMsk:	DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
		UESvrt:	DLP+ SDES+ TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
		CESta:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr-
		CEMsk:	RxErr- BadTLP- BadDLLP- Rollover- Timeout- NonFatalErr+
		AERCap:	First Error Pointer: 00, GenCap+ CGenEn- ChkCap+ ChkEn-
	Capabilities: [148 v1] Virtual Channel
		Caps:	LPEVC=0 RefClk=100ns PATEntryBits=1
		Arb:	Fixed- WRR32- WRR64- WRR128-
		Ctrl:	ArbSelect=Fixed
		Status:	InProgress-
		VC0:	Caps:	PATOffset=00 MaxTimeSlots=1 RejSnoopTrans-
			Arb:	Fixed- WRR32- WRR64- WRR128- TWRR128- WRR256-
			Ctrl:	Enable+ ID=0 ArbSelect=Fixed TC/VC=ff
			Status:	NegoPending- InProgress-
	Capabilities: [168 v1] Device Serial Number 00-e0-4c-00-00-00-00-00
	Capabilities: [178 v1] Latency Tolerance Reporting
		Max snoop latency: 0ns
		Max no snoop latency: 0ns
	Capabilities: [180 v1] L1 PM Substates
		L1SubCap: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1- L1_PM_Substates-
		L1SubCtl1: PCI-PM_L1.2- PCI-PM_L1.1- ASPM_L1.2- ASPM_L1.1-

		L1SubCtl2:
	Kernel driver in use: rtw_8723de
	Kernel modules: rtw_8723de

[   40.436787] rtw_core: loading out-of-tree module taints kernel.
[   40.664687] rtw_8723de 0000:01:00.0: enabling device (0000 -> 0002)
[   40.681400] rtw_8723de 0000:01:00.0: Firmware version 48.0.0, H2C version 0
```

### iw list

<details>

<summary>iw list</summary>

```
Wiphy phy0
	max # scan SSIDs: 4
	max scan IEs length: 2257 bytes
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
			* 2467 MHz [12] (20.0 dBm) (no IR)
			* 2472 MHz [13] (20.0 dBm) (no IR)
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

### Network Manager - Band 2.4

```
wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.151  netmask 255.255.255.0  broadcast 192.168.1.255
        RX packets 9  bytes 1510 (1.5 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 16  bytes 2560 (2.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### iwconfig 2.4

```
wlan0     IEEE 802.11  ESSID:""  
          Mode:Managed  Frequency:2.427 GHz  Access Point: 
          Bit Rate=58.5 Mb/s   Tx-Power=30 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:on
          Link Quality=58/70  Signal level=-52 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:1   Missed beacon:0

```

### Network Speed Test via Ookla - Band 2.4

```
Retrieving speedtest.net configuration...
Retrieving speedtest.net server list...
Selecting best server based on ping...
Testing download speed................................................................................
Download: 32.02 Mbit/s
Testing upload speed......................................................................................................
Upload: 3.06 Mbit/s
```

### Network Ping Tests - Band 2.4

#### DNS-Ping

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=59 time=7.19 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=59 time=14.3 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=59 time=5.63 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=59 time=5.65 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=59 time=9.03 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=59 time=7.86 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=59 time=5.57 ms
64 bytes from 8.8.8.8: icmp_seq=8 ttl=59 time=5.06 ms
64 bytes from 8.8.8.8: icmp_seq=9 ttl=59 time=5.72 ms
64 bytes from 8.8.8.8: icmp_seq=10 ttl=59 time=5.39 ms
64 bytes from 8.8.8.8: icmp_seq=11 ttl=59 time=8.22 ms
64 bytes from 8.8.8.8: icmp_seq=12 ttl=59 time=7.48 ms
64 bytes from 8.8.8.8: icmp_seq=13 ttl=59 time=9.53 ms
64 bytes from 8.8.8.8: icmp_seq=14 ttl=59 time=8.10 ms
64 bytes from 8.8.8.8: icmp_seq=15 ttl=59 time=4.74 ms
64 bytes from 8.8.8.8: icmp_seq=16 ttl=59 time=9.75 ms
64 bytes from 8.8.8.8: icmp_seq=17 ttl=59 time=5.99 ms
64 bytes from 8.8.8.8: icmp_seq=18 ttl=59 time=9.20 ms
64 bytes from 8.8.8.8: icmp_seq=19 ttl=59 time=4.37 ms
64 bytes from 8.8.8.8: icmp_seq=20 ttl=59 time=4.32 ms

--- 8.8.8.8 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19027ms
rtt min/avg/max/mdev = 4.320/7.160/14.336/2.387 ms
```

#### Self-Ping 

```
PING 192.168.1.151 (192.168.1.151) 10000(10028) bytes of data.
10008 bytes from 192.168.1.151: icmp_seq=1 ttl=64 time=0.103 ms
10008 bytes from 192.168.1.151: icmp_seq=2 ttl=64 time=0.065 ms
10008 bytes from 192.168.1.151: icmp_seq=3 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=4 ttl=64 time=0.078 ms
10008 bytes from 192.168.1.151: icmp_seq=5 ttl=64 time=0.068 ms
10008 bytes from 192.168.1.151: icmp_seq=6 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=7 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=8 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.151: icmp_seq=9 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=10 ttl=64 time=0.079 ms
10008 bytes from 192.168.1.151: icmp_seq=11 ttl=64 time=0.066 ms
10008 bytes from 192.168.1.151: icmp_seq=12 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=13 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=14 ttl=64 time=0.060 ms
10008 bytes from 192.168.1.151: icmp_seq=15 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.151: icmp_seq=16 ttl=64 time=0.083 ms
10008 bytes from 192.168.1.151: icmp_seq=17 ttl=64 time=0.066 ms
10008 bytes from 192.168.1.151: icmp_seq=18 ttl=64 time=0.061 ms
10008 bytes from 192.168.1.151: icmp_seq=19 ttl=64 time=0.059 ms
10008 bytes from 192.168.1.151: icmp_seq=20 ttl=64 time=0.060 ms

--- 192.168.1.151 ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 19461ms
rtt min/avg/max/mdev = 0.059/0.066/0.103/0.012 ms
```

### Server & Client Test via iperf3 (PC-Router-DUT)

<details>

<summary>iperf3</summary>

```
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
Accepted connection from 192.168.1.252, port 49723
[  5] local 192.168.1.151 port 5201 connected to 192.168.1.252 port 49724
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  1.30 MBytes  10.9 Mbits/sec    0   65.6 KBytes       
[  5]   1.00-2.00   sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]   2.00-3.00   sec  1.07 MBytes  8.99 Mbits/sec    0   65.6 KBytes       
[  5]   3.00-4.00   sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]   4.00-5.00   sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]   5.00-6.00   sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]   6.00-7.00   sec  1.38 MBytes  11.6 Mbits/sec    0   65.6 KBytes       
[  5]   7.00-8.00   sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]   8.00-9.00   sec  1.19 MBytes  10.0 Mbits/sec    0   65.6 KBytes       
[  5]   9.00-10.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  10.00-11.00  sec  1.07 MBytes  8.99 Mbits/sec    0   65.6 KBytes       
[  5]  11.00-12.00  sec   784 KBytes  6.42 Mbits/sec    0   65.6 KBytes       
[  5]  12.00-13.00  sec   784 KBytes  6.42 Mbits/sec    0   65.6 KBytes       
[  5]  13.00-14.00  sec  1.07 MBytes  8.99 Mbits/sec    0   65.6 KBytes       
[  5]  14.00-15.00  sec   627 KBytes  5.14 Mbits/sec    0   65.6 KBytes       
[  5]  15.00-16.00  sec   941 KBytes  7.71 Mbits/sec    0   65.6 KBytes       
[  5]  16.00-17.00  sec   627 KBytes  5.14 Mbits/sec    0   65.6 KBytes       
[  5]  17.00-18.00  sec   941 KBytes  7.71 Mbits/sec    0   65.6 KBytes       
[  5]  18.00-19.00  sec   941 KBytes  7.71 Mbits/sec    0   65.6 KBytes       
[  5]  19.00-20.00  sec   941 KBytes  7.71 Mbits/sec    0   65.6 KBytes       
[  5]  20.00-21.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  21.00-22.00  sec  1.07 MBytes  8.99 Mbits/sec    0   65.6 KBytes       
[  5]  22.00-23.00  sec   941 KBytes  7.71 Mbits/sec    0   65.6 KBytes       
[  5]  23.00-24.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  24.00-25.00  sec  1.07 MBytes  8.99 Mbits/sec    0   65.6 KBytes       
[  5]  25.00-26.00  sec  1.38 MBytes  11.6 Mbits/sec    0   65.6 KBytes       
[  5]  26.00-27.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  27.00-28.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  28.00-29.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  29.00-30.00  sec  1.23 MBytes  10.3 Mbits/sec    0   65.6 KBytes       
[  5]  30.00-30.08  sec   157 KBytes  15.6 Mbits/sec    0   65.6 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.08  sec  32.8 MBytes  9.15 Mbits/sec    0             sender
[  5]   0.00-30.08  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   40.436787] rtw_core: loading out-of-tree module taints kernel.
[   40.664687] rtw_8723de 0000:01:00.0: enabling device (0000 -> 0002)
[   40.681400] rtw_8723de 0000:01:00.0: Firmware version 48.0.0, H2C version 0
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
Accepted connection from 192.168.175.86, port 49765
[  5] local 192.168.175.1 port 5201 connected to 192.168.175.86 port 49766
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  1.45 MBytes  12.2 Mbits/sec    0   68.4 KBytes       
[  5]   1.00-2.00   sec  1.56 MBytes  13.1 Mbits/sec    0   68.4 KBytes       
[  5]   2.00-3.00   sec  1.72 MBytes  14.4 Mbits/sec    0   68.4 KBytes       
[  5]   3.00-4.00   sec  1.23 MBytes  10.3 Mbits/sec    1   68.4 KBytes       
[  5]   4.00-5.00   sec  1.47 MBytes  12.3 Mbits/sec    0   68.4 KBytes       
[  5]   5.00-6.00   sec  1.41 MBytes  11.8 Mbits/sec    0   68.4 KBytes       
[  5]   6.00-7.00   sec  1.93 MBytes  16.2 Mbits/sec    0   68.4 KBytes       
[  5]   7.00-8.00   sec  1.87 MBytes  15.7 Mbits/sec    0   68.4 KBytes       
[  5]   8.00-9.00   sec  2.14 MBytes  18.0 Mbits/sec    0   68.4 KBytes       
[  5]   9.00-10.00  sec  2.14 MBytes  18.0 Mbits/sec    0   68.4 KBytes       
[  5]  10.00-11.00  sec  2.17 MBytes  18.2 Mbits/sec    0   68.4 KBytes       
[  5]  11.00-12.00  sec  1.99 MBytes  16.7 Mbits/sec    0   68.4 KBytes       
[  5]  12.00-13.00  sec  2.14 MBytes  18.0 Mbits/sec    0   68.4 KBytes       
[  5]  13.00-14.00  sec  1.68 MBytes  14.1 Mbits/sec    0   68.4 KBytes       
[  5]  14.00-15.00  sec  1.84 MBytes  15.4 Mbits/sec    0   68.4 KBytes       
[  5]  15.00-16.00  sec  1.23 MBytes  10.3 Mbits/sec    0   68.4 KBytes       
[  5]  16.00-17.00  sec  1.84 MBytes  15.4 Mbits/sec    0   68.4 KBytes       
[  5]  17.00-18.00  sec  1.38 MBytes  11.6 Mbits/sec    0   68.4 KBytes       
[  5]  18.00-19.00  sec  1.44 MBytes  12.1 Mbits/sec    0   68.4 KBytes       
[  5]  19.00-20.00  sec  1.84 MBytes  15.4 Mbits/sec    0   68.4 KBytes       
[  5]  20.00-21.00  sec  2.14 MBytes  18.0 Mbits/sec    0   68.4 KBytes       
[  5]  21.00-22.00  sec  2.05 MBytes  17.2 Mbits/sec    0   68.4 KBytes       
[  5]  22.00-23.00  sec  1.26 MBytes  10.5 Mbits/sec    1   68.4 KBytes       
[  5]  23.00-24.00  sec  1.75 MBytes  14.6 Mbits/sec    0   68.4 KBytes       
[  5]  24.00-25.00  sec  1.90 MBytes  15.9 Mbits/sec    0   68.4 KBytes       
[  5]  25.00-26.00  sec  2.02 MBytes  17.0 Mbits/sec    0   68.4 KBytes       
[  5]  26.00-27.00  sec  1.87 MBytes  15.7 Mbits/sec    0   68.4 KBytes       
[  5]  27.00-28.00  sec  1.78 MBytes  14.9 Mbits/sec    0   68.4 KBytes       
[  5]  28.00-29.00  sec  1.90 MBytes  15.9 Mbits/sec    0   68.4 KBytes       
[  5]  29.00-30.00  sec  1.90 MBytes  15.9 Mbits/sec    0   68.4 KBytes       
[  5]  30.00-30.08  sec   157 KBytes  15.3 Mbits/sec    0   68.4 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-30.08  sec  53.2 MBytes  14.8 Mbits/sec    2             sender
[  5]   0.00-30.08  sec  0.00 Bytes  0.00 bits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
iperf3: interrupt - the server has terminated
[   40.436787] rtw_core: loading out-of-tree module taints kernel.
[   40.664687] rtw_8723de 0000:01:00.0: enabling device (0000 -> 0002)
[   40.681400] rtw_8723de 0000:01:00.0: Firmware version 48.0.0, H2C version 0
```

</details>

### End of Report
