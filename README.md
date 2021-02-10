How to configure a Cisco router as a local dial up ISP

You will need a Cisco router 2821, 2851, 3825, 3845, I used a 3825.
You will also need a digital modem carrier with digital modem cards,
the modems only work with the network modules the NM-1CE1T1-PRI works,
That completes the Access Server side of the configuration. For the
dial in side you will need some FXS ports (VIC-4FXS/DID) and a
PVDM2-64 to convert analog to PCM so it can be transmitted on the 
ISDN network, also a T1 card that provides a voice-port, will be
needed, I used a VWIC2-2MFT-T1/E1. One last thing, you will need to
make a T1 PRI crossover cable to connect the VWIC2-2MFT-T1/E1 to 
the NM-1CE1T1-PRI.

https://www.kieranlane.com/2012/02/26/isdn-crossover-cable-pinout/

Once the router is assembled and configured you can connect modems to
the FXS ports and dial in with the phone number 5035551212 and get on
line using the username cisco and the password cisco.

[ROUTER INVENTORY]

NAME: "3825 chassis", DESCR: "3825 chassis"
PID: CISCO3825         , VID: V03 , SN: FTX1117A17B

NAME: "VWIC2-2MFT-T1/E1 - 2-Port RJ-48 Multiflex Trunk - T1/E1 on Slot
0 SubSlot 0", DESCR: "VWIC2-2MFT-T1/E1 - 2-Port RJ-48 Multiflex Trunk -
T1/E1"
PID: VWIC2-2MFT-T1/E1  , VID: V01 , SN: FOC15200Y3D

NAME: "Four port FXS DID voice interface daughtercard on Slot 0 SubSlot
2", DESCR: "Four port FXS DID voice interface daughtercard"
PID: VIC-4FXS/DID=     , VID: 3.1, SN: FOC11245MK6

NAME: "Four port FXS DID voice interface daughtercard on Slot 0 SubSlot
3", DESCR: "Four port FXS DID voice interface daughtercard"
PID: VIC-4FXS/DID=     , VID: 3.1, SN: FOC11222QBF

NAME: "PVDMII DSP SIMM with four DSPs on Slot 0 SubSlot 4", DESCR:
"PVDMII DSP SIMM with four DSPs"
PID: PVDM2-64          , VID: V01 , SN: FOC1239666S

NAME: "Digital Modem Carrier on Slot 1", DESCR: "Digital Modem Carrier"
PID: NM-30DM=          , VID: 0.2, SN: 21947277

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164963

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164963

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165083

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165083

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164962

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21164962

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165089

NAME: "MICA-6DM Simm", DESCR: "MICA-6DM Simm"
PID: MICA-6DM Simm     , VID: 2.1, SN: 21165089

NAME: "One Port Channelized E1/T1/PRI with Integrated CSU on Slot 2",
DESCR: "One Port Channelized E1/T1/PRI with Integrated CSU"
PID: NM-1CE1T1-PRI=    , VID: V01 , SN: FOC11475K2A

[ROUTER CONFIG]

version 15.1

service timestamps debug datetime msec

service timestamps log datetime msec

service password-encryption

!

hostname 3825-AS

!

boot-start-marker

boot system flash:c3825-adventerprisek9_ivs-mz.151-4.M12a.bin

boot-end-marker

!

!

card type t1 0 0

card type t1 2

enable secret 5 [deleted]

!

aaa new-model

!

!

aaa authentication login default local

aaa authentication login NO_AUTHEN none

aaa authentication ppp default local

aaa authorization network default local

!

!

!

!

!

aaa session-id common

!

no network-clock-participate slot 2

network-clock-participate wic 0

!

modem firmware slot 1 location flash:mica-modem-pw.2.9.5.0.bin

modem country mica t1-default

dot11 syslog

ip source-route

!

ip cef

!

!

no ip dhcp conflict logging

!

ip dhcp pool NETWORK

 network 10.0.10.0 255.255.255.0

 default-router 10.0.10.1

 dns-server 10.0.10.1

 domain-name example.com

!

!

ip domain name example.com

ip name-server 192.168.1.1

no ipv6 cef

!

multilink bundle-name authenticated

!

!

!

!

async-bootp dns-server 192.168.1.1

isdn switch-type primary-ni

!

modemcap entry MICA:MSC=&F&D2S0=0S29=6S21=3S34=18000S40=10S10=50

voice-card 0

!

!

!

!

!

!

!

crypto pki token default removal timeout 0

!

!

!

!

license udi pid CISCO3825 sn FTX1117A17B

license accept end user agreement

username adam privilege 15 secret 5 [deleted]

username cisco password 7 14141B180F0B

!

redundancy

!

!

controller T1 0/0/0

 clock source internal

 cablelength short 110
 
 pri-group timeslots 1-24

!

controller T1 0/0/1

 shutdown
 
 cablelength long 0db

!

controller T1 2/0

 framing ESF
 
 linecode b8zs
 
 cablelength short 110
 
 pri-group timeslots 1-24

!

!

!

!

!

!

!

!

!

interface Loopback0
 
 ip address 10.0.20.1 255.255.255.0

!

interface Loopback1
 
 ip address 10.0.30.1 255.255.255.0

!

interface GigabitEthernet0/0
 
 ip address dhcp
 
 ip nat outside
 
 ip virtual-reassembly in
 
 duplex auto
 
 speed auto
 
 media-type rj45

!

interface GigabitEthernet0/1
 
 ip address 10.0.10.1 255.255.255.0
 
 ip nat inside
 
 ip virtual-reassembly in
 
 duplex auto
 
 speed auto
 
 media-type rj45
 
 no cdp enable

!

interface Serial0/0/0:23
 
 no ip address
 
 encapsulation ppp
 
 isdn switch-type primary-ni
 
 isdn protocol-emulate network
 
 isdn incoming-voice modem 64
 
 ppp multilink

!

interface Serial2/0:23
 
 no ip address
 
 ip nat inside
 
 encapsulation ppp
 
 dialer rotary-group 10
 
 dialer-group 5
 
 isdn switch-type primary-ni
 
 isdn incoming-voice modem 64
 
 ppp multilink

!

interface Dialer10
 
 ip unnumbered Loopback1
 
 ip nat inside
 
 ip virtual-reassembly in
 
 encapsulation ppp
 
 dialer in-band
 
 dialer idle-timeout 900
 
 dialer-group 5
 
 peer default ip address pool ISDN
 
 ppp authentication ms-chap-v2 ms-chap chap
 
 ppp multilink
 
!

interface Group-Async0
 
 ip unnumbered Loopback0
 
 ip nat inside
 
 ip virtual-reassembly in
 
 encapsulation ppp
 
 dialer in-band
 
 dialer idle-timeout 900
 
 dialer-group 5
 
 peer default ip address pool ASYNC
 
 async mode interactive
 
 no fair-queue
 
 no keepalive
 
 ppp reliable-link
 
 ppp authentication ms-chap-v2 ms-chap chap
 
 ppp multilink
 
 group-range 1/0 1/23
 
!

!

router eigrp 69
 
 network 10.0.0.0
 
 auto-summary
 
 no eigrp log-neighbor-changes

!

ip local pool ASYNC 10.0.20.100 10.0.20.254

ip local pool ISDN 10.0.30.100 10.0.30.254

ip default-gateway 192.168.1.1

ip forward-protocol nd

no ip http server

no ip http secure-server

!

!

ip dns server

ip nat inside source list 100 interface GigabitEthernet0/0 overload

ip route 0.0.0.0 0.0.0.0 192.168.1.1

!

access-list 100 permit ip 10.0.10.0 0.0.0.255 any

access-list 100 permit ip 10.0.20.0 0.0.0.255 any

access-list 100 permit ip 10.0.30.0 0.0.0.255 any

access-list 101 remark used in dialer-list 5

access-list 101 deny   eigrp any any

access-list 101 permit ip any any

dialer-list 5 protocol ip list 101

!

!

!

!

!

!

!

!

control-plane

!

!

voice-port 0/0/0:23

!

voice-port 0/2/0

!

voice-port 0/2/1

!

voice-port 0/2/2

!

voice-port 0/2/3

!

voice-port 0/3/0

!

voice-port 0/3/1

!

voice-port 0/3/2

!

voice-port 0/3/3

!

!

!

mgcp profile default

!

!

dial-peer voice 1000 pots

 destination-pattern ..........
 
 incoming called-number 5035551212
 
 port 0/0/0:23

!

!

!

!

gatekeeper
 
 shutdown

!

!

!

line con 0
 
 exec-timeout 0 0
 
 login authentication NO_AUTHEN

line aux 0

line 1/0 1/23
 
 modem Dialin
 
 modem autoconfigure type MICA
 
 transport input all
 
 autoselect during-login
 
 autoselect ppp

line vty 0 4
 
 exec-timeout 0 0
 
 transport input ssh

!

scheduler allocate 20000 1000

ntp server 192.168.1.1

end




