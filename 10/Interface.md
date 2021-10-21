#### 약어
- AS(Access Stratum)
- AF(Application Function)
- OFCS(Offline Charging System)
- PCRF(Policy and Charging Rule Function)
- SPR(Subscriber Profile Repository) : PCRF에게 가입자 및 가입 관련 정보 제공
- HSS(Home Subscriber Server)
- MME(Moblility Management Entity) : HSS와 s6a 인터페이스를 통해 사용자 인증 및 로밍 기능 제공
- ePDG(enhanced Packet Data Gateway) : Untrusted WLAN(=WIFI)를 LTE 망에 연동시키기 위한 Access Gateway
- EIR(Equipment Identity Register)
- GMLC(Gateway Mobile Location Centre) : 위치 기반 서비스 지원 
#### 인터페이스
- gx : PGW <-> PCRF
- gy : PGW <-> OCS
- rx : AF <-> PCRF
- rf : AS <-> OFCS
- s6a : HHS <-> MME
- s6b : PGW <-> 3GPP AAA server/proxy
- s9 : PCRF(HOME) <-> PCRF(VISITOR)
- slg : GMLC <-> MME
- sy : PCRF <-> OCS
- swm : 3GPP AAA server/proxy <-> ePDG
- sta : trusted non-3GPP IP access <-> 3GPP AAA server/proxy
- s13 : MME <-> EIR
- sh : AS <-> HSS
- sp : PCRF <-> SPR


https://www.f5.com/services/resources/glossary/diameter-interfaces

https://www.cablefree.net/wirelesstechnology/4glte/lte-interfaces/

https://www.netmanias.com/ko/post/blog/5484/ipsec-lte-wi-fi-epdg/network-architecture-for-lte-and-wi-fi-interworking-part-1-nrm
