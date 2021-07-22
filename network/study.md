[Netmanias.2010.02.10_Training_Material_for_Network_Engineer.pdf](https://github.com/lapaho8645/2021/files/6853796/Netmanias.2010.02.10_Training_Material_for_Network_Engineer.pdf)
===========================================================================

## 목록

> ### [1. 프로토콜](#프로토콜)
> ### [2. OSI 7 Layer Architecture](#osi-7-layer-architecture)
> ### [3. TCP/IP Architecture](#tcpip-architecture)
> ### [4. 포트와 소켓](#포트와-소켓)
> ### [5. Internetworking Device](#internetworking-device)
> ### [6. Ethernet](#ethernet)

## 프로토콜
* 컴퓨터나 통신 장비 사이에서 메시지를 주고 받기 위해 설계된 일련의 규칙 체계
* Syntax, Semantic, Actions
* 프로토콜들의 역할을 분담하여 특정 서비스를 제공하기 위한 Protocol의 계층별 집합 
* Protocol Data Unit : 발송지/목적지 주소, 사용자 정보, 오류 검출 정보, 흐름 제어 정보
![image](https://user-images.githubusercontent.com/64197428/126431981-3f6acb48-fee7-4f79-9bd8-8dcfd17e4e43.png)

## OSI 7 Layer Architecture
데이터를 전송할 때 각각의 층에서 헤더를 붙이는 과정을 캡슐화라고 하고, 전송된 데이터의 헤더를 벗기는 과정을 디캡슐레이션이라고 한다. 각각의 층마다 요청과 응답을 하면서 상호작용하기 떄문에 서버와 클라이언트 관계라고 할 수 있다. 
#### 1. Physical Layer
* **비트** 단위의 정보를 물리적 매체를 통해 전자기적 신호나 광 신호로 전달
> 장비 : 허브, 리피터
#### 2. Data Link Layer
* 하나의 **프레임**을 오류없이 안전하게 전송하는 것이 목적
> 장비 : 브리지, 스위치
#### 3. Network Layer
* **패킷**을 발신지로부터 목적지로 전달하는 Packet Path 제공
* Routing, Flow Control, Error Control 수행
> 장비 : 라우터
> 
> 프로토콜 : IP, ICMP, IGMP
#### 4. Transport Layer
* 메시지를 **Segmentation/Reassembly**
* 정보 전송, Flow Control, Checksum 방식으로 전송에러 검출
> 장비 : 게이트웨이
> 
> 프로토콜 : TCP, UDP, ARP
#### 5. Session Layer
* 응용 간의 질서 제어
#### 6. Presentation Layer
* 이해할 수 있는 포멧 변환
#### 7. Application Layer
* 사용자가 네트워크에 접근할 수 있게 해주며 사용자 응용프로그램간에 정보교환을 담당
> 프로토콜 : DHCP, DNS, FTP, HTTP
## TCP/IP Architecture
#### 1. Network Interface Layer
* 노드간의 신뢰성 있는 데이터 전송을 담당
> MAC 주소
>
> 프로토콜 : Ethernet, TokenRing
#### 2. Internet Layer
* 데이터를 정의하고 데이터의 경로를 배정하는 라우팅을 담당
> IP 주소
#### 3. Transport Layer
* 목적지까지 오류 없이 데이터를 전송
> 포트 번호
#### 4. Application Layer
* 전송 계층을 기반으로 한 다수의 프로토콜과 응용 프로그램을 포괄
> 소켓

## 포트와 소켓
#### 포트
포트는 네트워크를 통해 데이터를 주고 받는 프로세스를 식별하기 위해 호스트 내부적으로 프로세스가 할당받는 고유한 값이다. 메시지가 목적지 호스트에 도착하면 호스트 내에서 특정 포트번호를 할당받은 프로세스를 찾아 데이터를 전달하게 된다. 데이터를 보내는 프로세스, 데이터를 받는 프로세스 둘 다 포트 번호를 할당받아야 한다.
#### 소켓
프로세스가 네트워크를 통해서 데이터를 주고 받기 위해 열어야 하는 것으로 소켓을 열기 위해서는 호스트에 할당된 IP주소, 포트 넘버, 프로토콜 등이 필요하다. 

## MAC 주소
네트워크 하드웨어를 식별하는 주소

## Internetworking Device
#### Repeater
* 거리가 증가할수록 감쇄되는 신호를 증폭하여 연결된 네트워크로 전송
* 신호를 재생하여 전달되는 거리를 증가
#### Bridges
* LAN과 LAN을 상호 연결 
* MAC 주소를 조사하여 데이터링크층이 관리하는 패킷의 소스 주소와 목적지 주소를 보고 그 패킷을 통과시킬지를 판정해서 traffic을 filtering하는 기능과 데이터를 fowarding하는 기능
* 수신된 Ethernet Frame의 도착지 MAC 주소에 기초하여 특정 포트로 전송
* plug-and-play, sulf-learning -> 라우터와 달리 사용자가 설정할 필요가 없음
* 1:1방식으로 각각의 port는 대역폭을 보장 받음
* Collision Domains을 서로 분리
![image](https://user-images.githubusercontent.com/64197428/126580357-8aa62619-30be-423f-90ab-c8812000afef.png)
* 수신 프레임을 버퍼에 저장한 후 수신 프레임의 목적지 MAC 주소와 동일한 것을 브리지 테이블에서 찾아내어 해당 출력 포트로 프레임을 전달
#### Routers
* 다른 기종간의 네트워크를 연결하는 역할을 하며 특히 LAN과 WAN을 연결하는 데 많이 사용
* 트래픽이 가장 적은 경로를 찾아 목적지로 데이터를 전송하는 기능
![image](https://user-images.githubusercontent.com/64197428/126450696-ee0e09f8-ae2f-47ec-bfc2-7cc60d1ac8e9.png)
#### Hubs
* 네트워크 장비와 장비를 UTP 케이블로 연결하기 위해 사용
* Multiport Repeater
* 하나의 큰 충돌 도메인
* Dummy Hub (1계층 장비): 허브에 전달되는 데이터를 연결된 모든 컴퓨터로 전달하며 이 떄 허브에 연결된 다른 컴퓨터들은 데이터 전송이 끝날 때까지 통신할 수 없다. 따라서 포트 수가 증가할 수록 트랙픽이 발생 
* Switching Hub (2계층 장비) : 연결된 포트들을 1:1로 연결해주는 통로가 제공되어 포트를 스위칭해서 목적지에만 전달한다.
#### Gateway
* 서로 다른 네트워크 상의 통신 프로토콜을 적절히 변환하여 연결해주는 시스템
* 하나 이상의 프로토콜을 사용하여 통신한다는 점에서 라우터, 스위치와 구별됨

![image](https://user-images.githubusercontent.com/64197428/126582029-56a228f8-fe17-4841-9fb3-223776ed2dd7.png)

## Ethernet
가장 대표적인 버스 구조 방식의 근거리 통신망 LAN을 대표하는 기술로 각 기기들의 고유의 주소 MAC주소를 가지고 호스트간의 데이터를 주고 받을 수 있는 방식이다. 하나의 물리적인 전송매체를 다수의 단말이 공유하기 떄문에 두 개 이상의 단말이 동시에 수신한 프레임은 상호 충돌에 의해 모두 버려질 수 있다.
#### CSMA/CD(Carrier Sense Multiple Access/Collision Detection) 프로토콜
1. 통신을 하고 싶은 PC나 서버는 지금 네트워크 상에 통신이 일어나고 있는 지(캐리어가 감지 되면) 확인(Carrier Sense)
2. 캐리어가 감지되지 않으면 데이터를 네트워크에 보내는데 이떄 두 개 이상의 장비들이 데이터를 동시에 보내는 상황 발생(Multiple Access with Collision Detection)
3. collision이 발생하면 데이터를 전송했던 PC들은 랜덤한 시간동안 기다린 후 다시 전송하게 된다.
#### Ethernet MAC frame format
![image](https://user-images.githubusercontent.com/64197428/126583736-1219267f-87b0-4995-9f13-68df7dd01abe.png)
* Preamble : 송/수신 속도를 일치시키기 위해 비트 동기화를 맞추는 것
* SFD(Starting Frame Delimiter) : 수신자에게 데이터가 이어짐을 알려주기 위한 것으로 프레임의 시작을 알리는 필드
* Destination address/Source Address : 물리적 주소로 어떤 이더넷에 있는 어떤 노드도 유일한 주소를 가진다. Destination Address는 도착 노드의 고유 주소이고, SOurce Address는 전송 노드의 고유 주소이다.
* Ether Type : 도착한    상위 계층의 네트워크 프로토콜의 데이터 형식을 확인하고 패킷을 어떻게 처리할 것인지를 결정하는 데 사용한다. 즉, 상위 계층 프로토콜의 종류를 표시하는 데 사용한다.
* FCS(Frame Check Sequence) : 전송시 에러를 체크
#### Multiplexing/Demultiplexing
* Multiplexing : 소켓을 통해 데이터를 전달받아 데이터를 모으고, 이를 세그먼트 단위로 묶어 생성하기 위해 세그먼트 앞에 헤더를 붙여 캡슐화하고, 이 세그먼트들은 네트워크 계층으로 내려보내는 작업
* Demultiplexing : 트랜스포트 계층에서 세그먼트의 데이터를 올바른 소켓으로 전달하는 작업
#### Half Duplex/Full Duplex
* Half Duplex : 송신과 수신을 한번씩 번갈아 가며 교대로 하는 방식으로 전송 중에는 수신할 수 없다.
* Full Deplex : 송신과 수신을 동시에 하는 방식으로 통신로를 분산하여 2배의 데이터 전송속도를 가진다.
#### 
