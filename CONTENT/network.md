# Network Configuration

## Preface

- Make sure that you have the network card driver installed before performing any actions.

## Cable connections:

- The most common types of cables include UTP, FTP, STP, S/FTP, S/STP, as well as cat5, cat5e, cat6, cat6a, cat7 and cat8 standards. The ideal and most expensive choice is to use a cat8 shielded cable (STP) with a length of up to 50 cm or less. In case of a limited budget (and low Internet speed), it is recommended to pay attention to cat5e or cat6 shielded cables (STP or S/STP). This will provide a more stable connection to the network and image No. 1

## Important facts (which few people know about):

- It costs about $5 to manufacture all network adapters in China. Changing your traffic provider from a cyclic one to a more delay-sensitive one can lead to an increase in connection speed up to ± 500 times. Many providers use package aggregation, which allows them to increase download speeds by combining multiple packages into one. Some network cards, such as Solarflare, have a delay time.

## Choose a network adapter:

- If you have a Realtek adapter installed, you may encounter problems, while Intel adapters usually provide reliable performance. The preferred option is to use built-in network adapters from Intel or external adapters of the same brand. Remember to periodically update the drivers for your network adapter (LAN/WI-FI) by downloading them from the motherboard manufacturer's official website.

## A bit of theory:

- Internet speed is defined as the number of bits of information transmitted per second, measured in kilobits per second (Kbps), megabits per second (Mbps), or gigabits per second (Gbps). You can perform an [Internet speed test](http://www.dslreports.com/speedtest).

- Packet loss occurs when one or more packets do not reach their destination address during data transmission. You can perform a [packet loss test](https://packetlosstest.com).

- Excessive network buffering can result in increased latency and jitter, as well as reduced throughput. You can perform a test for excessive [network buffering](https://www.waveform.com/tools/bufferbloat).

## Network Adapter Settings

- Offloading features in network cards delegate specific packet handling functions, reducing CPU consumption. This ideally allocates more CPU time for other tasks and gaming activities.

# Settings for Intel Recommendations:

## Configuring the network card

```
Offload: (Recommended: On - if your adapter is good enough and has a decent driver. Off - if your adapter is shit or has a crappy adapter driver)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *EncapsulatedPacketTaskOffloadNvgre (Values 0-1 where 0 is full off and 1 is full on).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *EncapsulatedPacketTaskOffloadVxlan (Values 0-1 where 0 is Full Shutdown and 1 is Full Enable)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *EncapsulatedPacketTaskOffload (Values 0-1 where 0 is full off and 1 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *IPChecksumOffloadIPv4 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *LsoV1IPv4 (Values 0-1 where 0 is full off and 1 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *LsoV2IPv4 (Values 0-1 where 0 is Full Power Off and 1 is Full Power On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *LsoV2IPv6 (Values 0-1 where 0 is Full Power Off and 1 is Full Power On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *TCPChecksumOffloadIPv4 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *TCPCPChecksumOffloadIPv6 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *UDPChecksumOffloadIPv4 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *UDPChecksumOffloadIPv6 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *IPsecOffloadV1IPv4 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *IPsecOffloadV2 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *IPsecOffloadV2IPv4 (Values 0-3 where 0 is full off and 3 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *TCPConnectionOffloadIPv4 (Values 0-1 where 0 is full off and 1 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *TCPConnectionOffloadIPv6 (Values 0-1 where 0 is Full Off and 1 is Full On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *TCPUDPChecksumOffloadIPv4 (Values 0-3 where 0 is Full Off and 3 is Full On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *TCPUDPChecksumOffloadIPv6 (Values 0-3 where 0 is Full Power Off and 3 is Full Power On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *UsoIPv4 (Values 0-1 where 0 is Full Disable and 1 is Full Enable)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *UsoIPv6 (Values 0-1 where 0 is Full Off and 1 is Full On)

VMQ: (Recommended: off)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *VMQ (Values 0-1 where 0 is full off and 1 is full on).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *VMQVlanFiltering (Values 0-1 where 0 is Full Off and 1 is Full On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : MaxDelayInFreeVmqOID (Значения -1-800)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : VMQSupported (Values 0-1 where 0 is full off and 1 is full on)

RSC: (Recommended: off)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *RscIPv4 (Values 0-1 where 0 is completely off and 1 is completely on).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *RscIPv6 (Values 0-1 where 0 is Full Power Off and 1 is Full Power On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : ForceRscEnabled (Values 0-1 where 0 is Full Disable and 1 is Full Enable)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : RscMode (Values 0-2)

POWERSAVING: (Recommended: off)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *DeviceSleepOnDisconnect (Values 0-1 where 0 is completely off and 1 is completely on).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *PMARPOffload (Values 0-1 where 0 is Full Power Off and 1 is Full Power On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *PMNSOffload (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *WakeOnMagicPacket (Values 0-1 where 0 is full off and 1 is full on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *WakeOnPattern (Values 0-1 where 0 is completely off and 1 is completely on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *NicAutoPowerSaver (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *PMWiFiRekeyOffload (Values 0-1 where 0 is Full Off and 1 is Full On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EEELinkAdvertisement (Values 0-1 where 0 is completely off and 1 is completely on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EnableModernStandby (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EnablePME (Values 0-1 where 0 is full power off and 1 is full power on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EnablePowerManagement (Values 0-1 where 0 is full power off and 1 is full power on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : ForceWakeFromMagicPacketOnModernStandby (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : WakeFromS5 (Values 0-FFFF where 0 is a complete shutdown and the rest is a power on with a certain ???). 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : WakeOn (Values 0-4 where 0 is a full shutdown and the rest are full on with a certain ???). 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : WakeOnLink (Values 0-2 where 0 is a complete shutdown and the rest are full on with a certain ????) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : LinkNegotiationProcess (Values 0-1 where 0 is completely off and 1 is completely on). 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : WaitForValidPhyIDRead (Values 0-1 where 0 is full off and 1 is full on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : WaitAutoNegComplete (Values 0-2 where 0 is a complete shutdown and 1 is a complete on with a certain ???) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : SleepWhileWaiting (Values 0-1 where 0 is full shutdown and 1 is full on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EnableETW (Values 0-1 where 0 is completely off and 1 is completely on) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : OBFFEnabled (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : ULPMode (Values 0-1 where 0 is completely off and 1 is completely on). 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : I218DisablePLLShut (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : I218DisablePLLShutGiga (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : I219DisableK1Off (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : DisableDelayedPowerUp (Values 0-1 where 0 is Full Power Off and 1 is Full Power On) 

HEADER DATA SPLIT:
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *HeaderDataSplit (Values 0-1 where 0 is full off and 1 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : HDSplitAlways (Values 0-1 where 0 is completely off and 1 is completely on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : HDSplitBufferPad (Значения 0-2)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : HDSplitLocation (Значения 0-3)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : HDSplitSize (Значения 128-960)

RECEIVE BUFFERS:
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : *ReceiveBuffers (Значения 128-4096)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : ReceiveBuffersOverride (Values 0-1 where 0 is full power off and 1 is full power on).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : MaxPacketCountPerDPC (Значения 8-FFFF)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : MaxPacketCountPerIndicate (Значения 1-FFFF)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : RxDescriptorCountPerTailWrite (Значения 4-4096)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : MinHardwareOwnedPacketCount (Значения 8-4096)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : RxBufferPad (Значения 0-63)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : RegForceRxPathSerialization (Values 0-1 where 0 is full off and 1 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EnableRxDescriptorChaining (Values 0-1 where 0 is completely off and 1 is completely on).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : EnableAdaptiveQueuing (Values 0-1 where 0 is completely off and 1 is completely on) (Recommended: off)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : AdaptiveQHysteresis (Значения 16-1024)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : AdaptiveQSize (Значения 64-2000)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : AdaptiveQWorkSet (Значения 32-2000)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : PadReceiveBuffer (Values 0-1 where 0 is full off and 1 is full on)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : StoreBadPackets (Values 0-1 where 0 is completely off and 1 is completely on) (Recommended: off).
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : ERT (Values 0-1 where 0 is Full Off and 1 is Full On)
Registry\Machine\SYSTEM\ControlSet001\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}\0009 : DynamicLTR (Values 0-1 where 0 is Full Off and 1 is Full On) (Recommended: Off)
 ```

- **These recommendations aim to optimize network performance and reduce latency. For further details and explanations, refer to Intel's and Microsoft's network subsystem performance tuning support guides, available in the Technical References section.**

## Operating System Specific Configuration

- Make sure the Network Throttling Index feature is enabled. Recommendation: Set the value between 10 and 20 decimal places, for example, 15 Mbps to 30 Mbps.
```HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\NetworkThrottlingIndex``` 
For more information about Network Throttling Index and its effect on NDIS DPC processing latency, see the study on [Network Throttling Index](../../RESEARCH/NETWORK/README.md#networkthrottlingindex).

- Open cmd as administrator and enter the following commands:

## IP Settings
 ```
netsh winsock reset catalog 
netsh int ip reset c:resetlog.txt 
netsh int ip reset C:\tcplog.txt
netsh int tcp set heuristics disabled
netsh int tcp set supplemental Internet congestionprovider=ctcp
netsh int tcp set global rsc=disabled
netsh int tcp set global chimney=disabled
netsh int tcp set global chimney=enabled
netsh int tcp set global autotuninglevel=normal
netsh int tcp set global congestionprovider=ctcp
netsh int tcp set global autotuninglevel=disabled
netsh advfirewall firewall add rule name="Block Windows Telemetry" dir=in action=block remoteip=134.170.30.202,137.116.81.24,157.56.106.189,184.86.53.99,2.22.61.43,2.22.61.66,204.79.197.200,23.218.212.69,65.39.117.23,65.55.108.23,64.4.54.254 enable=yes
netsh advfirewall firewall add rule name="Block NVIDIA Telemetry" dir=in action=block remoteip=8.36.80.197,8.36.80.224,8.36.80.252,8.36.113.118,8.36.113. 141,8.36.80.230,8.36.80.231,8.36.113.126,8.36.80.195,8.36.80.217,8.36.80.237,8.36.80.246,8.36.113.116,8.36.113.139,8.36.80.244,216.228.121.209 enable=yes
 ```

## Security concerns
 ```
netsh int ip set global taskoffload=enabled
netsh int ip set global dhcpmediasense=disabled
netsh int ip set global mediasenseeventlog=disabled
netsh int ip set global icmpredirects= disabled
 ```
## TCP settings
 ```
netsh int tcp set supplemental template=custom icw=10
netsh int tcp set global nonsackrttresiliency=disabled
netsh int tcp set global rsc=disabled
netsh int tcp set global dca=enabled
netsh int tcp set global netdma=disabled
netsh int tcp set heuristics disabled
netsh int tcp set global chimney=disabled
netsh int tcp set global dca=enabled
netsh int tcp set global netdma=disabled
netsh int tcp set global rsc=disabled
netsh int tcp set global timestamps=disabled
netsh int tcp set global ecncapability=disabled
netsh int tcp set global ecn=disabled
netsh int tcp set global timestamps=disabled
netsh int tcp set global nonsackrttresiliency=disabled
netsh int tcp set global maxsynretransmissions=2
netsh int tcp set global fastopen=enabled
netsh int tcp set global fastopenfallback=enabled
netsh int tcp set global rss=enabled
netsh int tcp set global hystart=enabled
netsh int tcp set global initialRto=2000
 ```

## Disable ICMP Redirects for security
 ```
netsh int tcp set global chimney=enabled
netsh int tcp set global dca=enabled
netsh int tcp set global netdma=disabled
netsh int tcp set global rsc=disabled
netsh int tcp set global maxsynretransmissions=2
netsh int tcp set global timestamps=disabled
netsh int tcp set global ecncapability=disabled
netsh interface teredo set state disabled
netsh int isatap set state disable
 ```

## UDP settings
 ```
netsh int udp set global uro=enabled
 ```

## IPv6 settings
 ```
netsh interface teredo set state disabled
netsh int isatap set state disable
netsh int ipv6 isatap set state disabled
netsh int ipv6 6to4 set state disabled
netsh interface IPV6 set global randomizeidentifier=disabled
netsh interface IPV6 set privacy state=disabled
 ```

## Get the interface name
 ```
$INTERFACE = (netsh int ip show interfaces | Select-String -Pattern '0-9' | % { $_.Matches[0].Value })[0]
netsh int ip set interface $INTERFACE dadtransmits=1 routerdiscovery=disabled ecncapability=ecndisabled store=persistent
netsh int tcp set heuristics disabled
netsh int tcp set heuristics wsh=disabled
netsh int tcp set security mpp=disabled
netsh int tcp set security profiles=disabled >nul
netsh int ipv4 set dynamicport tcp start=1025 num=645111
netsh int ipv4 set dynamicport udp start=1025 num=64511
netsh int ip set global icmpredirects=disabled
netsh int ip set global multicastforwarding=disabled
 ```

### Tips

- Optimize the performance of your system using the best available CPU, RAM and GPU components. Perform a quality overclocking of these components, taking into account the speed of the CPU and RAM, as well as RAM timings and CPU cache size. These parameters directly affect system latency, which can impact hit-reg performance in game scenarios.

- If possible, consider removing the router from the network chain. Connect the network cable directly, bypassing the router. This may result in a slight decrease in ping by 1-3 milliseconds.
